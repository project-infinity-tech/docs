---
title: "Understanding User Management"
description: "An overview of how users, authentication, and roles work in Scram."
---

Scram has a built-in user management system that handles authentication, roles, and access control out of the box. You don't need a third-party auth service — it's all part of the platform.

---

## The Users table

Every Scram project has a built-in `Users` table. Unlike regular database tables, it uses a UUID rather than an integer as its primary key, and it comes with a fixed set of built-in fields covering authentication type, profile information, roles, and account status.

You can add custom fields to the Users table just like any other table — useful for storing app-specific profile data like subscription tier, onboarding status, or company name.

See [The User Table](/understanding/subpages/the-user-table) for the full field reference.

---

## Authentication

Scram supports two types of authentication out of the box:

**Email and password** — enabled by default on every new project.

**Social login** — Google, Facebook, and Microsoft can be enabled from the [Users](/resources/users) section of the Resource View. Each provider requires OAuth credentials from the provider's developer console.

See [Setting Up Google Login](/understanding/subpages/setting-up-google-login) for a step-by-step example of configuring a social provider.

---

## Roles

Roles control what users can access in your app. Every project starts with two default roles — **Registered User** and **Admin**. You can add more but not delete them.

Roles are assigned to users in the `roles` column of the Users table — stored as a text array. Users sign up with no roles by default, so your signup workflow must explicitly assign at least one role.

Roles are referenced by their **ID** (not their display name) in SQL queries, RLS policies, and expressions.

---

## Row Level Security

RLS policies on your database tables use role and user ID checks to control which rows each user can read, write, update, or delete. The standard pattern is `"ownerId" = auth.user_id()` for user-owned data, with role checks for admin access.

See [Row Level Security](/understanding/understanding-row-level-security) for full details.

---

## Signing users up

Scram provides built-in signup actions — **Signup with Email and Password** and **Signup or Login with Social Provider**. After a successful signup, your workflow should immediately assign a role to the new user and call **Reload User** to refresh the session.

See [Signing Users Up](/understanding/subpages/signing-users-up) for the full signup pattern.

---

## Access control

Access can be controlled at three levels:

**Page authorisation** — restrict which roles can access a page. Unauthenticated or unauthorised users are redirected to a page you specify in [Frontend Configuration](/understanding/subpages/frontend-configuration).

**Workflow authorisation** — restrict which roles can trigger a workflow. Workflows inherit their page's auth settings by default and can be overridden individually.

**Row Level Security** — restrict which rows a user can read or write at the database level.

See [Workflow Auth](/understanding/subpages/workflow-auth) and [Page Authorisation](/understanding/subpages/page-authorisation) for more detail.

---

## API Tokens

For third-party or service-level access, Scram supports API tokens. A token is generated for a dedicated user record and carries specific roles, giving that token exactly the permissions it needs and no more.

See the [Users](/resources/users) resource page for full details on generating and managing tokens.