## Technology Stack

* **Frontend:** React  
* **Backend:** Node.js 
* **Database:** Prisma as ORM
    * Option A: PostgreSQL
    * Option B: MS SQL
* **Auth:**
    * email
    * Optional: Azure AD / Entra ID integration (enterprise SSO)

**Core Principles:**
* Avoid DB-specific features 
* Keep logic in application layer
* Use Prisma as strict abstraction

---

## Naming Conventions

* **JavaScript:** Use `camelCase` for variables, functions, and object properties in app code.
* **Domain data:** Use `snake_case` to match the PostgreSQL schema (e.g., `location_id`, `serial_number`, `current_location_id`).
* **HTML/CSS:** Use `kebab-case` for ids and classes.
* **Screen names:** Simple lowercase route keys (e.g., `locations`, `assets`, `warehouse`, `maintenance`).
* **Warehouse identifiers:** Explicit domain names (e.g., `Rack_A`, `Rack_B`, `Rack_C`).
* **Warehouse API:** Clear verb-based methods:
    * `InitializeWarehouse`
    * `ValidatePosition`
    * `StoreTool`
    * `RetrieveTool`
    * `MoveTool`
    * `GetInventoryReport`

---

## Architectural Practices

* **Separation of Concerns:** Rendering, formatting, data, and warehouse rules are split instead of mixed together.
* **Navigation:** The app uses hash-driven screen switching rather than one long dashboard.
* **Logic Style:** Pure-function style for data transformations where possible, especially in warehouse and report generation logic.
* **State Management:** In-memory warehouse state with explicit error codes:
    * `OUT_OF_BOUNDS`
    * `POSITION_OCCUPIED`
    * `TOOL_NOT_FOUND`
* **Coordinate System:** 1-based indexing for warehouse coordinates.
* **Visual Consistency:** Shared renderer for warehouse racks so the locations and warehouse screens stay visually and logically consistent.
* **Data Portability:** Client-side export via JSON snapshot generation.
* **Rendering Pattern:** View-model style rendering: derive filtered views, then render the DOM from those derived objects.
* **Public API:** Exposure on `window.ToolingWarehouse` so the warehouse logic is reusable outside the UI.

---

## Universal Unit Testing Strategy

Implement a comprehensive unit testing suite using **Vitest** (recommended for Wasp/React) to ensure reliability across all system objects and logic layers.

### General Testing Requirements:
- **Isolation:** Each object (Warehouse, I18nManager, etc.) must be tested in isolation.
- **Pattern:** Use the **Arrange-Act-Assert (AAA)** pattern for all test cases.
- **Coverage:** Aim for 100% coverage of core business logic and edge cases.

### Specific Object Test Cases:

#### A. Warehouse Logic (`ToolingWarehouse` object)
- **Initialization:** Verify correct grid setup for various rack configurations.
- **Validation:** Test `ValidatePosition` with valid, out-of-bounds, and negative coordinates.
- **State Changes:** - Verify `StoreTool` updates state correctly and prevents double-occupancy.
    - Verify `RetrieveTool` clears the state and returns the correct tool ID.
    - Verify `MoveTool` correctly executes a "remove from A, add to B" atomic-like operation.
- **Errors:** Ensure explicit error codes (`OUT_OF_BOUNDS`, `POSITION_OCCUPIED`, etc.) are returned correctly.

#### B. Translation Logic (`I18nManager` object)
- **Loading:** Verify that the correct JSON file is loaded based on `config.json`.
- **Key Lookup:** Test retrieval of existing keys and handling of missing keys (fallback mechanism).
- **Interpolation:** Verify that variables (e.g., `{tool_id}`) are correctly injected into the translated strings.

#### C. Data & State Management
- **Immutability:** Ensure that state updates do not produce unintended side effects in the original data objects.
- **Snapshot Export:** Verify that the generated JSON snapshot matches the expected schema and contains all current warehouse data.

### Implementation Note:
Mock external dependencies (like the file system for JSON loading) to ensure tests are fast, deterministic, and do not rely on the actual environment.

---

## Security & Access Control

All database interactions must be governed by a centralized **Security Module** to enforce granular access control.

### Authorization Workflow
Before any database object (Prisma model) executes a query, it must verify permissions through the security service.

* **Service Method:** `SecurityModule.authorize(user_id, table_name, access_type)`
* **Parameters:**
    * `user_id`: The identifier of the authenticated user.
    * `table_name`: The target or source database table (e.g., `assets`, `warehouse_slots`).
    * `access_type`: One of the defined actions: `READ`, `WRITE`, `MODIFY`, `DELETE`.
* **Response:** `Boolean` (`true` to allow, `false` to deny).

### Access Type Definitions:
- **READ:** Permission to view or fetch data.
- **WRITE:** Permission to create new records.
- **MODIFY:** Permission to update existing records.
- **DELETE:** Permission to remove records.

### Implementation Rule:
- Authorization checks must be performed on the **application layer** (Backend) before calling Prisma methods.
- If `authorize` returns `false`, the operation must throw a `SECURITY_UNAUTHORIZED` error and log the attempted access.

---

## Logging & Activity Tracking

The system must implement a centralized **Logger Service** to track system behavior, security events, and user activities.

### Logging Levels
The logging verbosity is controlled via a configuration setting in `config.json` (e.g., `"log_level": "INFO"`). 
Available levels (from least to most verbose):
- **ERROR:** Only critical failures and exceptions.
- **WARN:** Potential issues or failed authorization attempts.
- **INFO:** Standard operational events (successful logins, tool movements).
- **DEBUG (Everything):** Detailed execution flow, database queries, and state changes for development purposes.

### Audit Categories
1. **Authentication Logs:**
   - Log every login and logout attempt.
   - Include `user_id`, `timestamp`, and `status` (Success/Failure).
2. **Activity Logs (Audit Trail):**
   - Log all warehouse operations: `StoreTool`, `RetrieveTool`, `MoveTool`.
   - Record: `Who` (user_id), `What` (action), `Which` (tool_id), `Where` (source/destination), and `When` (timestamp).
3. **System Logs:**
   - Database connection status, initialization events, and unhandled exceptions.

### Implementation Requirements:
- **Persistence:** High-level logs (Auth & Activity) must be stored in the database via Prisma for permanent auditing.
- **Console Output:** All logs should be piped to the standard output (stdout) according to the configured level.
- **Performance:** Logging should be asynchronous to ensure it does not block the main application thread.
