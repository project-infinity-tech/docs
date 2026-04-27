---
title: "Data Sources - API Calls"
---

Scram handles API calls by importing text files (or URLS to those text files) that describe how these APIs function. This makes it quicker and simpler for the user, as most API calls have already been specified (often by the provider) and can, therefore, just be imported and used immediately rather than manually typing out URLs and Parameters.

Unlike cURL, which describes a single API call, Scram is able to import multiple API calls in one file, which includes all the calls, authorisation, descriptions and data structures associated with this set of API calls.

The following formats are supported:

- OpenAPI 3.0 / 3.1
  - OpenAPI is the generally accepted standard for describing RESTful APIs. It is both human and machine-readable.
- Postman export
  - Postman one of the most widely used API management platforms.
  - Many API providers provide their APIs as a regularly updated “collection” on POSTman that can be tested on their platform before being used in an app.
  - Note that Postman can read OpenAPI files but not export them

OpenAPI provides the following over and above the basic “call”

- Metadata
  - **Title**: The name of the API.
  - **Version**: The version of the API (e.g., `v1`, `v2`).
  - **Description**: A brief or detailed description of what the API does.
  - **Terms of Service**: Optional terms and conditions for using the API.
  - **Contact Information**: Contact details for support or questions (e.g., name, email).
  - **License**: Information about the licensing of the API (e.g., MIT, Apache 2.0).
- Server Information
  - **Base URL**: The root URL(s) where the API is hosted.
  - **Server Variables**: Placeholder variables for URLs (e.g., `{environment}.api.example.com`).
  - **Environments**: Definitions for production, staging, development, etc
- Paths - each endpoint in the API
  - **HTTP Methods**: `GET`, `POST`, `PUT`, `DELETE`, etc.
  - **Parameters**: Query, path, header, or cookie parameters.
  - **Request Body**: The structure and content of the request payload for applicable methods.
  - **Responses**: Expected response codes (`200`, `404`, `500`, etc.) and their schemas.
- Components - Reusable data that can be referenced throughout the specification:
  - **Schemas**: Data models used in request and response payloads.
  - **Parameters**: Common parameters that can be reused across multiple endpoints.
  - **Headers**: Custom headers used in requests or responses.
  - **Security Schemes**: Authentication and authorization methods (e.g., API keys, OAuth2, JWT).
  - **Examples**: Predefined examples for requests or responses.
  - **Request Bodies**: Common request payload definitions.
- Security -  the security mechanisms used by the API.
  - API keys (query, header, or cookie).
  - OAuth 2.0 flows (e.g., implicit, password, client credentials).
  - HTTP authentication (e.g., Basic, Bearer).
- Tags - Logical grouping of endpoints for better organization
  - Note that this is currently not all that well supported
- External Documentation - Links to additional resources, guides, or documentation relevant to the API.
- Callbacks - Describes asynchronous operations or webhooks the API supports