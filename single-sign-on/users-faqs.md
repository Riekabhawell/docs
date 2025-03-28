---
description: Single Sign-on FAQs
keywords: Docker, Docker Hub, SSO FAQs, single sign-on
title: Manage users
---

### How do I manage users when using SSO?

Users are managed through organizations in Docker Hub. When you configure SSO in Docker, you need to make sure an account exists for each user in your IdP account. When a user signs in to Docker for the first time using their domain email address, they will be automatically added to the organization after a successful authentication.

### Do I need to manually add users to my organization?

No, you don’t need to manually add users to your organization in Docker Hub. You just need to make sure an account for your users exists in your IdP. When users sign in to Docker Hub, they're automatically assigned to the organization using their domain email address.

When a user signs into Docker for the first time using their domain email address, they will be automatically added to the organization after a successful authentication.

### Can users in my organization use different email addresses to authenticate through SSO?

During the SSO setup, you’ll have to specify the company email domains that are allowed to authenticate. All users in your organization must authenticate using the email domain specified during SSO setup. Some of your users may want to maintain a different account for their personal projects.

Users with a public domain email address will be added as guests.

### Can Docker org owners/Admins/company owners approve users to an organization and use a seat, rather than having them automatically added when SSO Is enabled?

Admins, organization owners and company owners can currently approve users by configuring their permissions through their IdP. That's if the user account is configured in the IdP, the user will be automatically added to the organization in Docker Hub as long as there’s an available seat.

### How will users be made aware that they're being made a part of a Docker Org?

When SSO is enabled, users will be prompted to authenticate through SSO the next time they try to sign in to Docker Hub or Docker Desktop. The system will see the end-user has a domain email associated with the docker ID they're trying to authenticate with, and prompts them to sign in with SSO email and credentials instead.

If users attempt to sign in through the CLI, they must authenticate using a personal access token (PAT).

### Is it possible to force users of Docker Desktop to authenticate, and/or authenticate using their company’s domain?

Yes. Admins can force users to authenticate with Docker Desktop by provisioning a [`registry.json`](../docker-hub/configure-sign-in.md) configuration file. The `registry.json` file will force users to authenticate as a user that's configured in the `allowedOrgs` list in the `registry.json` file.

Once SSO enforcement is set up on their Docker Business organisation or company on Hub, when the user is forced to authenticate with Docker Desktop, the SSO enforcement will also force users to authenticate through SSO with their IdP (instead of authenticating using their username and password).

Users may still be able to authenticate as a "guest" account using a non-domain email address. However, they can only authenticate as guests if that non-domain email was invited.

### Is it possible to convert existing users from non-SSO to SSO accounts?

Yes, you can convert existing users to an SSO account. To convert users from a non-SSO account:

* Ensure your users have a company domain email address and they have an account in your IdP
* Verify that all users have Docker Desktop version 4.4.2 or later installed on their machines
* Each user has created a PAT to replace their passwords to allow them to sign in through Docker CLI
* Confirm that all CI/CD pipelines automation systems have replaced their passwords with PATs.

For detailed prerequisites and instructions on how to enable SSO, see [Configure Single Sign-on](index.md).

### What impact can users expect once we start onboarding them to SSO accounts?

When SSO is enabled and enforced, your users just have to sign in using the email address and password.

### Is Docker SSO fully synced with Active Directory (AD)?

Docker doesn’t currently support a full sync with AD. That's, if a user leaves the organization, administrators must sign in to Docker Hub and manually [remove the user](/docker-hub/members/#remove-a-member-or-invitee) from the organization.

Additionally, you can use our APIs to complete this process.

### What's the best way to provision the Docker Subscription without SSO?

Company or organisation owners can invite users through Docker Hub UI, by email address (for any user) or by Docker ID (assuming the user has created a user account on Hub already).

### If we add a user manually for the first time, can I register in the dashboard and will the user get an invitation link through email?

Yes, if the user is added through email address to an org, they will receive an email invite. If invited through Docker ID as an existing user instead, they'll be added to the organization automatically. A new invite flow will occur in the near future that will require an email invite (so the user can choose to opt out). If the org later sets up SSO for [zeiss.com](https://www.zeiss.com/) domain, the user will automatically be added to the domain SSO org next sign in which requires SSO auth with the identity provider (Hub login will automatically redirect to the identity provider).

### Can someone join an organization without an invitation? Is it possible to put specific users to an organization with existing email accounts?

Not without SSO. Joining requires an invite from a member of the Owners group. When SSO is enforced, then the domains verified through SSO will allow users to automatically join the organization the next time they sign in as a user that has a domain email assigned.

### When we send an invitation to the user, will the existing account be consolidated and retained?

Yes, the existing user account will join the organization with all assets retained.

### How can I view, update, and remove multiple email addresses for my users?

We only support one email per user on the Docker platform.

### How can I remove invitees to the org who haven't signed in?

They can go to the invitee list in the org view and remove them.

### How's the flow for service account authentication different from a UI user account?

It isn't; we don't differentiate the two in product.

