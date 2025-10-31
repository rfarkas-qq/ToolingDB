# 🖥️ Screen: Main Dashboard (Home)

**User Story:** As a production manager, I want to see a top-level overview of all tool locations and access core management areas so I can quickly assess asset distribution and navigate the app.

---

## Functional Requirements

### 1. Location Status Tiles
Display a grid of tiles based on `Location.LocationType`. Each tile must show the location name and a real-time count of `Tools` at that location.

| Tile | Count (from DB) |
| :--- | :--- |
| <h3>📦 Tooling Warehouse</h3> | `[COUNT(Tools where LocationType='ToolingWarehouse')]` |
| <h3>🏭 Production Line</h3> | `[COUNT(Tools where LocationType='ProductionLine')]` |
| <h3>🔧 Maintenance Area</h3> | `[COUNT(Tools where LocationType='MaintenanceArea')]` |
| <h3>🔬 Engineering Area</h3> | `[COUNT(Tools where LocationType='EngineeringArea')]` |
| <h3>🧼 Cleaning Area</h3> | `[COUNT(Tools where LocationType='CleaningArea')]` |
| <h3>🚚 External Supplier</h3> | `[COUNT(Tools where LocationType='ExternalSupplier')]` |
| <h3>🗄️ Archive Storage</h3> | `[COUNT(Tools where LocationType='ArchiveStorage')]` |

**Interactivity:**
* Clicking any location tile navigates the user to the corresponding subpage for that location. (e.g., clicking "Tooling Warehouse" -> `Screens/03-WarehouseOverview.md`).

### 2. Management Tiles
Display a second set of tiles for primary system actions.

| Tile | Description |
| :--- | :--- |
| <h3>🛠️ All Tools</h3> | Search, view, and modify parameters for any tool in the system. |
| <h3>➕ Register New Asset</h3> | Add a new Tool, Carrier, or Modificator to the database. |
| <h3>🔄 Quick Move</h3> | A simple interface to scan a tool and scan a new location to move it. |

**Interactivity:**
* Clicking **"All Tools"** navigates to a "Master Tool List" page (a new screen to be defined, based on `Flow 2`).
