**Task:** Convert this ALPS profile into a comprehensive OpenAPI 3.1 specification.

**Key Instructions:**

1. **State to Endpoint Mapping:**
   - Map each semantic state to a resource endpoint
   - Use tag attributes to organize endpoints into logical groups
   - Apply proper REST principles (plural nouns for collections, etc.)

2. **Transition Operations:**
   - Convert transitions with specific type attributes:
     - `safe` → GET operations
     - `unsafe` → POST operations 
     - `idempotent` → PUT/PATCH operations
     - Include DELETE operations for removal actions
   - Use appropriate HTTP status codes (200, 201, 204, 400, 404, etc.)

3. **Schema Definitions:**
   - Build schemas from semantic descriptors
  - If a `def` attribute is present in a semantic descriptor (e.g., pointing to a Schema.org URI), include it in the OpenAPI schema as `x-semantic`.
  - This provides semantic grounding for documentation, code generation, and external tool compatibility.
  - Example:
    ```yaml
    email:
      type: string
      format: email
      title: Email address
      description: Email address of the person
      x-semantic: https://schema.org/email
    ```

   - Include all properties referenced in state descriptors
   - Use Schema.org definitions when available via `def` attributes
   - Apply proper validation constraints based on domain knowledge
   - Create both request and response schemas
  - Include example values using the `example` attribute on each property within the schema (e.g., `email`, `status`).
  - Do not use top-level `example` blocks alongside `$ref` in request/response bodies, as this is not supported by all OpenAPI tools.
  - Example:
    ```yaml
    email:
      type: string
      format: email
      title: Email address
      description: Email address associated with the person
      x-semantic: https://schema.org/email
      example: "jane.doe@example.com"
    ```


4. **Complete Documentation:**
   - Use titles as summary descriptions
   - Convert doc attributes to detailed descriptions
   - Include examples for each operation
   - Document error responses and handling

5. **Consistent Design:**
   - Apply query parameters for filtering, sorting, pagination  
  - For ALPS transitions with `type: safe` and `rel` including terms like `filter` or `search` (e.g., `goFilter`), treat all referenced `descriptor.href` items as query parameters.
  - Use the referenced semantic descriptor's `id` as the parameter name.
  - Use its `title` and `doc.value` (if available) as the OpenAPI `description`.
  - Set `in: query` and `required: false` in the OpenAPI parameter.

   - Use path parameters for resource identifiers
   - Include security schemes appropriate for the domain
   - Ensure all endpoints have complete request/response documentation

**Output Format:** Provide YAML format with appropriate indentation and organization.

