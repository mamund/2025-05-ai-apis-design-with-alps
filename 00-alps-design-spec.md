
**ALPS: Application-Level Profile Semantics - Comprehensive Specification & Design Guide**

**Section 0: Core Definitions & Purpose**

**0.1. ALPS (Application-Level Profile Semantics): Definition**
*   **Format Type:** Data format.
*   **Primary Function:** Describes application-level semantics.
*   **Mechanism:** Augments generic media types (e.g., JSON, HTML) with application-specific:
    *   Meaning (semantics)
    *   Structure
    *   Operations (affordances)
*   **Abstraction Level:** Abstract, protocol-independent.
*   **Core Components Modeled:**
    *   Application "Vocabulary": Semantic descriptors.
    *   Application "Grammar": State transitions, affordances.
*   ALPS is pronounced 'alps', the same as the Swiss Alps. It is not A-L-P-S. "/ælps/"

**0.2. ALPS: Key Objectives & Benefits**
*   **Objective: Shared Semantic Understanding**
    *   *Benefit:* Common language for stakeholders (designers, developers, product owners).
    *   *Impact:* Efficient communication, reduced ambiguity.
*   **Objective: System Interoperability**
    *   *Benefit:* Standardized meaning of data and operations.
    *   *Impact:* Simplified integration between disparate systems.
*   **Objective: API/Service Reusability & Discoverability**
    *   *Benefit:* Clearer API/service semantics.
    *   *Impact:* Enhanced understanding, reuse, and discovery.
*   **Objective: Development Efficiency**
    *   *Benefit:* Early clarification of application logic and data semantics.
    *   *Impact:* Minimized rework, consistent API implementation.
*   **Objective: Domain Model Stability (Protocol Agnostic)**
    *   *Benefit:* Focus on abstract business logic.
    *   *Impact:* Core domain model (defined in ALPS) remains valid despite changes in underlying protocols (e.g., REST, GraphQL) or architectural styles.

**0.3. ASD (Application State Diagram): ALPS Visualization**
*   **Tool Type:** Visualization tool.
*   **Input:** ALPS document.
*   **Output:** Diagram of application states and transitions.
*   **Primary Function:** Provides intuitive, visual understanding of:
    *   Application overall structure.
    *   State transitions.
    *   Available actions per state.
*   **Key Benefits for Design & Development:**
    *   Visual clarity of application flows.
    *   Enhanced cross-functional team collaboration (shared perspective).
    *   Early identification/resolution of design flaws.
    *   Increased project transparency.

**Part 1: ALPS Foundational Principles**

**Section 1.1: ALPS and Information Architecture (IA)**
*   **IA Core Concepts in ALPS:**
    *   **Meaning:** Clarified by ALPS semantic descriptors.
    *   **Structure:** Defined by ALPS descriptor hierarchies and relationships.
    *   **Interaction:** Modeled by ALPS state transitions and operations.
*   **Dan Klyn's IA Framework (Foundation for ALPS Domain Modeling):**
    *   **Ontology (What things mean):**
        *   *ALPS Implementation:* `semantic` descriptors define terms and concepts. External definitions (e.g., Schema.org) can be linked via the `def` attribute. Documentation is provided via `doc` elements.
    *   **Taxonomy (How things are organized and related):**
        *   *ALPS Implementation:* `semantic` descriptors represent application states or complex data types. These group other descriptors (data elements, affordances/transitions) to define information structure and composition.
    *   **Choreography (How things work; interactions):**
        *   *ALPS Implementation:* `safe`, `idempotent`, and `unsafe` descriptors represent operations and state transitions. The `rt` (return type) attribute specifies the resulting application state.
*   **ALPS vs. OpenAPI in Design Focus:**
    *   **OpenAPI:** Focuses on technical API details (endpoints, HTTP methods, request/response structures).
    *   **ALPS:** Focuses on business domain semantics and structure using IA concepts.

**Section 1.2: Role of ALPS in the Design Process**
*   **Function: Bridge Business Requirements and System Design**
    *   *Applicability:* From requirements definition phase onwards (unlike endpoint-centric design).
    *   *Benefit:* Early detection and correction of differing interpretations of business requirements. Establishes common language between business and technical teams.
*   **Function: Single Source of Truth (SSOT) for Domain Knowledge**
    *   *Scope:* Beyond API endpoint design; systematizes and shares business domain knowledge.
    *   *Mechanism:* Consistently models system structure and behavior using business terminology.
    *   *Output:* Clear expression of complex business rules, visualized workflows, intuitive understanding of information interactions.
*   **Function: Adaptability to Technical Changes**
    *   *Characteristic:* Flexibility in application to various API styles (REST, GraphQL, microservices, new protocols).
    *   *Reason:* ALPS focuses on abstracted business logic, not implementation details. Domain models defined in ALPS remain valid even if technology or architecture changes.

**Section 1.3: Building a Sustainable Knowledge Foundation**
*   **Taxonomy Implementation:**
    *   Defines relationships between business entities.
    *   Ensures scalability through hierarchical structure.
    *   Establishes a common vocabulary across the organization, streamlining communication.
*   **Choreography Implementation:**
    *   Defines business process flows and service coordination rules.
    *   Enhances system-wide consistency and reliability.
*   **Outcome:** Systematic structuring and evolution of organizational knowledge, resilient to technological changes, by connecting technical implementation with business requirements through the ALPS framework.

**Part 2: ALPS Tutorials**

