# Prompt: Tooling Warehouse Management Logic

## 1. Context & Purpose
The goal is to develop a software logic for managing a **tooling warehouse** in a foam parts manufacturing plant. The warehouse stores heavy tools (molds) in a rack-based system.

## 2. Warehouse Structure
The warehouse is organized into **Racks**. Each rack is a grid defined by:
* **Rack Name**: Unique identifier (e.g., "Rack_A").
* **Columns**: Vertical sections.
* **Rows**: Horizontal levels.

A unique storage position is identified by the triplet: `(Rack_Name, Column, Row)`.

## 3. Configuration Table
The system must be initialized using a configuration structure that defines the limits for each rack.
| Rack Name | Max Columns | Max Rows |
| :--- | :--- | :--- |
| Rack_A | 5 | 10 |
| Rack_B | 3 | 5 |
| Rack_C | 8 | 4 |

## 4. Required Operations
Implement the following core functionalities:

* **InitializeWarehouse**: Set up the environment based on the configuration table.
* **ValidatePosition(rack, col, row)**: Verify if the given coordinates are within the defined limits for the specific rack.
* **StoreTool(tool_id, rack, col, row)**: Assign a tool to a position. 
  * *Constraint*: Fail if the position is occupied or out of bounds.
* **RetrieveTool(rack, col, row)**: Remove a tool from a position. 
  * *Constraint*: Fail if the position is already empty.
* **MoveTool(source, destination)**: Transfer a tool from one valid position to another.
* **GetInventoryReport**: Return a list of all occupied positions and their contents.

## 5. Logic Rules
1. **Indexing**: Use 1-based indexing for rows and columns.
2. **Error Handling**: Provide clear feedback for:
   - `OUT_OF_BOUNDS`
   - `POSITION_OCCUPIED`
   - `TOOL_NOT_FOUND`
3. **Uniqueness**: A single tool cannot exist in multiple locations simultaneously.
