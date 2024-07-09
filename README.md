# Alma/ArchivesSpace Integrations Plugin - Beinecke Adaptation

## Introduction

This project is an adaptation of the Alma/ArchivesSpace Integrations plugin originally developed by Kevin Clair. The original plugin provides integrations between the ArchivesSpace archival collection management system and the Alma library management system from Ex Libris, building upon the Top Container functionality developed by Hudson Molonglo for ArchivesSpace.

This fork is specifically geared toward the needs of the Beinecke Rare Book and Manuscript Library, extending and customizing the plugin's functionality to better suit our workflows and integration requirements. While maintaining the core features of the original plugin, this project aims to enhance and tailor the integration process for Beinecke's unique environment.

We acknowledge and appreciate the foundational work done by Kevin Clair, which has made this adaptation possible.

## Current Features
- Checks for BIBs with a Resource's MMS ID in Alma
- Checks for holdings associated with the BIB identified by the MMS ID
- Allows adding new holdings in Alma
- Creates new BIB records in Alma if no MMS ID is present or doesn't match existing records
- Synchronizes changes from ArchivesSpace Resources to Alma BIB records
- Provides a user interface for viewing and managing Alma metadata (BIBs, Holdings, Items) within ArchivesSpace

## Planned Enhancements
I am planning to extend this plugin's functionality in the following ways:

1. MARCXML Integration:
   - Enhance the ArchivesSpace MARCXML export to include all necessary data for bibliographic, holdings, and item records.
   - Develop a MARCXML parser to extract data for all three record types from a single MARCXML file.

2. Alma API Expansion:
   - Extend the Alma API integration to handle creation and updating of bibliographic, holdings, and item records simultaneously.

3. Workflow Improvements:
   - Create a streamlined process for exporting MARCXML from ArchivesSpace and creating/updating corresponding records in Alma.
   - Implement batch processing capabilities for handling multiple resources at once.

4. Configuration Flexibility:
   - Add options for customizing field mappings and default values for holdings and item records.

5. User Interface Enhancements:
   - Develop an improved interface for initiating the MARCXML export and Alma record creation process.
   - Add progress indicators and detailed result summaries.

6. Testing and Documentation:
   - Implement comprehensive testing for new functionalities.
   - Provide updated documentation for the enhanced plugin features and workflows.

These planned enhancements aim to create a more robust and flexible integration between ArchivesSpace and Alma, streamlining workflows and improving data synchronization between the two systems.

## Contributing
Feedback and contributions are welcome! Please feel free to submit a Pull Request.

## License

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/).
