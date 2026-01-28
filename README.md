# Component Catalog Repository

This repository serves as a data source for a component viewer application. It uses a structured format to define various hardware components, their dimensions, and standards.

## Structure

The data is organized hierarchically in directories. Each directory represents a category or a specific component type.

Inside each leaf directory (representing a specific component), you will find:
- `config.yaml`: Identifying data, schema definition, and the actual dimensional data.
- `diagram.svg`: A vector graphic representing the component, likely used to visualize the dimensions enclosed in the `config.yaml`.

Example structure:
```
/
├── screws/
│   ├── socket_head/
│   │   ├── config.yaml
│   │   └── diagram.svg
├── smd/
│   ├── diodes/
│   │   ├── config.yaml
│   │   └── diagram.svg
```

## Data Format (config.yaml)

The `config.yaml` file is the core data file for each component. It follows a consistent schema:

### Root Fields

- **`name`** (string): The human-readable name of the component (e.g., "Socket Head Cap Screws").
- **`standard`** (string): The industrial standard the component conforms to (e.g., "DIN 912 / ISO 4762").
- **`columns`** (list): Defines the columns for the data table.
- **`data`** (list): Contains the actual rows of data.

### Columns Definitions

The `columns` field is a list of objects, each defining a property of the component.

- **`key`** (string): The unique identifier for this property. This key is used in the `data` entries.
- **`label`** (string): The display name for this property (e.g., "Head Diameter (Max)").

### Data Entries

The `data` field is a list of objects where each object represents a variant of the component (e.g., a specific size).

- Keys in the data objects must correspond to the `key`s defined in the `columns` section.
- Values are typically strings including units (e.g., "10mm").

### Example

```yaml
name: "Socket Head Cap Screws"
standard: "DIN 912 / ISO 4762"
columns:
  - key: "size"
    label: "Nominal Size"
  - key: "H"
    label: "Head Diameter (Max)"
data:
  - { size: "M3", H: "5.5mm" }
  - { size: "M4", H: "7.0mm" }
```

## Diagrams

Each component folder includes a `diagram.svg`. This image is expected to visually reference the keys defined in the `columns` (e.g., showing where dimension "H" or "L" is measured on the physical part).
