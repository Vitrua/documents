# Certificates Management

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/certman.jpg?raw=true" alt="certman" width="300" height="300">
</div>

## Objective

Learn to manage certificates in OpenShift to ensure secure communication. This includes generating service certificates, configuring client applications to trust these certificates, and handling key rotation. Additionally, explore alternatives such as service mesh and the cert-manager operator for advanced encryption solutions.

## Introduction

In the ancient kingdom of OpenShift, where the digital fortress stands tall, the mantra of zero-trust is the law of the land. Here, every communication is encrypted, every certificate is meticulously vetted, and trust is a privilege earned through rigorous validation. The king's court, comprising administrators and guardians, ensures that all network traffic is secure, safeguarding the kingdom from unseen threats.

## Service Certificates and Creation

In this fortified realm, the royal scribes, known as the *service-ca* controllers, generate and sign service certificates for internal traffic. These certificates, much like royal seals, authenticate and protect the messages exchanged within the kingdom.

### Generating a Certificate and Key Pair

To obtain a royal seal, you must send a formal request to the scribes. This is done by annotating the service with `service.beta.openshift.io/serving-cert-secret-name=your-secret`. It's akin to placing a request in the royal register for a sealed document.

```bash
oc annotate service my-app service.beta.openshift.io/serving-cert-secret-name=my-app-secret
```

Once the scribes generate the secret, it must be securely delivered and mounted in the application deployment, just like delivering the sealed decree to its rightful place in the castle.

```yaml
spec:
  template:
    spec:
      containers:
        - name: my-app
          volumeMounts:
            - name: my-app-volume
              mountPath: /etc/pki/nginx/
      volumes:
        - name: my-app-volume
          secret:
            defaultMode: 420
            secretName: my-app-secret
            items:
              - key: tls.crt
                path: server.crt
              - key: tls.key
                path: private/server.key
```

### Client Service Application Configuration

For a client service application to trust a certificate, it needs the CA bundle that signed the certificate. The *service-ca* controller, acting as the royal notary, injects the CA bundle when you apply the `service.beta.openshift.io/inject-cabundle=true` annotation. This ensures that the client can verify the authenticity of the certificate, much like checking the royal seal on a document.

```bash
oc annotate configmap ca-bundle service.beta.openshift.io/inject-cabundle=true
```

### Key Rotation

In the kingdom of OpenShift, the validity of certificates is carefully managed. The service CA certificate is valid for 26 months and is automatically rotated after 13 months. There is a 13-month grace period where the original CA certificate remains valid, allowing for a seamless transition. This is much like updating royal decrees periodically to maintain their legitimacy and authority.

Should the need arise, you can manually rotate the certificates by deleting existing secrets, akin to a royal edict declaring the replacement of old seals with new ones:

```bash
oc delete secret certificate-secret
oc delete secret/signing-key -n openshift-service-ca
```

## Alternatives to Service Certificates

The kingdom of OpenShift also offers alternative methods to ensure TLS encryption within its borders, akin to various layers of protection around the castle.

### Service Mesh

A service mesh creates a network of secured passageways within the castle, ensuring that every interaction between services is encrypted and protected. This is like having an intricate system of guarded tunnels connecting different parts of the fortress.

### Cert-Manager Operator

The cert-manager operator acts like a trusted envoy, delegating the task of certificate signing to a reliable external service. This allows the kingdom to maintain the integrity of its communications through trusted external partners.

### Red Hat OpenShift Service Mesh

Red Hat OpenShift Service Mesh provides advanced functionalities for encrypted communication between services. It is akin to having an elite team of royal guards dedicated to ensuring that every message and interaction within the kingdom is secure and trustworthy.

## Conclusion

In the realm of OpenShift, zero-trust environments are the cornerstone of security. By using trusted certificates, automating key rotations, and exploring advanced options like service mesh and cert-manager, the kingdom remains vigilant and well-protected from external threats. As guardians of this digital fortress, administrators must continuously ensure the integrity and security of all communications within the castle walls.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
