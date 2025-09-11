# OpenAPI Specification Standards

The OpenAPI Specification (OAS) defines a standard, language-agnostic interface to HTTP APIs, allowing both humans and computers to understand the capabilities of services without requiring access to source code or documentation inspection.

## Key Concepts

- **OpenAPI Description (OAD)**: A formal definition of an API's surface and semantics, composed of an entry document and referenced documents
- **OpenAPI Document**: A single JSON or YAML document that conforms to the OpenAPI Specification
- **Schema**: A formal description of syntax and structure, based on JSON Schema

## Core Structure

- **openapi**: REQUIRED field specifying the version number of the OAS being used
- **info**: REQUIRED object providing metadata about the API (title, version, etc.)
- **servers**: Array of server objects providing connectivity information
- **paths**: Available paths and operations for the API
- **components**: Reusable objects for the specification (schemas, responses, parameters, etc.)
- **security**: Declaration of security mechanisms that can be used across the API
- **tags**: Optional list of tags for organizing operations
- **externalDocs**: Additional external documentation

## Path Items and Operations

- Paths are defined as relative URLs to individual endpoints
- Each path can support multiple operations (GET, POST, PUT, DELETE, etc.)
- Operations include parameters, request bodies, responses, and callbacks
- Path templating allows for parameterized URLs with curly braces (e.g., `/users/{id}`)

## Data Types and Schemas

- Based on JSON Schema Validation Specification Draft 2020-12
- Supports primitive types: null, boolean, object, array, number, string
- Schema Objects can use patterns, validations, examples, and extended keywords
- Binary data can be handled in raw or encoded form

## Request/Response Structure

- Parameters can be defined in path, query, header, or cookie
- Request bodies specify the content for API calls
- Responses are mapped to HTTP status codes
- Content types are specified using Media Type Objects

## Reusable Components

- Schema Objects for data models
- Response Objects for API responses
- Parameter Objects for operation parameters
- Example Objects for providing examples
- Request Body Objects for request payloads
- Header Objects for custom headers
- Security Scheme Objects for security definitions
- Link Objects for specifying relations between operations

## Security

- Supports multiple security mechanisms: API key, HTTP authentication, OAuth2, OpenID Connect
- Security requirements can be defined globally or per-operation
- OAuth flows can be configured with scopes and endpoints

## Documentation Features

- Supports CommonMark markdown for rich text descriptions
- Examples can be embedded or referenced externally
- Tags provide a way to group operations

## Extensions

- Allows extending the specification with custom properties
- Extension fields are prefixed with `x-`

## File Structure

- Can be a single file or split across multiple files using references
- References use JSON Pointer syntax or full URLs
- Components can be reused across multiple documents

## Formats

- Supports both JSON and YAML formats
- YAML version 1.2 is recommended for compatibility

## Versioning

- Uses semantic versioning (major.minor.patch)
- Tooling supporting OAS 3.1 should be compatible with all 3.1.x versions
