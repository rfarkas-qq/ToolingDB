# 🛠️ Screen: Tool Details

**User Story:** As an engineer or manager, I want to view and modify all parameters for a specific tool so I can keep its data accurate.

**Context:** This screen is accessed whenever a user clicks a specific `Tool.SerialNumber` from *any* list (Warehouse, "All Tools" list, Production Line, etc.).

---

## Functional Requirements

### 1. Tool Data Form
Display all parameters for the selected `Tool`. The form must be pre-filled with the tool's current data.

* **Serial Number:** [Text, Read-Only] e.g., "KIA-001-A01"
* **OEM Partner:** [Dropdown or Text]
* **Manufacturer:** [Text]
* **Car Model:** [Text]
* **Picture:** [Image Upload/Display]
* **Release Date:** [Date Picker]
* **Tilt (degrees):** [Number (decimal)]
* **Airbag:** [Checkbox or Yes/No Toggle]
* **Autovents:** [Number (integer)]
* **Part Number (Finished Good):** [Text]

### 2. Current Status (Read-Only)
Display the tool's current location and relationships.
* **Current Location:** [Text] e.g., "Tooling Warehouse / S1-C2-R3" or "Production Line 1"
* **Mounted on Carrier:** [Text, Link] e.g., "CARR-005" or "None"
* **Modificator Installed:** [Text, Link] e.g., "MOD-002" or "None"

### 3. Cavity Management (Sub-section)
* Display a list of all `Cavities` associated with this tool.
* Allow user to change the `Status` of each `Cavity` ('Good', 'NeedsRepair').
