# Local Jenkins OpenId test - Login in Jenkins with Azure Entra Id

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/workflows/butlerwhale.jpg?raw=true" alt="butlerwhale" width="300" height="300">
</div>

## Objective 
Setting up a local Jenkins instance with OpenID Connect authentication using Docker containers. 

## Prerequisites

Before you begin, ensure you have the following installed:

- Docker

## Story Time

*In a bustling coral reef community, a cozy new workshop was being built by a Docker whale, where Jenkins, a diligent fish butler, would soon begin his work. One of their main concerns was securing the workshop by fitting a new lock on the front door.*

## Start Jenkins as container

*The fish and the whale began by setting up a cozy corner in their neighborhood. They needed to bring their workshop to life, so Jenkins could cheerfully go about his duties, much like a diligent housekeeper.*

### 1. Create a Docker network

*Docker and Jenkins decided to start by laying down pathways in their neighborhood, they established a connection.*

Open a terminal window and create a bridge network in Docker:

```bash
docker network create jenkins
```

### 2. Run Jenkins Docker image

*With the network in place, they proceed to welcome the new inhabitant to their underwater community.*

Execute the following command to run the Docker image for Jenkins:

```bash
docker run \
  --name jenkins-docker \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2
```

### 3. Create Dockerfile for custom Jenkins image

*Docker and Jenkins started by drafting a custom blueprint for their workshop. In this plan, they included all the necessary components to make their workshop unique.*

Create a file named 'Dockerfile' and add the following content:

```Dockerfile title="Dockerfile"
FROM jenkins/jenkins:2.440.3-jdk17
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean docker-workflow"
```

### 4. Build and run custom Jenkins image

*With the blueprint ready, Docker fired up and built a fresh workshop image from scratch. Jenkins watched eagerly as their creation took shape.*

Build a new Docker image from the Dockerfile:

```bash
docker build -t myjenkins-blueocean:2.440.3-1 .
```

Run the custom Jenkins image as a container:

```bash
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.440.3-1
```

### 5. Access Jenkins

*As the sunlight filtered through the water, Docker and Jenkins admired their handiwork as their workshop came to life, accessible with a flick of a fin. They retrieved the workshop keys from their treasure chest and unlocked the door to their new workspace.*

Jenkins is now accessible at http://localhost:8080/. Retrieve the initial password from the container logs using:

```bash
docker ps
docker logs -f <container_name>
```

## Install plugins

*Eager to enhance their workspace, Docker and Jenkins dove into a trove of plugins, much like searching for new tools in a reef. They carefully selected the ones that would streamline their workflow and improve productivity.*

These steps include the process to setup the login configuration as code. You can skip the "Configuration as Code" installation and still have a working login setup through interface.

### Through GUI

1. Connect to http://localhost:8080/.
2. Use the password retrieved earlier to login.
3. Navigate to **Dashboard** -> **Manage Jenkins** -> **Manage Plugins** -> **Available**.
4. Search and install "Configuration as Code" and "OpenId Connect Authentication".

Keep the last page open, so you can restart Jenkins later.

### Through CLI

1. Get into the Jenkins container shell:

```bash
docker ps
docker exec -it <container_name> bash
```

2. Inside the shell, install plugins:

```bash
jenkins-plugin-cli --plugins oic-auth:4.257.v5360e8489e8b_
jenkins-plugin-cli --plugins configuration-as-code:1775.v810dc950b_514
```

3. Restart Jenkins from the plugin installation section if needed.

## [Setup App registration](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/walkthrough-register-app-azure-active-directory)

*In the bustling reef marketplace, Docker and Jenkins registered their workshop as an official establishment. They filled out the necessary forms and secured access for themselves and their trusted collaborators.*