**Section 2.1: Basic ALPS Tutorial**
*   **Objective:** Learn basic ALPS usage through hands-on practice.
*   **Prerequisites:** ALPS Editor (e.g., `https://editor.app-state-diagram.com/`). Start with an empty editor pane.

    **2.1.1. Step 1: Prepare an Empty ALPS File**
    *   **Purpose:** Establishes the minimum required structure for an ALPS document.
    *   **Formats:** XML or JSON. Functionally equivalent.
    *   **Schema Reference (XML):** `xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd"`
        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <alps
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd">
        </alps>
        ```
    *   **Schema Reference (JSON):** `"$schema": "https://alps-io.github.io/schemas/alps.json"`
        ```json
        {
            "$schema": "https://alps-io.github.io/schemas/alps.json",
            "alps": {
                "descriptor": []
            }
        }
        ```

    **2.1.2. Step 2: Register Meanings as IDs (Ontology - Semantic Descriptors)**
    *   **Concept:** Define application-specific terms as `id`s.
    *   **Example (XML):** Adding `dateCreated`.
        ```xml
        <descriptor id="dateCreated"/>
        ```
    *   **Example (JSON):**
        ```json
        {"id": "dateCreated"}
        ```

    **2.1.3. Step 3: Describe Terms**
    *   **Mechanism:** Use `title` (concise heading) and `doc` (detailed explanation).
    *   **Concept:** This `id` bound to a meaning is a **semantic descriptor**. Defining meanings and concepts is **ontology**.
    *   **Example (XML):**
        ```xml
        <descriptor id="dateCreated" title="Creation Date">
           <doc format="text">Represents the article creation date in ISO8601 format</doc>
        </descriptor>
        ```
    *   **Example (JSON):**
        ```json
        {"id": "dateCreated", "title": "Creation Date", "doc": {"format": "text", "value": "Represents the article creation date in ISO8601 format"}}
        ```
    *   **Vocabulary Role:** ALPS serves as a dictionary, promoting consistent terminology.

    **2.1.4. Step 4: Information Contains Information (Taxonomy)**
    *   **Concept:** Semantic descriptors can contain other semantic descriptors, representing information hierarchy. This is **taxonomy**.
    *   **Mechanism:** Nested `descriptor` elements or `href` for inline linking (referencing other descriptors).
    *   **Example (JSON):** `BlogPosting` contains `id`, `dateCreated`, `articleBody`.
        ```json
        {
            "descriptor": [
                {"id": "id", "title": "ID"},
                {"id": "articleBody", "title": "Content"},
                {"id": "dateCreated", "title": "Creation Date"},
                {"id": "BlogPosting", "title": "Article", "descriptor": [
                    {"href": "#id"},
                    {"href": "#dateCreated"},
                    {"href": "#articleBody"}
                ]},
                {"id": "Blog", "title": "Article List", "descriptor": [
                    {"href": "#BlogPosting"}
                ]}
            ]
        }
        ```

    **2.1.5. Step 5: Viewing and Manipulating Information (Choreography - Operations)**
    *   **Operation Types:**
        *   **`safe`**: View related information. No resource state change. Changes *application state* (user's current view/URL). (Corresponds to HTTP GET).
        *   **`idempotent`**: Changes resource state. Repeated execution yields the same result. (Corresponds to HTTP PUT, DELETE).
        *   **`unsafe`**: Changes resource state. Lacks idempotency; repeated execution yields different results. (Corresponds to HTTP POST).
    *   **Defining Links/Operations:**
        *   `type` attribute specifies operation type.
        *   `rt` (return type) attribute specifies the destination state/resource (target of the transition).
    *   **Example (JSON):** Link to view `Blog` (`goBlog`).
        ```json
        {"type": "safe", "id": "goBlog", "rt": "#Blog", "title": "View Blog Post List"}
        ```
    *   **Example (JSON):** Add `goBlog` transition to `BlogPosting`.
        ```json
        {"id": "BlogPosting", "title": "Article", "descriptor": [
{"id": "BlogPosting", "title": "Article", "descriptor": [
    {"href": "#goBlog"}
]}
        ```json
        {"id": "goBlogPosting", "type": "safe", "rt": "#BlogPosting", "title": "View Article", "descriptor": [
           {"href": "#id"}
        ]}
        ```
    *   **Complete Example with Ontology, Taxonomy, Choreography (JSON):**
        ```json
        {
            "$schema": "https://alps-io.github.io/schemas/alps.json",
            "alps": {
                "descriptor": [
                    {"id": "id", "title": "ID"},
                    {"id": "articleBody", "title": "Content"},
                    {"id": "dateCreated", "title": "Creation Date"},
                    {"id": "BlogPosting", "title": "Article", "descriptor": [
                        {"href": "#id"}, {"href": "#dateCreated"}, {"href": "#articleBody"}, {"href": "#goBlog"}
                    ]},
                    {"id": "Blog", "title": "Article List", "descriptor": [
                        {"href": "#BlogPosting"}, {"href": "#goBlogPosting"}
                    ]},
                    {"id": "goBlog", "type": "safe", "rt": "#Blog", "title": "View Article List"},
                    {"id": "goBlogPosting", "type": "safe", "rt": "#BlogPosting", "title": "View Article", "descriptor": [
                       {"href": "#id"}
                    ]}
                ]
            }
        }
        ```

**Section 2.2: Advanced ALPS Tutorial: Designing REST Applications**
*   **Essence of REST Applications:** State transition systems.
    *   Client is always in a "current state" (application state, represented by URL).
    *   Client can transition to other "possible states."
    *   "How" to transition is defined (transition method, network affordances).
*   **Two Key States in REST:**
    *   **Application State:** Client-side location/context (URL).
    *   **Resource State:** Server-side data state.
*   **State Transition Flow in REST:**
    1.  Client recognizes current state and available information/affordances.
    2.  Client chooses a transition (link/action).
    3.  Client executes transition, moving to a new application state, potentially altering resource state.
*   **ALPS for REST (using IA Framework):**
    1.  **Ontology:** Define basic terms (e.g., `dateCreated`, `articleBody`).
        *   *Naming Convention:* CamelCase (e.g., `dateCreated`). Semantic terms preferred.
        *   *Example (JSON):*
            ```json
            {"id": "dateCreated", "title": "Creation Date", "doc": {"format": "text", "value": "Represents the post creation date in ISO8601 format"}},
            {"id": "articleBody", "title": "Article Body", "doc": {"format": "text", "value": "The body of the blog post"}}
            ```
    2.  **Taxonomy (1): Define Information Structure (Resource Representations).**
        *   Combine ontological terms into larger concepts (e.g., `BlogPosting`).
        *   Use `href` for referencing.
        *   *Example (JSON):*
            ```json
            {"id": "BlogPosting", "title": "Blog Post", "descriptor": [
               {"href": "#dateCreated"},
               {"href": "#articleBody"}
            ]}
            ```
    3.  **Choreography: Define State Transitions (Operations mapping to HTTP Methods).**
        *   Operation types: `safe` (GET), `unsafe` (POST), `idempotent` (PUT/DELETE).
        *   *Naming Convention (Prefixes):* `go` for `safe`; `do` for `unsafe`/`idempotent`.
        *   `rt` attribute: Specifies destination state.
        *   Nested `descriptor`s: Specify information/parameters needed for the transition.
        *   *Example: View Blog Post (`goBlogPosting`, `safe` operation)*
            ```json
            {"id": "goBlogPosting", "type": "safe", "rt": "#BlogPosting", "title": "View Blog Post", "descriptor": [
               {"href": "#dateCreated"} // Example: uses dateCreated for lookup, often it's an 'id'
            ]}
            ```
        *   *Example: Create Blog Post (`doCreateBlogPosting`, `unsafe` operation)*
            ```json
            {"id": "doCreateBlogPosting", "type": "unsafe", "rt": "#BlogPosting", "title": "Create Blog Post", "descriptor": [
                {"href": "#articleBody"}
            ]}
            ```
        *   *Example: Update Blog Post (`doUpdateBlogPosting`, `idempotent` operation)*
            ```json
            {"id": "doUpdateBlogPosting", "type": "idempotent", "rt": "#BlogPosting", "title": "Update Blog Post", "descriptor": [
               {"href": "#articleBody"}
            ]}
            ```
    4.  **Taxonomy (2): Integrate States and Transitions (Application State Definitions).**
        *   Define overall application states that group resource representations and available transitions.
        *   *Example (JSON):* `Blog` application state.
            ```json
            {"id": "Blog", "title": "Blog Application State", "descriptor": [
               {"href": "#BlogPosting"}, // Represents the data/resource structure
               {"href": "#goBlogPosting"}, // Available action
               {"href": "#doCreateBlogPosting"}, // Available action
               {"href": "#doUpdateBlogPosting"}  // Available action
            ]}
            ```
*   **Conclusion:** ALPS provides a methodology for clear, consistent API design by modeling ontology, taxonomy, and choreography.

**Part 3: ALPS Reference**

**Section 3.1: Document Structure Overview**
1.  **Root Element (`alps`):** Contains version information and all definitions.
2.  **Descriptor Element (`descriptor`):** Central element defining semantics of application features, information, or operations.
    *   *Types:* `semantic` (default), `safe`, `idempotent`, `unsafe`.
    *   Can be nested or contain `link` elements.
3.  **Supplementary Elements:** `doc`, `link`, `title`, `ext`.

**Section 3.2: Representation Formats**
*   **XML & JSON:** Functionally equivalent.
*   **Important Note:** JSON does not support comments, unlike XML. When using JSON format, avoid attempting to include comments in ALPS documents.
*   **Example XML Structure:**
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <alps version="1.0">
        <title>Blog API Profile</title>
        <doc>API profile for a blog system</doc>
        <descriptor id="titleSemantic" title="Title" doc="Article title."/>
        <descriptor id="blogPostResource">
            <doc>Blog post resource</doc>
            <descriptor href="#titleSemantic"/>
            <link rel="related" href="http://example.org/docs/blog.html"/>
        </descriptor>
    </alps>
    ```
*   **Example JSON Structure:**
    ```json
    {
        "alps": {
            "version": "1.0",
            "title": "Blog API Profile",
            "doc": {"value": "API profile for a blog system"},
            "descriptor": [
                {"id": "titleSemantic", "title": "Title", "doc": {"value": "Article title."}},
                {"id": "blogPostResource", "doc": {"value": "Blog post resource"},
                 "descriptor": [{"href": "#titleSemantic"}],
                 "link": [{"rel": "related", "href": "http://example.org/docs/blog.html"}]
                }
            ]
        }
    }
    ```

**Section 3.3: Elements and Attributes in Detail**

    **3.3.1. `alps` Element**
    *   **Description:** Root element.
    *   **Attributes:**
        *   `version` (String, Required): ALPS document version (e.g., "1.0").

    **3.3.2. `descriptor` Element**
    *   **Description:** Defines semantics of application features, information, or operations.
    *   **Child Elements:** `descriptor`, `doc`, `link`, `ext`.
    *   **Key Constraint:** MUST have either `id` or `href`, but not both.
    *   **Attributes:**
*   `id` (String, Conditional): Unique identifier within the document (mutually exclusive with `href`). Must use URL-safe characters (RFC3986).
        *   `href` (String, Conditional): URI reference to another descriptor. Internal (e.g., `#someId`) or external (e.g., `profile.xml#someId`). (Mutually exclusive with `id`).
        *   `type` (Enum, Optional, Default: `semantic`): Descriptor type.
            *   `semantic`: Represents information, terminology, or application state.
            *   `safe`: Read operation (no resource state change).
            *   `idempotent`: Operation with idempotent effect on resource state.
            *   `unsafe`: Operation with non-idempotent effect on resource state.
        *   `rt` (String, Optional): Return Type. Fragment identifier (e.g., `#BlogPostState`) pointing to the target `semantic` descriptor (application state) after a transition. Used when `type` is `safe`, `idempotent`, or `unsafe`.
        *   `rel` (String, Optional): Relationship of the descriptor. Uses IANA Link Relations (e.g., `item`, `collection`) or custom URI.
        *   `title` (String, Optional): Human-readable display name/label.
        *   `tag` (String, Optional): Space-separated classification tags for grouping/filtering.
        *   `name` (String, Optional): Name used in actual representations; allows multiple descriptors to share a common presentation name if `id`s must be unique.
        *   `def` (String, Optional): URI indicating an external resource defining the descriptor's semantics (e.g., Schema.org URI).

    **3.3.3. `doc` Element**
    *   **Description:** Provides detailed descriptions or supplementary information.
    *   **Attributes:**
        *   `href` (String, Optional): URL of an external document.
        *   `format` (String, Optional): Format of the documentation content (e.g., `text`, `html`, `markdown`, `asciidoc`).
            *   `text`: MUST support.
            *   `html`: SHOULD support.
            *   `markdown` (RFC7763), `asciidoc`: MAY support.
        *   `contentType` (String, Optional): MIME type of the content. (Takes precedence over `format` if both exist. If neither, `text/plain` is assumed).
        *   `tag` (String, Optional): Space-separated classification tags.
        *   `value` (String, Optional): Inline documentation text. (Mutually exclusive with `href`).

    **3.3.4. `link` Element**
    *   **Description:** Defines references to related external documents or resources. Child of `alps` or `descriptor`.
    *   **Attributes:**
        *   `href` (String, Required): Target URL of the linked resource.
        *   `rel` (String, Required): Relationship type (e.g., `self`, `profile`, `help`, `related`, IANA link relations).
        *   `title` (String, Optional): Human-readable title for the link.
        *   `tag` (String, Optional): Space-separated classification tags.

    **3.3.5. `ext` Element**
    *   **Description:** Provides extension information not covered by the standard ALPS specification.
    *   **Attributes:**
        *   `id` (String, Required): Unique identifier for the extension.
        *   `href` (String, Recommended): URL explaining the extension's semantics.
        *   `value` (String, Optional): Value of the extension.
        *   `tag` (String, Optional): Space-separated classification tags.

**Section 3.4: Validation Rules**
1.  A `descriptor` element MUST have exactly one of `id` or `href`.
2.  `id` attribute values MUST be unique within an ALPS document.
3.  `href` attribute values that are fragment identifiers MUST resolve to an existing `id` within the document (or be a resolvable URL if external).
4.  `rt` attribute values MUST refer to the `id` of an existing `semantic` descriptor within the document.
5.  `type` attribute value MUST be one of: `semantic`, `safe`, `idempotent`, `unsafe`.
6.  Recommended `id` prefixes for operation descriptors: `go` for `safe`; `do` for `unsafe`/`idempotent`.

**Section 3.5: Hierarchical Structure Example**
*   **Concept:** Nesting `descriptor` elements to represent parent-child relationships.
*   **Example (JSON):**
    ```json
    { "alps": { "version": "1.0", "descriptor": [
      { "id": "userResource", "type": "semantic", "doc": {"value": "User information"},
        "descriptor": [
          {"id": "userNameSemantic", "type": "semantic"},
          {"id": "userEmailSemantic", "type": "semantic"}
        ],
        "link": [{"rel": "help", "href": "http://example.org/help/user.html"}]
      }
    ]}}
    ```

**Part 4: ALPS Best Practices**

**Section 4.1: Naming Conventions**
*   **Application State Descriptors (`type="semantic"` representing states):**
    *   `id`: `UpperCamelCase` (e.g., `BlogPosting`, `UserProfile`).
*   **Operation/Transition Descriptors (`type="safe"`, `idempotent"`, `unsafe"`):**
    *   `id` prefix for `safe`: `go` (e.g., `goHome`, `goUserProfile`).
    *   `id` prefix for `unsafe`/`idempotent`: `do` (e.g., `doCreateUser`, `doUpdateProfile`).
    *   Convention: `rt` value (target state `id`) often forms part of the operation `id` (e.g., `id="goUserProfile"` with `rt="#UserProfile"`).
*   **Element/Parameter Descriptors (`type="semantic"` for data fields):**
    *   `id`: `lowerCamelCase` (e.g., `articleBody`, `dateCreated`, `firstName`).

**Section 4.2: Recommended ALPS File Structure**
*   **Order of Descriptor Groups:**
    1.  **Ontology:** Semantic descriptors defining basic elements, meanings (often with `def`, `doc`).
    2.  **Taxonomy:** Semantic descriptors defining application states or complex data structures (grouping ontology elements and choreography affordances).
    3.  **Choreography:** Semantic descriptors defining state transitions (operations).
*   **Example (JSON outline):**
    ```json
    {"alps": {"descriptor": [
        /* Ontology Block */
        {"id": "name", "type": "semantic", "def": "http://schema.org/name"},
        {"id": "age", "type": "semantic", "def": "http://schema.org/Integer"},
        /* Taxonomy Block */
        {"id": "PersonState", "type": "semantic", "descriptor": [
            {"href": "#name"}, {"href": "#age"}, {"href": "#goViewAddress"} /* Choreography ref */
        ]},
        /* Choreography Block */
        {"id": "goViewAddress", "type": "safe", "rt": "#AddressState"}
    ]}}
    ```

**Section 4.3: Representing Hierarchical Meaning Outside ALPS**
*   **ALPS:** Hierarchy expressed by nested `descriptor`s or `href` paths.
*   **Flat Hierarchies (e.g., HTML form fields):** Use context-specific naming conventions.
    *   *Example:* ALPS `Product/name` and `Person/name`.
    *   *HTML:* `<input name="productName">`, `<input name="personName">`.

**Section 4.4: Adding Schema References**
*   **Purpose:** Enable validation and editor support.
*   **JSON:**
    ```json
    {
      "$schema": "https://alps-io.github.io/schemas/alps.json",
      "alps": { /* ... */ }
    }
    ```
*   **XML:**
    ```xml
    <alps version="1.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd">
      {/* ... */}
    </alps>
    ```

**Section 4.5: Implementation Examples**

    **4.5.1. Semantic Element Definitions & Reuse**
    *   **Basic Elements (Ontology):**
        ```json
        {"id": "title", "title": "Title", "doc": {"value": "Max 100 chars."}},
        {"id": "content", "title": "Content", "doc": {"value": "Markdown supported."}}
        ```
    *   **Reusing Elements in Complex Types (Taxonomy):**
        ```json
        {"id": "blogPost", "doc": {"value": "User-created article."}, "descriptor": [
            {"href": "#title"}, {"href": "#content"}, {"href": "#publishedAt"}
        ]},
        {"id": "pagePost", "doc": {"value": "Static page."}, "descriptor": [
            {"href": "#title"}, {"href": "#content"}
        ]}
        ```

    **4.5.2. Operation Definitions (Choreography)**
    *   **Example (JSON):**
        ```json
        {"id": "goBlog", "type": "safe", "rt": "#BlogState", "doc": {"value": "Display blog homepage."}},
        {"id": "doCreateBlogPost", "type": "unsafe", "rt": "#BlogPostState", "doc": {"value": "Create new article."}, "descriptor": [
            {"href": "#title"}, {"href": "#content"}
        ]},
        {"id": "doPublishBlogPost", "type": "idempotent", "rt": "#BlogPostState", "doc": {"value": "Publish article."}, "descriptor": [
            {"href": "#id"} /* Assuming 'id' is the identifier of the post to publish */
        ]}
        ```

**Part 5: Leveraging Shared Vocabularies**

**Section 5.1: IANA Link Relations**
*   **Purpose:** Standardized identifiers for the relationship between two resources (or a resource and a state transition).
*   **Usage in ALPS:**
    *   `rel` attribute of `link` elements.
    *   Inform the naming or `doc` of transition descriptors (choreography).
*   **Key Relation Categories & Examples (for ALPS context):**
    *   **State Transitions:** `edit`, `edit-form`, `create-form`, `collection` (transition to collection view), `item` (transition to item view).
    *   **Ordered Transitions:** `first`, `last`, `next`, `prev` (for paginated or sequential states).
    *   **Semantic Description:** `describedby` (ref to detailed description), `type` (indicates abstract type).
    *   **Document Structure (if ALPS describes parts of a larger document):** `section`, `subsection`, `contents`.
    *   **Metadata:** `author`, `license`.
    *   **Version Control:** `latest-version`, `predecessor-version`.
    *   **General:** `help`, `status`, `alternate`.
*   **Reference:** IANA Link Relations Registry (`https://www.iana.org/assignments/link-relations/link-relations.xhtml`).

**Section 5.2: Schema.org**
*   **Purpose:** Widely adopted vocabulary for structured data, useful for grounding ALPS semantic descriptors.
*   **Usage in ALPS:** `def` attribute of `descriptor` elements points to a Schema.org URI.
    *   *Example:* `<descriptor id="givenName" def="https://schema.org/givenName" />`
*   **Schema.org ALPS Imports:** Pre-defined ALPS files for Schema.org terms are available (e.g., `https://alps-io.github.io/imports/schema.org/`). These can be referenced via `href` in your ALPS descriptors.
    *   *Example:* `<descriptor href="https://alps-io.github.io/imports/schema.org/properties/givenName.json" />`
*   **Narrowing Semantics:** Create ALPS descriptors that refine or specify a broader Schema.org term.
    *   *Example:* `<descriptor id="bankAccountId" href="https://alps-io.github.io/imports/schema.org/properties/accountId.json" title="Bank Account ID" />` (narrows general `accountId`).

**Part 6: Prompts for ALPS Profile Creation & Conversion**
*(This section provides structured prompts to guide the generation or transformation of ALPS profiles, suitable for AI or human use.)*

**Section 6.1: ALPS Profile Creation Prompt Template**

*   **Input Request:** "Create an ALPS profile based on the following requirements. The profile must represent a complete and consistent application state design."
*   **Required Parameters for Request:**
    *   `Output Format`: [JSON | XML]
    *   `Language for titles/docs`: [e.g., English, Japanese]
    *   `User Story / Requirements Content`: [Detailed description of the application, user flows, data entities, and operations to be modeled.]

*   **Core Design Guidelines (to be included in prompt or as system instructions):**
    1.  **State Connectivity:** All states must be interconnected (no isolated states). Ensure logical entry/exit transitions for each state (except initial/final states).
    2.  **Semantic Descriptor Consistency:** Use consistent `id` naming for identical concepts. Use `def` attribute ONLY if a direct Schema.org (or other standard vocabulary) definition exists. Provide clear `title` and `doc` for custom concepts.
    3.  **User Flow Completeness:** Model complete state transition paths for all key user stories and CRUD operations.
    4.  **Transition Completeness:** Define success paths for operations. Ensure critical business processes have robust transitions. Consider critical failure recovery paths if necessary.
    5.  **Element Grouping (Tagging):** Use the `tag` attribute to group related processes, user journeys, or functional areas (e.g., "user-management", "payment-process"). Apply consistent tags to states and transitions within the same functional domain.

*   **Format-Specific Guidelines (to be included in prompt):**

    *   **JSON Format:**
        1.  Each `descriptor` generally on a single line.
        2.  Indent and line-break `descriptor`s ONLY if they contain nested `descriptor`s.
        3.  Nested `descriptor`s (children) should primarily use `href` to reference their constituent elements/transitions (which are defined elsewhere at the top level of the `alps.descriptor` array).
        *   *Example Snippet:*
            ```json
            {"$schema": "...", "alps": {"version": "1.0", "descriptor": [
              {"id": "name", "title": "Name", "def": "https://schema.org/name"},
-             {"id": "User", "title": "User Profile", "descriptor": [ {"href": "#name"}, /* ... */ ]},
+             {"id": "User", "title": "User Profile", "descriptor": [ {"href": "#name"} ]},
              {"id": "goUser", "type": "safe", "rt": "#User"}
            ]}}
            ```

    *   **XML Format:**
        1.  Use indentation to indicate hierarchy.
        2.  Each element generally on a new line for readability if complex.
        *   *Example Snippet:*
            ```xml
            <alps version="1.0" ...>
              <descriptor id="name" title="Name" def="https://schema.org/name"/>
              <descriptor id="User" title="User Profile">
                <descriptor href="#name"/>
                {/* ... */}
              </descriptor>
              <descriptor id="goUser" type="safe" rt="#User"/>
            </alps>
            ```

*   **Structuring Semantic Descriptors (File Organization):**
    1.  **Block 1: Ontology (Semantic Definitions):** Basic elements (`lowerCamelCase` `id`s). `def` with full URI if Schema.org. `title` mandatory. `doc` if needed. Each defined element MUST be referenced by at least one Taxonomy state.
    2.  **Block 2: Taxonomy (Containment Relationships / Application States):** State descriptors (`UpperCamelCase` `id`s). Use `href` to reference ontological elements and choreographical transitions. Each application state includes elements displayed/used and actions performable. Each taxonomy state MUST connect to others via transitions.
    3.  **Block 3: Choreography (State Transitions):** Operation descriptors. Define `type`, `rt`. Use `href` for necessary data items. Each operation MUST be referenced by at least one Taxonomy state.

*   **General Output Requirements (for the generated ALPS profile):**
    *   `title` attribute for every descriptor (concise).
    *   `doc` attribute for detailed explanations where necessary.
    *   `def` attribute (Schema.org URLs) only if a direct corresponding definition exists.
    *   Appropriate `type` attribute (`safe`, `unsafe`, `idempotent`) for all transitions.
    *   Reusable descriptors for common patterns.
    *   Consistent `id`s and naming for identical concepts.
    *   `tag` attribute for grouping related elements (business domains, functional areas).

**Section 6.2: ALPS Conversion Prompt Templates**

    **6.2.1. To OpenAPI 3.1 Specification**
    *   **Task:** Convert the provided ALPS profile into a comprehensive OpenAPI 3.1 specification (YAML format).
    *   **Key Instructions:**
        1.  **State to Endpoint/Path Mapping:** Map ALPS `semantic` states (Taxonomy) to OpenAPI Paths. Use ALPS `tag` attributes to group Operations in OpenAPI. Apply REST principles (plural nouns for collections).
        2.  **Transition to Operation Mapping:** Convert ALPS transitions (Choreography) to OpenAPI Operations: `safe` -> GET; `unsafe` -> POST; `idempotent` -> PUT/PATCH/DELETE. Use appropriate HTTP status codes.
        3.  **Schema Definitions:** Build OpenAPI Schemas from ALPS semantic descriptors (Ontology and data elements within Taxonomy states). Include all referenced properties. Use `def` attributes for Schema.org mappings. Define request and response schemas.
        4.  **Documentation:** Use ALPS `title` for OpenAPI `summary`. Use ALPS `doc` for `description`. Include examples.
        5.  **Design Consistency:** Implement query parameters (for filtering/sorting from ALPS descriptors if specified), path parameters (for resource identifiers like `id`).

    **6.2.2. To JSON Schema**
    *   **Task:** Convert the provided ALPS profile into comprehensive JSON Schemas.
    *   **Key Instructions:**
        1.  **Semantic Descriptor to Schema Mapping:** Create JSON Schema type definitions (in `$defs`) for each ALPS `semantic` descriptor (Ontology, Taxonomy data structures). Use `$ref` for reusability.
        2.  **Type & Format Selection:** Choose appropriate JSON Schema `type`s (string, number, object, array) and `format`s (date-time, email) based on ALPS descriptor semantics and `doc`.
        3.  **Validation Rules:** Infer constraints (minLength, maxLength, pattern, required, enum) from ALPS `doc` or domain knowledge associated with descriptors.
        4.  **Documentation:** Use ALPS `title` for JSON Schema `title`, ALPS `doc` for `description`.

    **6.2.3. To GraphQL Schema (SDL)**
    *   **Task:** Convert the provided ALPS profile into a GraphQL schema (SDL format), including example operations.
    *   **Key Instructions:**
        1.  **Type Definitions:** Create GraphQL Types for ALPS `semantic` descriptors (Ontology, Taxonomy data structures). Define Scalars.
        2.  **Query Operations:** Derive GraphQL Queries from ALPS `safe` transitions.
        3.  **Mutation Operations:** Derive GraphQL Mutations from ALPS `unsafe` and `idempotent` transitions. Define Input types.
        4.  **Schema Organization:** Use ALPS `tag` attributes to group related operations if applicable.

    **6.2.4. To SQL Database Schema (DDL)**
    *   **Task:** Convert the provided ALPS profile into SQL DDL statements for schema creation.
    *   **Key Instructions:**
        1.  **Table Structure:** Create SQL Tables for main ALPS `semantic` descriptors representing entities (Taxonomy states holding data). Define columns based on ontological elements.
        2.  **Relationship Modeling:** Infer relationships (one-to-many, many-to-many) from nested ALPS structures or `rel` attributes. Implement foreign keys.
        3.  **Data Types & Constraints:** Select appropriate SQL column types and define constraints based on ALPS `doc` or implied semantics.

    **6.2.5. To TypeScript Type Definitions**
    *   **Task:** Convert the provided ALPS profile into TypeScript interfaces and types.
    *   **Key Instructions:**
        1.  **Core Type Definitions:** Create TypeScript `interface`s or `type` aliases for ALPS `semantic` descriptors (Ontology, Taxonomy data structures).
        2.  **Property Types:** Use appropriate TypeScript types (string, number, boolean, Date, arrays, nested types).
        3.  **Documentation:** Convert ALPS `title` and `doc` to JSDoc comments.
        4.  **API Integration (Optional):** Define request/response types for operations derived from ALPS transitions if modeling an API client.

**Part 6: Frequently Asked Questions about ALPS**

**Q. What is the difference between ALPS and IDL such as OpenAPI?**
A. ALPS deals with REST abstractions that are higher than HTTP. Therefore, it can be used as a modeling and design language for OpenAPI implementations. While OpenAPI focuses on technical API details (endpoints, HTTP methods, request/response structures), ALPS focuses on business domain semantics and structure using Information Architecture concepts.

**Q. Who can use ALPS?**
A. It can be used by anyone involved in site creation (engineers, designers, product owners). Anyone who can understand XML and JSON and can do simple HTML coding can write ALPS.

**Q. How do you use ALPS?**
A. It is used to design a site by organizing information into the minimum necessary elements, and to design web and API services. The design can be expressed in formats such as JSON and XML, and documents such as transition diagrams and vocabulary lists can be generated. Each producer can know the exact words, meanings, and structures of information based on the information design.

**Q. Can it be used for APIs without links?**
A. Yes. It cannot represent a transition diagram, but it can generate a vocabulary and documentation of the nature of the information.

**Part 7: Integration with Existing Media Types**

ALPS can be used in combination with various existing media types. Below, we explain how to integrate with major media types.

**Integration with HTML**
In HTML, ALPS descriptors are primarily represented using the `class` attribute:

```html
<div class="blog-post">
  <h1 class="title">Article Title</h1>
  <div class="content">Content...</div>
  <form class="add-comment" method="post">
    <input name="comment-text" class="comment-text">
    <button type="submit">Add Comment</button>
  </form>
</div>
```

Corresponding ALPS profile:
```xml
<alps version="1.0">
  <descriptor id="blog-post" type="semantic">
    <descriptor id="title" type="semantic"/>
    <descriptor id="content" type="semantic"/>
    <descriptor id="add-comment" type="unsafe">
      <descriptor id="comment-text" type="semantic"/>
    </descriptor>
  </descriptor>
</alps>
```

**Integration with HAL (Hypertext Application Language)**
In HAL, state transitions are expressed as link relations and semantic descriptors as properties:

```json
{
  "_links": {
    "self": {"href": "/posts/1"},
    "add-comment": {"href": "/posts/1/comments"}
  },
  "title": "Article Title",
  "content": "Content...",
  "_embedded": {
    "comments": [
      {
        "_links": {
          "self": {"href": "/comments/1"}
        },
        "text": "Comment content..."
      }
    ]
  }
}
```

**Referencing ALPS Documents**

This section describes how to reference ALPS profiles when applying them.

1. **Referencing in HTML**
   ```html
   <link rel="profile" href="http://example.com/alps/blog" />
   ```

2. **Referencing in HTTP Link Header**
   ```http
   Link: <http://example.com/alps/blog>; rel="profile"
   ```

3. **Referencing in Media Type Parameter**
   ```http
   Content-Type: application/json; profile="http://example.com/alps/blog"
   ```

**Appendix A: Complete ALPS Example (Bookstore)**
*(This section would contain the full XML example of the Bookstore ALPS profile from the original document, slightly formatted for consistency if needed, but content preserved.)*
```xml
<?xml version="1.0" encoding="UTF-8"?>
<alps version="1.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd">
    <title>ALPS Book Store</title>
    <doc format="text">ALPS profile for managing an online bookstore catalog and defining the user purchase flow. This profile provides semantic definitions for both RESTful APIs and UI.</doc>
    <link href="https://github.com/example/online-bookstore-api/issues" rel="issue"/>

    <!-- Ontology Block -->
    <descriptor id="id" def="https://schema.org/identifier" title="Identifier" tag="core">
        <doc format="text">Unique identifier for each resource. UUID or auto-generated integer.</doc>
    </descriptor>
    <descriptor id="title" def="https://schema.org/name" title="Title" tag="catalog">
        <doc format="text">Title of book or category name. String with a maximum of 200 characters.</doc>
    </descriptor>
    <descriptor id="author" def="https://schema.org/author" title="Author" tag="catalog">
        <doc format="text">Name of the book's author. For multiple authors, names are comma-separated.</doc>
    </descriptor>
    <descriptor id="isbn" def="https://schema.org/isbn" title="ISBN" tag="catalog">
        <doc format="text">International Standard Book Number. Formatted as ISBN-13 with hyphens.</doc>
    </descriptor>
    <descriptor id="price" def="https://schema.org/price" title="Price" tag="commerce">
        <doc format="text">Sales price of the book. Pre-tax amount in JPY currency.</doc>
    </descriptor>
    <descriptor id="categoryName" def="https://schema.org/category" title="Category Name" tag="catalog">
        <doc format="text">Genre or category name of the book.</doc>
    </descriptor>
    <descriptor id="quantity" def="https://schema.org/quantity" title="Quantity" tag="commerce"> <!-- Changed from quantityValue to quantity for better Schema.org alignment -->
        <doc format="text">Quantity of books in the cart. Integer value greater than or equal to 1.</doc>
    </descriptor>
    <descriptor id="totalAmount" def="https://schema.org/totalPrice" title="Total Amount" tag="commerce">
        <doc format="text">Total amount for an order or cart contents. Displayed with tax included.</doc>
    </descriptor>
    <descriptor id="userName" def="https://schema.org/name" title="User Name" tag="customer">
        <doc format="text">Name of the customer. First and last name separated by a space.</doc>
    </descriptor>
    <descriptor id="userEmail" def="https://schema.org/email" title="Email Address" tag="customer">
        <doc format="text">Customer's contact email address. Used for sending order confirmation emails.</doc>
    </descriptor>
    <descriptor id="shippingAddress" def="https://schema.org/address" title="Shipping Address" tag="shipping">
        <doc format="text">Delivery address for products. Includes postal code, prefecture, city, street address, and building name.</doc>
    </descriptor>
    <descriptor id="paymentMethod" def="https://schema.org/paymentMethod" title="Payment Method" tag="payment">
        <doc format="text">Method of payment for the order. Options include credit card, cash on delivery, bank transfer, etc.</doc>
    </descriptor>
    <descriptor id="searchQuery" title="Search Query" tag="catalog-search"> <!-- More specific tag -->
        <doc format="text">Keywords or conditions used for book searches. Can search by title, author name, ISBN, etc.</doc>
    </descriptor>

    <!-- Taxonomy Block (Application States & Resource Structures) -->
    <descriptor id="HomeState" title="Home Screen State" tag="navigation ui-state">
        <doc format="text">Starting point of the application. Displays site-wide navigation and promotional information.</doc>
        <descriptor href="#goToCatalog"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="BookResource" def="https://schema.org/Book" title="Book Resource Structure" tag="catalog resource-structure">
        <doc format="text">Structure representing individual book information.</doc>
        <descriptor href="#id"/>
        <descriptor href="#title"/>
        <descriptor href="#author"/>
        <descriptor href="#isbn"/>
        <descriptor href="#price"/>
        <descriptor href="#categoryName"/>
    </descriptor>

    <descriptor id="CategoryResource" def="https://schema.org/Thing" title="Category Resource Structure" tag="catalog resource-structure"> <!-- schema.org/Category is a type, Thing or Intangible might be better for a generic category resource -->
        <doc format="text">Structure representing a book category.</doc>
        <descriptor href="#id"/>
        <descriptor href="#title"/> <!-- Assuming category title -->
    </descriptor>

    <descriptor id="CatalogState" def="https://schema.org/CollectionPage" title="Book Catalog State" tag="catalog ui-state">
        <doc format="text">State for displaying all books. Provides category filtering, keyword search, and sorting functions.</doc>
        <descriptor href="#BookResource" rel="item"/> <!-- Multiple book resources -->
        <descriptor href="#CategoryResource" rel="item"/> <!-- List of categories for filtering -->
        <descriptor href="#goSearchBooks"/>
        <descriptor href="#goToBookDetails"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="BookDetailsState" title="Book Details State" tag="catalog ui-state">
        <doc format="text">State for displaying individual book information. Shows detailed information, reviews, and related books.</doc>
        <descriptor href="#BookResource"/> <!-- The specific book resource -->
        <descriptor href="#doAddToCart"/>
        <descriptor href="#goToCatalog"/>
    </descriptor>

    <descriptor id="CartItemResource" title="Cart Item Resource Structure" tag="cart resource-structure">
        <doc format="text">Structure representing an item in the shopping cart.</doc>
        <descriptor href="#BookResource"/> <!-- The book details -->
        <descriptor href="#quantity"/>
    </descriptor>

    <descriptor id="ShoppingCartState" def="https://schema.org/Order" title="Shopping Cart State" tag="cart ui-state"> <!-- Schema.org/Order is closer to a cart than ShoppingCart which is less defined -->
        <doc format="text">State for the shopping cart. Allows quantity changes, deletion, and total amount confirmation.</doc>
        <descriptor href="#CartItemResource" rel="item"/> <!-- Multiple cart items -->
        <descriptor href="#totalAmount"/>
        <descriptor href="#doUpdateQuantity"/>
        <descriptor href="#doRemoveFromCart"/>
        <descriptor href="#goToCheckout"/>
        <descriptor href="#goToCatalog"/>
    </descriptor>

    <descriptor id="CheckoutState" title="Checkout State" tag="checkout ui-state">
        <doc format="text">State for the purchase procedure. Input user information, delivery destination.</doc>
        <descriptor href="#userName"/>
        <descriptor href="#userEmail"/>
        <descriptor href="#shippingAddress"/>
        <descriptor href="#doSubmitUserInfo"/>      <!-- New Choreography element needed -->
        <descriptor href="#doSubmitShippingInfo"/>  <!-- New Choreography element needed -->
        <descriptor href="#goToPayment"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="PaymentState" title="Payment State" tag="payment ui-state">
        <doc format="text">State for entering payment information and confirming the order.</doc>
        <descriptor href="#paymentMethod"/>
        <descriptor href="#totalAmount"/>
        <descriptor href="#doSubmitPaymentInfo"/> <!-- New Choreography element needed -->
        <descriptor href="#doPlaceOrder"/>
        <descriptor href="#goToOrderConfirmation"/> <!-- Transition to a new confirmation state -->
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="OrderConfirmationState" title="Order Confirmation State" tag="order ui-state">
        <doc format="text">State displaying details of the placed order (order number, items, total, estimated delivery).</doc>
        <descriptor href="#id"/> <!-- Order ID -->
        <descriptor href="#CartItemResource" rel="item"/>
        <descriptor href="#totalAmount"/>
        <descriptor href="#shippingAddress"/>
        <descriptor href="#paymentMethod"/>
        <descriptor href="#goToHome"/>
    </descriptor>


    <!-- Choreography Block (State Transitions / Operations) -->
    <descriptor id="goToHome" type="safe" rt="#HomeState" title="Go to Home Screen" tag="navigation action">
        <doc format="text">Navigate to the application's home screen.</doc>
    </descriptor>
    <descriptor id="goToCatalog" type="safe" rt="#CatalogState" title="Go to Catalog Screen" tag="navigation catalog action">
        <doc format="text">Navigate to the book catalog list screen.</doc>
    </descriptor>
    <descriptor id="goToBookDetails" type="safe" rt="#BookDetailsState" title="Go to Book Details Screen" tag="navigation catalog action">
        <doc format="text">Navigate to the detailed information screen for the selected book.</doc>
        <descriptor href="#id"/> <!-- Book ID -->
    </descriptor>
    <descriptor id="goToCart" type="safe" rt="#ShoppingCartState" title="Go to Cart Screen" tag="navigation cart action">
        <doc format="text">Navigate to the screen displaying the current shopping cart contents.</doc>
    </descriptor>
    <descriptor id="goToCheckout" type="safe" rt="#CheckoutState" title="Go to Checkout Screen" tag="navigation checkout action">
        <doc format="text">Navigate to confirm cart contents and proceed with purchase.</doc>
    </descriptor>
    <descriptor id="goToPayment" type="safe" rt="#PaymentState" title="Go to Payment Screen" tag="navigation payment action">
        <doc format="text">Navigate to the payment screen to input payment information.</doc>
    </descriptor>
    <descriptor id="goToOrderConfirmation" type="safe" rt="#OrderConfirmationState" title="Go to Order Confirmation Screen" tag="navigation order action">
        <doc format="text">Navigate to the order confirmation screen after placing an order.</doc>
    </descriptor>

    <descriptor id="goSearchBooks" type="safe" rt="#CatalogState" rel="collection" title="Search Books" tag="catalog-search action">
        <doc format="text">Search for books based on the specified search query.</doc>
        <descriptor href="#searchQuery"/>
    </descriptor>

    <descriptor id="doAddToCart" type="unsafe" rt="#ShoppingCartState" title="Add Book to Cart" tag="cart action">
        <doc format="text">Add the specified book to the shopping cart.</doc>
        <descriptor href="#id"/> <!-- Book ID -->
        <descriptor href="#quantity"/>
    </descriptor>
    <descriptor id="doUpdateQuantity" type="idempotent" rt="#ShoppingCartState" title="Update Cart Item Quantity" tag="cart action">
        <doc format="text">Update the quantity of a specific product in the cart.</doc>
        <descriptor href="#id"/> <!-- Cart Item ID or Book ID within cart context -->
        <descriptor href="#quantity"/>
    </descriptor>
    <descriptor id="doRemoveFromCart" type="idempotent" rt="#ShoppingCartState" title="Remove Item from Cart" tag="cart action">
        <doc format="text">Completely remove the specified item from the cart.</doc>
        <descriptor href="#id"/> <!-- Cart Item ID or Book ID within cart context -->
    </descriptor>

    <descriptor id="doSubmitUserInfo" type="unsafe" rt="#CheckoutState" title="Submit User Information" tag="customer checkout action">
        <doc format="text">Submit customer's name and email address for checkout.</doc>
        <descriptor href="#userName"/>
        <descriptor href="#userEmail"/>
    </descriptor>
    <descriptor id="doSubmitShippingInfo" type="unsafe" rt="#CheckoutState" title="Submit Shipping Information" tag="shipping checkout action">
        <doc format="text">Submit product delivery address for checkout.</doc>
        <descriptor href="#shippingAddress"/>
    </descriptor>
    <descriptor id="doSubmitPaymentInfo" type="unsafe" rt="#PaymentState" title="Submit Payment Information" tag="payment action">
        <doc format="text">Select payment method and submit necessary payment details.</doc>
        <descriptor href="#paymentMethod"/>
        <!-- Potentially other payment-specific fields if needed -->
    </descriptor>
    <descriptor id="doPlaceOrder" type="unsafe" rt="#OrderConfirmationState" title="Place Order" tag="order payment action">
        <doc format="text">Confirm order, process payment, and finalize the purchase. Transitions to order confirmation.</doc>
    </descriptor>
</alps>
```

# ‼️ Important: Guidelines for Design Consistency and Completeness ‼️

1. **All states must be connected**:
   - Avoid isolated states (states that cannot be reached or exited)
   - Every state should have at least one incoming and one outgoing transition (except for home/start and final states)
   - Ensure all transitions between states are logical and clear

2. **Consistent use of semantic descriptors**:
   - Use consistent naming conventions for the same concepts
   - Only use the `def` attribute when a corresponding Schema.org definition exists
   - For custom concepts, provide clear titles and use the `doc` attribute for details when needed

3. **Complete user flows**:
   - Provide complete state transition paths for each key user story
   - Ensure CRUD operations (Create, Read, Update, Delete) are fully represented
   - Include all necessary functionality for each user role

4. **State transition completeness**:
   - Clearly define the success path for each operation
   - Ensure transitions between key states to prevent disruption of important business processes
   - Consider alternative flows for critical failure cases when necessary

5. **Grouping related elements**:
   - Group related processes and user journeys using the `tag` attribute
   - Use tags like "user-management", "content-creation", "payment-process", etc.
   - Apply consistent tags to states and transitions belonging to the same functional area
   - This helps identify related functionality when converting to APIs or data models

## ‼️ Important: JSON Format Guidelines ‼️

0. Do not comment on JSON.
1. Write each descriptor on a single line (mandatory).
2. Only indent and line-break descriptors if they contain other descriptors.
3. All nested descriptors must reference their parent with `href`.

```json
{"$schema": "https://alps-io.github.io/schemas/alps.json", "alps": {"version": "1.0", "descriptor": [
{"id": "name", "title": "Name", "def": "https://schema.org/name"},
{"id": "email", "title": "Email", "def": "https://schema.org/email"},
{"id": "User", "title": "User Profile", "descriptor": [
  {"href": "#name"},
  {"href": "#email"}
]},
{"id": "UserList", "title": "User List", "descriptor": [
  {"href": "#User"},
  {"href": "#goUser"},
  {"href": "#doCreateUser"}
]},
{"id": "goUser", "type": "safe", "title": "View User Details", "rt": "#User"},
{"id": "doCreateUser", "type": "unsafe", "title": "Create User", "rt": "#UserList"}
]}}
```

## XML Format Guidelines

- Use indentation to indicate hierarchy.
- Write each element on a single line.

```xml
<alps version="1.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd">
</alps>
```

## Structuring Semantic Descriptors

Organize into the following three blocks. Each descriptor must either reference or contain other descriptors:

1. Semantic Definitions (Ontology)
   - Define basic elements (lowerCamelCase).
   - Always specify `def` as a full URL if there's a Schema.org definition.
   - Add a `title` to all descriptors.
   - Include `doc` only if necessary.
   - Each defined element must be referenced by at least one taxonomy state.

2. Containment Relationships (Taxonomy)
   - Descriptors representing states use UpperCamelCase.
   - Use `href` for referencing elements (direct definition via `id` is not allowed).
   - Each application state includes:
     * Elements displayed/used in the state (defined in the ontology).
     * Actions that can be performed (defined in choreography).
   - Use `doc` for additional details if needed.
   - Each taxonomy must either contain or transition to other taxonomies.

3. State Transitions (Choreography)
   - Define transition actions.
   - Select the appropriate `type` attribute.
   - Specify the transition destination (`rt`).
   - Use `href` to refer to necessary data items.
   - Each operation must be referenced by at least one taxonomy state.

## Output Requirements

- Include a clear title for every descriptor (concise one-line explanation)
- Use the doc attribute for detailed explanations when necessary
- Only reference Schema.org URLs with the def attribute when a corresponding definition exists
- Set appropriate type attributes (safe, unsafe, idempotent) for all state transitions
- Create reusable descriptors for common patterns
- Use consistent IDs and naming conventions for the same concepts
- Utilize the tag attribute to group related elements
- Use consistent tags for business domains or functional areas

## Example ALPS Profile

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alps
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="https://alps-io.github.io/schemas/alps.xsd">
    <title>ALPS Book Store</title>
    <doc>ALPS profile for managing an online bookstore catalog and defining the user purchase flow. This profile provides semantic definitions for both RESTful APIs and UI.</doc>
    <link href="https://github.com/example/online-bookstore-api/issues" rel="issue"/>

    <!-- Ontology  -->
    <descriptor id="id" def="https://schema.org/identifier" title="Identifier" tag="core">
        <doc>Unique identifier for each resource. UUID or auto-generated integer.</doc>
    </descriptor>
    <descriptor id="title" def="https://schema.org/name" title="Title" tag="catalog">
        <doc>Title of book or category name. String with a maximum of 200 characters.</doc>
    </descriptor>
    <descriptor id="author" def="https://schema.org/author" title="Author" tag="catalog">
        <doc>Name of the book's author. For multiple authors, names are comma-separated.</doc>
    </descriptor>
    <descriptor id="isbn" def="https://schema.org/isbn" title="ISBN" tag="catalog">
        <doc>International Standard Book Number. Formatted as ISBN-13 with hyphens.</doc>
    </descriptor>
    <descriptor id="price" def="https://schema.org/price" title="Price" tag="commerce">
        <doc>Sales price of the book. Pre-tax amount in JPY currency.</doc>
    </descriptor>
    <descriptor id="category" def="https://schema.org/category" title="Category" tag="catalog">
        <doc>Genre or category of the book. Books may belong to multiple categories.</doc>
    </descriptor>
    <descriptor id="quantity" def="https://schema.org/quantityValue" title="Quantity" tag="commerce">
        <doc>Quantity of books in the cart. Integer value greater than or equal to 1.</doc>
    </descriptor>
    <descriptor id="totalAmount" def="https://schema.org/totalPrice" title="Total Amount" tag="commerce">
        <doc>Total amount for an order or cart contents. Displayed with tax included.</doc>
    </descriptor>
    <descriptor id="userName" def="https://schema.org/name" title="User Name" tag="customer">
        <doc>Name of the customer. First and last name separated by a space.</doc>
    </descriptor>
    <descriptor id="userEmail" def="https://schema.org/email" title="Email Address" tag="customer">
        <doc>Customer's contact email address. Used for sending order confirmation emails.</doc>
    </descriptor>
    <descriptor id="shippingAddress" def="https://schema.org/address" title="Shipping Address" tag="shipping">
        <doc>Delivery address for products. Includes postal code, prefecture, city, street address, and building name.</doc>
    </descriptor>
    <descriptor id="paymentMethod" def="https://schema.org/paymentMethod" title="Payment Method" tag="payment">
        <doc>Method of payment for the order. Options include credit card, cash on delivery, bank transfer, etc.</doc>
    </descriptor>
    <descriptor id="query" title="Search Query" tag="catalog">
        <doc>Keywords or conditions used for book searches. Can search by title, author name, ISBN, etc.</doc>
    </descriptor>

    <!-- Taxonomy -->
    <descriptor id="Home" title="Home Screen" tag="navigation">
        <doc>Starting point of the application. Displays site-wide navigation and promotional information.</doc>
        <descriptor href="#goToCatalog"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="Catalog" def="https://schema.org/CollectionPage" title="Book Catalog" tag="catalog">
        <doc>Screen displaying all books. Provides category filtering, keyword search, and sorting functions. Default display is ordered by recent additions.</doc>
        <descriptor href="#goListBooks"/>
        <descriptor href="#goSearchBooks"/>
        <descriptor href="#goGetCategories"/>
        <descriptor href="#goToBookDetails"/>
        <descriptor href="#goToCart"/>
        <descriptor href="#Book"/>
    </descriptor>

    <descriptor id="Book" def="https://schema.org/Book" title="Book" tag="catalog">
        <doc>Screen displaying individual book information. Shows detailed information, reviews, and related books. Items can be added to cart from this screen.</doc>
        <descriptor href="#id"/>
        <descriptor href="#title"/>
        <descriptor href="#author"/>
        <descriptor href="#isbn"/>
        <descriptor href="#price"/>
        <descriptor href="#category"/>
        <descriptor href="#doAddToCart"/>
        <descriptor href="#goToCatalog"/>
    </descriptor>

    <descriptor id="Category" def="https://schema.org/Category" title="Category" tag="catalog">
        <doc>Book genre classification. May have a hierarchical structure with parent and child categories.</doc>
        <descriptor href="#id"/>
        <descriptor href="#title"/>
    </descriptor>

    <descriptor id="ShoppingCart" def="https://schema.org/ShoppingCart" title="Shopping Cart" tag="cart">
        <doc>Cart containing books the user intends to purchase. Allows quantity changes, deletion, and total amount confirmation. Managed on a session basis.</doc>
        <descriptor href="#goListCartItems"/>
        <descriptor href="#doUpdateQuantity"/>
        <descriptor href="#doRemoveFromCart"/>
        <descriptor href="#goToCheckout"/>
        <descriptor href="#goToCatalog"/>
    </descriptor>

    <descriptor id="Checkout" title="Checkout Screen" tag="checkout">
        <doc>Purchase procedure screen. Input user information, delivery destination, and proceed to payment. Displays final confirmation before order is placed.</doc>
        <descriptor href="#doUserInfo"/>
        <descriptor href="#doShippingInfo"/>
        <descriptor href="#goToPayment"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <descriptor id="Payment" title="Payment Screen" tag="payment">
        <doc>Screen for entering payment information, confirming the order, and displaying order completion details. Handles payment method selection, payment validation, order placement, and shows order number, total amount, and estimated delivery date upon completion. A confirmation email is sent automatically.</doc>
        <descriptor href="#paymentMethod"/>
        <descriptor href="#doPaymentInfo"/>
        <descriptor href="#doPlaceOrder"/>
        <descriptor href="#goOrderDetails"/>
        <descriptor href="#goToHome"/>
        <descriptor href="#goToCart"/>
    </descriptor>

    <!-- Choreography -->
    <descriptor id="goToHome" type="safe" rt="#Home" title="Go to Home Screen">
        <doc>Navigate to the application's home screen. Accessible from any screen.</doc>
    </descriptor>
    <descriptor id="goToCatalog" type="safe" rt="#Catalog" title="Go to Catalog Screen">
        <doc>Navigate to the book catalog list screen. All books are displayed.</doc>
    </descriptor>
    <descriptor id="goToBookDetails" type="safe" rt="#Book" title="Go to Book Details Screen">
        <doc>Navigate to the detailed information screen for the selected book. Book ID must be specified.</doc>
        <descriptor href="#id"/>
    </descriptor>
    <descriptor id="goToCart" type="safe" rt="#ShoppingCart" title="Go to Cart Screen">
        <doc>Navigate to the screen displaying the contents of the current shopping cart.</doc>
    </descriptor>
    <descriptor id="goToCheckout" type="safe" rt="#Checkout" title="Go to Checkout Screen">
        <doc>Navigate to the screen to confirm cart contents and proceed with purchase. Cannot transition if cart is empty.</doc>
    </descriptor>
    <descriptor id="goToPayment" type="safe" rt="#Payment" title="Go to Payment Screen">
        <doc>Navigate to the payment screen to input payment information and complete the order.</doc>
    </descriptor>

    <descriptor id="goListBooks" type="safe" rt="#Catalog" rel="collection" title="Get Book List" tag="catalog">
        <doc>Retrieve list of all books in the catalog. Can specify pagination (default 20 items/page) and sort order (newest, price, popularity, etc.).</doc>
    </descriptor>
    <descriptor id="goSearchBooks" type="safe" rt="#Catalog" rel="collection" title="Search Books" tag="catalog">
        <doc>Search for books based on specified search query. Can search across multiple fields including title, author name, content description, ISBN, etc.</doc>
        <descriptor href="#query"/>
    </descriptor>
    <descriptor id="goGetCategories" type="safe" rt="#Catalog" rel="collection" title="Get Category List" tag="catalog">
        <doc>Retrieve list of all available book categories. For hierarchical categories, parent-child relationships are also returned.</doc>
    </descriptor>
    <descriptor id="goGetBookDetails" type="safe" rt="#Book" rel="item" title="Get Book Details" tag="catalog">
        <doc>Retrieve detailed information for a specific book based on the specified book ID. Includes stock status and related book information.</doc>
        <descriptor href="#id"/>
    </descriptor>

    <descriptor id="doAddToCart" type="unsafe" rt="#ShoppingCart" rel="collection" title="Add to Cart" tag="cart">
        <doc>Add the specified book to the shopping cart. If already in the cart, quantity is increased. Orders exceeding stock will result in an error.</doc>
        <descriptor href="#id"/>
        <descriptor href="#quantity"/>
    </descriptor>
    <descriptor id="goListCartItems" type="safe" rt="#ShoppingCart" rel="collection" title="Get Cart Items List" tag="cart">
        <doc>Retrieve all products in the current shopping cart, including their quantities, subtotals, and total amount.</doc>
    </descriptor>
    <descriptor id="doUpdateQuantity" type="idempotent" rt="#ShoppingCart" title="Update Cart Item Quantity" tag="cart">
        <doc>Update the quantity of a specific product in the cart. Values less than or equal to 0 cannot be specified. Quantities exceeding stock will result in an error.</doc>
        <descriptor href="#id"/>
        <descriptor href="#quantity"/>
    </descriptor>
    <descriptor id="doRemoveFromCart" type="idempotent" rt="#ShoppingCart" title="Remove Item from Cart" tag="cart">
        <doc>Completely remove the specified item from the cart. If the item does not exist in the cart, no changes are made.</doc>
        <descriptor href="#id"/>
    </descriptor>

    <descriptor id="doUserInfo" type="unsafe" rt="#Checkout" title="Input User Information" tag="customer">
        <doc>Input customer's name and email address. Email address is validated using regular expressions.</doc>
        <descriptor href="#userName"/>
        <descriptor href="#userEmail"/>
    </descriptor>
    <descriptor id="doShippingInfo" type="unsafe" rt="#Checkout" title="Input Shipping Information" tag="shipping">
        <doc>Input product delivery address. Features automatic address input using postal code lookup.</doc>
        <descriptor href="#shippingAddress"/>
    </descriptor>
    <descriptor id="doPaymentInfo" type="unsafe" rt="#Payment" title="Input Payment Information" tag="payment">
        <doc>Select order payment method and input necessary payment information. When credit card is selected, card information is input and validated.</doc>
        <descriptor href="#paymentMethod"/>
    </descriptor>
    <descriptor id="doPlaceOrder" type="unsafe" rt="#Payment" title="Place Order" tag="order">
        <doc>Confirm order based on user input information, process payment, and display order confirmation details on the payment screen. Payment processing is executed, inventory is secured, and a confirmation email is sent. This operation cannot be reversed.</doc>
    </descriptor>

    <descriptor id="goOrderDetails" type="safe" rt="#Payment" title="Display Order Details" tag="order">
        <doc>Display detailed information for the confirmed order on the payment screen. Includes order number, list of purchased products, total amount, delivery destination, payment method, etc.</doc>
    </descriptor>
</alps>
```

