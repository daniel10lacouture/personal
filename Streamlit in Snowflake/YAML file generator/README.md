![Snowflake SQL Optimizer](https://github.com/Snowflake-Labs/snowflake-demo-streamlit/raw/main/shared_assets/sis-header.jpeg)
# Cortex Analyst YAML Generator

## Overview

This Streamlit application simplifies the creation of YAML files for [Snowflake's Cortex Analyst](https://docs.snowflake.com/LIMITEDACCESS/snowflake-cortex/cortex-analyst-overview#overview). It helps users select databases, schemas, and tables to auto-fill the YAML structure with relevant information. The generated YAML files can then be downloaded or copied for use in creating semantic models for Cortex Analyst. Note that some additional details such as synonyms, sample values, and descriptions will need to be added manually.

## Features

- **Database Selection**: Choose from available databases.
- **Schema Selection**: Select schemas within the chosen database.
- **Table Selection**: Pick tables to include in the YAML file.
- **YAML Auto-Fill**: Automatically populate the YAML structure with table definitions.
- **YAML Download**: Download the generated YAML file.

## Instructions

### 0. Setup Code
- **Purpose**: Create a SiS applciaiotn. Copy and paste the .py file from this repo.
  
### 1. Welcome Page
- **Purpose**: Provides an overview of the app and instructions on how to use it.
- **Details**: Explains the features and steps to create a YAML file for Snowflake's Cortex Analyst.

### 2. Get Started Page
- **Purpose**: Collects basic information about the semantic model.
- **Details**: 
  - Enter Semantic Name: Input the name of your semantic model.
  - Enter Description: Provide a detailed description of the semantic model.
  - Click "Save Semantic Model Info" to proceed to the Table Definition page.

### 3. Table Definition Page
- **Purpose**: Allows users to define tables and columns for the semantic model.
- **Details**:
  - Select Database: Choose the database from the dropdown menu.
  - Select Schema: Select the schema associated with the chosen database.
  - Select Table: Pick the table you want to include in the YAML file.
  - Click "Add Table to YAML" to add the selected table to the YAML structure. The YAML display will be updated accordingly.
  - Download YAML: Once your tables are added, you can download the generated YAML file by clicking on the "Download YAML file" button.

### 4. Reset Application
- **Purpose**: Clears all saved data and resets the application.
- **Details**: 
  - Navigate to the "Reset" page from the sidebar.
  - Click the "Reset" button to clear all saved data and reset the application to its initial state.

## Usage

1. **Start the App**: Open the Streamlit app and navigate through the sidebar to the "Welcome" page.
2. **Get Started**: Enter the semantic model name and description, then save the info.
3. **Define Tables**: Select the database, schema, and tables to include in your YAML file. Add them to the YAML structure.
4. **Download YAML**: Once the YAML structure is complete, download the YAML file for use in Cortex Analyst.
5. **Reset**: If needed, reset the application to clear all data and start fresh.

For further details, refer to the [Snowflake Documentation](https://docs.snowflake.com/LIMITEDACCESS/snowflake-cortex/semantic-model-spec#label-semantic-model-tips).

![Yaml file generator](https://github.com/daniel10lacouture/personal/blob/main/Streamlit%20in%20Snowflake/YAML%20file%20generator/cortex-analyst-yaml-generator.png)