1. Login to [Azure Portal](https://portal.azure.com/). You need to have the necessary permissions, like *Application Developer*.
2. Navigate to **App registrations** and create a new app, name it something appropriate, like 'jenkins-oauth-sandbox'.
3. In **Authentication** menu add Redirect URIs: `http://localhost:8080/securityRealm/finishLogin`.
4. In **Certificate & secrets** create a new client secret, add a name like 'oauth' and save its value securely.
5. In **Owners**, 'Add owners', add all the users that will be able to authenticate. 

## Get data

*Armed with the necessary information, Docker and Jenkins swam through the reef to collect tokens and secrets for access. They made sure to keep everything organized in their treasure trove.*

Collect the following parameters for the OpenID Connect plugin configuration (not all of them mandatory, but you can easily get them):

- **tokenServerUrl**: *https://login.microsoftonline.com/123456a7-xxx-xxx-xxx-xxxx/oauth2/v2.0/token* In **Overview** -> **Endpoints** it's 'OAuth 2.0 authorization endpoint (v2)'.

- **authorizationServerUrl**: *https://login.microsoftonline.com/987654b3-xxx-xxx-xxx-xxxx/oauth2/v2.0/authorize* In **Overview** -> **Endpoints** it's 'OAuth 2.0 authorization endpoint (v2)'In **Overview** -> **Endpoints** It's 'OAuth 2.0 token endpoint (v2)'.

- **clientId**: *12345-xxx-xxx-xxx-xxxx* In **Overview** it's 'Application (client) ID'.

- **clientSecret**: *12345~a-xxx-xxx-xxxx* It's the secret you copied earlier from **Certificate & secrets**.

- **userNameField**: *preferred_username* default value, copy exactly this.

- **fullNameFieldName**: *name* default value, copy exactly this.

- **emailFieldName**: *email* default value, copy exactly this.

- **scopes**: *openid email profile* default value, copy exactly this.

## Manual Setup Jenkins

*With their paperwork in order, Docker and Jenkins dove into the settings of their workshop. They adjusted security settings and user permissions to ensure everything ran smoothly.*

1. Go to **Dashboard** -> **Manage Jenkins** -> **Security**.
2. Select *Security Realm* as *Login with OpenID Connect*.
3. Configure with *Manual configuration* and adjust *Advanced* options.

## Optional: Add escape hatch

*For added security, Docker and Jenkins installed an emergency escape tunnel, much like building a secret passage in their workshop. This provided a safe retreat in case access to their workshop was ever temporarily disrupted.*

**To access through 'escape hatch' you must add */login*, so go to http://localhost:8080/login .**

You can configure the option **Dashboard** -> **Manage Jenkis** -> **Security**

Selecting *Security Realm* as *Login with Openid Connect* and going into detail with *Manual configuration*, *Advanced*, and *Configure 'escape hatch' for when the OpenID Provider is unavailable*.

Then you activate the option from the interface and insert the credentials to login with.

## Optional: Configure Jenkins Using Configuration as Code

*In a final touch, Docker and Jenkins decided to automate their setup for their eventual future workshop. They codified their settings, ensuring consistency and ease of management.*

1. Navigate to **Dashboard** -> **Manage Jenkins** -> **Configuration as Code**.

2. Click on the **Download configuration** button to retrieve the current configuration in YAML format.

3. Open the downloaded `jenkins.yaml` file and locate the `jenkins.securityRealm.local` section.

4. Replace `jenkins.securityRealm.local` with `jenkins.securityRealm.oic` and insert the following configuration:

    ```yaml
    jenkins:
      securityRealm:
        oic:
          authorizationServerUrl: https://login.microsoftonline.com/987654b3-xxx-xxx-xxx-xxxx/oauth2/v2.0/authorize
          clientId: 12345-xxx-xxx-xxx-xxxx
          clientSecret: 12345~a-xxx-xxx-xxxx
          userNameField: preferred_username
          fullNameFieldName: name
          emailFieldName: email
          scopes: openid email profile
          tokenServerUrl: https://login.microsoftonline.com/123456a7-xxx-xxx-xxx-xxxx/oauth2/v2.0/token
          escapeHatchEnabled: true
          escapeHatchGroup: ''
          escapeHatchSecret: password
          escapeHatchUsername: test
    ```
    e.g:
    ```yaml title="jenkins.yaml"
    jenkins:
      agentProtocols:
      - "JNLP4-connect"
      - "Ping"
      authorizationStrategy:
        loggedInUsersCanDoAnything:
          allowAnonymousRead: false
      crumbIssuer:
        standard:
          excludeClientIPFromCrumb: false
      disableRememberMe: false
      labelAtoms:
      - name: "built-in"
      markupFormatter: "plainText"
      mode: NORMAL
      myViewsTabBar: "standard"
      nodeMonitors:
      - "architecture"
      - "clock"
      - diskSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "swapSpace"
      - tmpSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "responseTime"
      numExecutors: 2
      primaryView:
        all:
          name: "all"
      projectNamingStrategy: "standard"
      quietPeriod: 5
      remotingSecurity:
        enabled: true
      scmCheckoutRetryCount: 0
      securityRealm:
        local:
          allowsSignup: false
          enableCaptcha: false
          users:
          - id: "admin"
            name: "admin"
            properties:
            - "apiToken"
            - "consoleUrlProvider"
            - "mailer"
            - "myView"
            - preferredProvider:
                providerId: "default"
            - "timezone"
            - "experimentalFlags"
            - "favorite"
      slaveAgentPort: 50000
      updateCenter:
        sites:
        - id: "default"
          url: "https://updates.jenkins.io/update-center.json"
      views:
      - all:
          name: "all"
      viewsTabBar: "standard"
    globalCredentialsConfiguration:
      configuration:
        providerFilter: "none"
        typeFilter: "none"
    appearance:
      prism:
        theme: PRISM
    security:
      apiToken:
        creationOfLegacyTokenEnabled: false
        tokenGenerationOnCreationEnabled: false
        usageStatisticsEnabled: true
      gitHooks:
        allowedOnAgents: false
        allowedOnController: false
      gitHostKeyVerificationConfiguration:
        sshHostKeyVerificationStrategy: "knownHostsFileVerificationStrategy"
    unclassified:
      bitbucketEndpointConfiguration:
        endpoints:
        - bitbucketCloudEndpoint:
            enableCache: false
            manageHooks: false
            repositoriesCacheDuration: 0
            teamCacheDuration: 0
      buildDiscarders:
        configuredBuildDiscarders:
        - "jobBuildDiscarder"
      fingerprints:
        fingerprintCleanupDisabled: false
        storage: "file"
      gitHubConfiguration:
        apiRateLimitChecker: ThrottleForNormalize
      gitHubPluginConfig:
        hookUrl: "http://localhost:8080/github-webhook/"
      junitTestResultStorage:
        storage: "file"
      location:
        adminAddress: "address not configured yet <nobody@nowhere>"
      mailer:
        charset: "UTF-8"
        useSsl: false
        useTls: false
      pollSCM:
        pollingThreadCount: 10
      scmGit:
        addGitTagAction: false
        allowSecondFetch: false
        createAccountBasedOnEmail: false
        disableGitToolChooser: false
        hideCredentials: false
        showEntireCommitSummaryInChanges: false
        useExistingAccountWithSameEmail: false
      timestamper:
        allPipelines: false
        elapsedTimeFormat: "'<b>'HH:mm:ss.S'</b> '"
        systemTimeFormat: "'<b>'HH:mm:ss'</b> '"
    tool:
      git:
        installations:
        - home: "git"
          name: "Default"
      mavenGlobalConfig:
        globalSettingsProvider: "standard"
        settingsProvider: "standard"
    ```
    becomes:
    ```yaml title="updated-jenkins.yaml"
    jenkins:
      agentProtocols:
      - "JNLP4-connect"
      - "Ping"
      authorizationStrategy:
        loggedInUsersCanDoAnything:
          allowAnonymousRead: false
      crumbIssuer:
        standard:
          excludeClientIPFromCrumb: false
      disableRememberMe: false
      labelAtoms:
      - name: "built-in"
      markupFormatter: "plainText"
      mode: NORMAL
      myViewsTabBar: "standard"
      nodeMonitors:
      - "architecture"
      - "clock"
      - diskSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "swapSpace"
      - tmpSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "responseTime"
      numExecutors: 2
      primaryView:
        all:
          name: "all"
      projectNamingStrategy: "standard"
      quietPeriod: 5
      remotingSecurity:
        enabled: true
      scmCheckoutRetryCount: 0
      securityRealm:
        oic:
          authorizationServerUrl: https://login.microsoftonline.com/987654b3-xxx-xxx-xxx-xxxx/oauth2/v2.0/authorize
          clientId: 12345-xxx-xxx-xxx-xxxx
          clientSecret: 12345~a-xxx-xxx-xxxx
          userNameField: preferred_username
          fullNameFieldName: name
          emailFieldName: email
          scopes: openid email profile
          tokenServerUrl: https://login.microsoftonline.com/123456a7-xxx-xxx-xxx-xxxx/oauth2/v2.0/token
          escapeHatchEnabled: true
          escapeHatchGroup: ''
          escapeHatchSecret: password
          escapeHatchUsername: test
      slaveAgentPort: 50000
      updateCenter:
        sites:
        - id: "default"
          url: "https://updates.jenkins.io/update-center.json"
      views:
      - all:
          name: "all"
      viewsTabBar: "standard"
    globalCredentialsConfiguration:
      configuration:
        providerFilter: "none"
        typeFilter: "none"
    appearance:
      prism:
        theme: PRISM
    security:
      apiToken:
        creationOfLegacyTokenEnabled: false
        tokenGenerationOnCreationEnabled: false
        usageStatisticsEnabled: true
      gitHooks:
        allowedOnAgents: false
        allowedOnController: false
      gitHostKeyVerificationConfiguration:
        sshHostKeyVerificationStrategy: "knownHostsFileVerificationStrategy"
    unclassified:
      bitbucketEndpointConfiguration:
        endpoints:
        - bitbucketCloudEndpoint:
            enableCache: false
            manageHooks: false
            repositoriesCacheDuration: 0
            teamCacheDuration: 0
      buildDiscarders:
        configuredBuildDiscarders:
        - "jobBuildDiscarder"
      fingerprints:
        fingerprintCleanupDisabled: false
        storage: "file"
      gitHubConfiguration:
        apiRateLimitChecker: ThrottleForNormalize
      gitHubPluginConfig:
        hookUrl: "http://localhost:8080/github-webhook/"
      junitTestResultStorage:
        storage: "file"
      location:
        adminAddress: "address not configured yet <nobody@nowhere>"
      mailer:
        charset: "UTF-8"
        useSsl: false
        useTls: false
      pollSCM:
        pollingThreadCount: 10
      scmGit:
        addGitTagAction: false
        allowSecondFetch: false
        createAccountBasedOnEmail: false
        disableGitToolChooser: false
        hideCredentials: false
        showEntireCommitSummaryInChanges: false
        useExistingAccountWithSameEmail: false
      timestamper:
        allPipelines: false
        elapsedTimeFormat: "'<b>'HH:mm:ss.S'</b> '"
        systemTimeFormat: "'<b>'HH:mm:ss'</b> '"
    tool:
      git:
        installations:
        - home: "git"
          name: "Default"
      mavenGlobalConfig:
        globalSettingsProvider: "standard"
        settingsProvider: "standard"
    ```

5. Save the changes and close the file.

6. Connect to the Jenkins Docker container's shell:

    ```bash
    docker ps
    docker exec -it <container_name> bash
    ```

7. In the Docker container shell, navigate to the home directory:

    ```bash
    cd
    pwd
    ```

8. Create a new file named `conf.yaml` and paste the content of the updated `jenkins.yaml` file into it(you may need to escape with '\' the '<''>' characters in the date format). From command line you use the commands:

    ```bash
    echo '<updated-jenkinsfile.yaml_content>' > conf.yaml
    ```

    e.g.:

    ```bash
    echo 'jenkins:
      agentProtocols:
      - "JNLP4-connect"
      - "Ping"
      authorizationStrategy:
        loggedInUsersCanDoAnything:
          allowAnonymousRead: false
      crumbIssuer:
        standard:
          excludeClientIPFromCrumb: false
      disableRememberMe: false
      labelAtoms:
      - name: "built-in"
      markupFormatter: "plainText"
      mode: NORMAL
      myViewsTabBar: "standard"
      nodeMonitors:
      - "architecture"
      - "clock"
      - diskSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "swapSpace"
      - tmpSpace:
          freeSpaceThreshold: "1GiB"
          freeSpaceWarningThreshold: "2GiB"
      - "responseTime"
      numExecutors: 2
      primaryView:
        all:
          name: "all"
      projectNamingStrategy: "standard"
      quietPeriod: 5
      remotingSecurity:
        enabled: true
      scmCheckoutRetryCount: 0
      securityRealm:
        oic:
          authorizationServerUrl: https://login.microsoftonline.com/987654b3-xxx-xxx-xxx-xxxx/oauth2/v2.0/authorize
          clientId: 12345-xxx-xxx-xxx-xxxx
          clientSecret: 12345~a-xxx-xxx-xxxx
          userNameField: preferred_username
          fullNameFieldName: name
          emailFieldName: email
          scopes: openid email profile
          tokenServerUrl: https://login.microsoftonline.com/123456a7-xxx-xxx-xxx-xxxx/oauth2/v2.0/token
          escapeHatchEnabled: true
          escapeHatchGroup: ''
          escapeHatchSecret: password
          escapeHatchUsername: test
      slaveAgentPort: 50000
      updateCenter:
        sites:
        - id: "default"
          url: "https://updates.jenkins.io/update-center.json"
      views:
      - all:
          name: "all"
      viewsTabBar: "standard"
    globalCredentialsConfiguration:
      configuration:
        providerFilter: "none"
        typeFilter: "none"
    appearance:
      prism:
        theme: PRISM
    security:
      apiToken:
        creationOfLegacyTokenEnabled: false
        tokenGenerationOnCreationEnabled: false
        usageStatisticsEnabled: true
      gitHooks:
        allowedOnAgents: false
        allowedOnController: false
      gitHostKeyVerificationConfiguration:
        sshHostKeyVerificationStrategy: "knownHostsFileVerificationStrategy"
    unclassified:
      bitbucketEndpointConfiguration:
        endpoints:
        - bitbucketCloudEndpoint:
            enableCache: false
            manageHooks: false
            repositoriesCacheDuration: 0
            teamCacheDuration: 0
      buildDiscarders:
        configuredBuildDiscarders:
        - "jobBuildDiscarder"
      fingerprints:
        fingerprintCleanupDisabled: false
        storage: "file"
      gitHubConfiguration:
        apiRateLimitChecker: ThrottleForNormalize
      gitHubPluginConfig:
        hookUrl: "http://localhost:8080/github-webhook/"
      junitTestResultStorage:
        storage: "file"
      location:
        adminAddress: "address not configured yet <nobody@nowhere>"
      mailer:
        charset: "UTF-8"
        useSsl: false
        useTls: false
      pollSCM:
        pollingThreadCount: 10
      scmGit:
        addGitTagAction: false
        allowSecondFetch: false
        createAccountBasedOnEmail: false
        disableGitToolChooser: false
        hideCredentials: false
        showEntireCommitSummaryInChanges: false
        useExistingAccountWithSameEmail: false
      timestamper:
        allPipelines: false
        elapsedTimeFormat: "'\<b\>'HH:mm:ss.S'\</b\> '"
        systemTimeFormat: "'\<b\>'HH:mm:ss'\</b\> '"
    tool:
      git:
        installations:
        - home: "git"
          name: "Default"
      mavenGlobalConfig:
        globalSettingsProvider: "standard"
        settingsProvider: "standard"' > conf.yaml
    ```

9. Once `conf.yaml` is created, exit the Docker container shell.

10. Return to [http://localhost:8080/manage/configuration-as-code/](http://localhost:8080/manage/configuration-as-code/).

11. In the **Path or URL** field, enter:

    ```
    /var/jenkins_home/conf.yaml
    ```

12. Click **Apply new configuration** to update Jenkins with the new configuration.


*With their workshop now revamped and secured, Docker and Jenkins floated contentedly, ready to tackle their projects with renewed energy and efficiency.*

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="wiz" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="wiz" width="150" height="150">
  </a>
</div>