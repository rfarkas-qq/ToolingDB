# Task: i18n Support

## 1. Task Overview
Add support for multiple languages (i18n) by loading all user-facing strings from external JSON files.

## 2. Directory Structure
The project must follow this structure:
- `/lang` - Directory containing translation files (e.g., `en.json`, `sk.json`).
- `config.json` - Configuration file defining the `default_language`.
- `i18n.py` - Language logic.

## 3. Multi-language (i18n) Requirements
- **Externalization**: No hardcoded strings in the main logic. Every error message, success notification, and report header must be fetched from the `/lang` directory.
- **Language Manager**: Create a class/module that:
    1. Reads `config.json` to determine the active language.
    2. Loads the corresponding `.json` file from the `/lang` folder at startup.
    3. Provides a translation function (e.g., `t("KEY")`) with support for variables/placeholders (e.g., "Tool {id} not found").
- **Fallback**: If a key is missing in the primary language, return the key itself or a fallback English string.

## 4. Deliverables
1. **Source Code**: A clean, documented Python implementation.
2. **Example Translations**:
    - `lang/en.json`: Containing keys for `ERR_OCCUPIED`, `ERR_OUT_OF_BOUNDS`, `MSG_STORED`, etc.
    - `lang/sk.json`: Slovak version of the same keys.
3. **Configuration**: A sample `config.json` with a language toggle.

## 5. Constraints
- Use robust error handling.
- Ensure the system is easily extensible for new languages (adding a new JSON file should be enough).

Language selection will be on the top of main page.
