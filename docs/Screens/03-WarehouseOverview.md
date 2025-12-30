# 📦 Screen: Tooling Warehouse Overview

**User Story:** As a warehouse operator, I want to see a visual layout of all shelves so I can quickly find a tool or identify an empty storage slot.

**Context:** This screen is accessed by clicking the "Tooling Warehouse" tile on the `MainDashboard`.

---

## Functional Requirements

### 1. Visual Layout
* Dynamically generate a grid (or series of grids) based on the `WarehouseSlot` data.
* Group the display by `Shelf` (e.g., "Shelf 1", "Shelf 2"...).
* For each shelf, display a grid of cells representing `Column` and `Row`.
* **Cell Styling:**
    * **Empty Slot:** (where `OccupiedByAssetID` is null) - Display as 'Available' (e.g., green background).
    * **Occupied Slot:** (where `OccupiedByAssetID` is not null) - Display as 'Occupied' (e.g., red background) and show the `SerialNumber` of the asset in the cell.

### 2. Interactivity
* **Hover:** Hovering over an occupied cell must show a tooltip with more tool details (e.g., "Tool: KIA-001-A01, Part: Sorento").
* **Click (Occupied):** Clicking an occupied cell navigates to the `Screens/02-ToolScreen.md` for that specific tool.
* **Click (Empty):** Clicking an empty cell could start a "Move Tool to this Slot" flow (future feature).

### 3. Navigation
* This page must include a clear button or link: **"⚙️ Configure Layout"**.
* Clicking this button navigates the user to `Screens/04-WarehouseSetup.md`.
