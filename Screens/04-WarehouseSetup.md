# ⚙️ Screen: Warehouse Setup

**User Story:** As an administrator, I want to define or update the physical layout of the warehouse (number of shelves, columns, and rows) so the visual overview is accurate.

**Context:** This screen is a subpage, accessed from the `WarehouseOverview` screen.

---

## Functional Requirements

### 1. Configuration Form
Provide a simple form for defining the warehouse structure.
* **Number of Shelves:** [Integer Input] (Default: 10)
* **Number of Columns (per shelf):** [Integer Input] (Default: 10)
* **Number of Rows (per shelf):** [Integer Input] (Default: 5)

### 2. Actions
* **"Generate/Update Layout" Button:**
    * **Warning:** Show a confirmation prompt: "WARNING: Regenerating the layout may delete old slot definitions. This action cannot be undone. Proceed?"
    * **On Confirm:** The system will:
        1.  (Safeguard: Check if any slots are currently occupied. If so, warn user.)
        2.  Wipe all existing `WarehouseSlot` records.
        3.  Loop through the numbers provided (e.g., 10x10x5) and create new, empty `WarehouseSlot` records in the database.
        4.  Example record created: `SlotID: 'S1-C1-R1'`, `Shelf: 1`, `Column: 1`, `Row: 1`, `OccupiedByAssetID: null`.
    * After completion, redirect the user back to the `WarehouseOverview` screen, which will now show the new layout.
