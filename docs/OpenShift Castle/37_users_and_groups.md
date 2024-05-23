# Users and Groups

<div style="text-align:center;">
  <img src="https://github.com/Vitrua/images/blob/main/openshift/usersgroups.jpg?raw=true" alt="users_groups" width="300" height="300">
</div>

## Objective

Understand the primary resources for authentication and access control in OpenShift, including users, identities, service accounts, groups, and roles, to manage permissions and secure interactions with the API server.

## Prerequisites

- Access to an OpenShift cluster or a terminal emulator connected to one.
- Basic knowledge of OpenShift concepts and command-line interfaces (CLI).

## Introduction

Greetings, vigilant guardian of the OpenShift kingdom! In your realm, managing who has access to what is paramount to maintaining order and security. OpenShift provides several resources to help you govern interactions with the API server. By understanding and utilizing users, identities, service accounts, groups, and roles, you can assign permissions effectively and safeguard your kingdom's integrity. Join us as we explore these essential elements of authentication and access control, and ensure your realm remains secure and well-regulated.

## Primary Resources for Authentication

### User

In the bustling marketplace of your kingdom, the **User** is like a citizen with a unique identity. These entities interact with the API server and represent actors within the system. Permissions for users can be assigned directly or through membership in groups.

- **Usage**: Users can perform various tasks and actions within the OpenShift environment, granted through role assignments.

### Identity

**Identity** serves as the record keeper, documenting successful authentication attempts by users and identity providers. It stores data about the authentication source, ensuring that each interaction is traceable to its origin.

- **Usage**: Helps track authentication sources and verify user legitimacy within the kingdom.

### Service Account

A **Service Account** is akin to a trusted envoy, allowing applications to communicate independently with the API server. By using service accounts, you preserve the integrity of user credentials and avoid the risks associated with sharing them.

- **Usage**: Ensures secure application communication without exposing user credentials.

### Group

**Group** represents specific sets of users, much like guilds or councils within your kingdom. By assigning permissions to groups, you can collectively manage access for multiple users, streamlining the process of role assignment.

- **Usage**: Simplifies permission management by grouping users with similar roles or responsibilities.

### Role

The **Role** is the decree that defines what API operations users, groups, and service accounts can perform. Roles are granted through assignments, empowering actors within the system to carry out their duties effectively.

- **Usage**: Specifies permissions and access levels, ensuring that actors can perform necessary tasks while maintaining security.

## Conclusion

Noble custodian of the OpenShift kingdom, you now possess the knowledge to manage users and groups effectively. By understanding the roles of users, identities, service accounts, groups, and roles, you can govern interactions with the API server, ensuring that your realm remains secure and well-regulated. Embrace these resources to assign permissions wisely, safeguard credentials, and maintain the integrity of your kingdom.

With these skills, you are equipped to uphold order and security within your domain, ensuring that all actors can perform their duties while protecting the kingdom's treasures. Your vigilant management of users and groups fortifies your realm, keeping it safe and thriving under your wise and watchful eye.

<div style="text-align:center;">
  <a href="https://patreon.com/Vitrua">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmonlight.png?raw=true#only-light" alt="support" width="150" height="150">
    <img src="https://github.com/Vitrua/images/blob/main/others/supportmon.png?raw=true#only-dark" alt="support" width="150" height="150">
  </a>
</div>
