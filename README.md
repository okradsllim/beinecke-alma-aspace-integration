```
# ArchivesSpace Alma Integration Plugin

## Current Functionality

This plugin provides integration between ArchivesSpace and Alma, focusing on MARC record synchronization and holdings management. It leverages the Alma API to perform operations and presents a user interface within ArchivesSpace for managing these integrations.

### Key Features

1. Bi-directional sync between ArchivesSpace and Alma (push only)
2. MARC record comparison
3. Holdings management
4. Item display from Alma within ArchivesSpace

### Configuration

The plugin requires specific configuration in ArchivesSpace's `config.rb` file:

```ruby
AppConfig[:alma_api_url] = 'https://api-na.hosted.exlibrisgroup.com/almaws/v1/bibs'
AppConfig[:alma_apikey] = 'your_api_key_here'
AppConfig[:alma_holdings] = [
  ['building_code1', 'location_code1'],
  ['building_code2', 'location_code2']
]
```

### Core Components

1. **Controller (alma_integrations_controller.rb)**

   Handles user interactions and API calls:

   ```ruby
   def search
     @results = do_search(params)
   end

   def add_bibs
     post_bibs(params)
   end

   def add_holdings
     post_holdings(params)
   end
   ```

2. **Alma Integrator (alma_integrator.rb)**

   Manages communication with the Alma API:

   ```ruby
   def search_bibs(ref, mms)
     aspace = get_archivesspace_bib(ref)
     alma = get_alma_bib(mms)
     results['marc'] = sync_bibs(aspace, alma) if aspace['content'] && alma['content']
     results
   end

   def post_bib(mms, data)
     uri = mms.nil? ? URI(@baseurl) : URI("#{@baseurl}/#{mms}")
     uri.query = URI.encode_www_form({:apikey => @key})
     response = AlmaRequester.new.post(uri, data, :use_ssl => true)
   end
   ```

3. **Record Builder (record_builder.rb)**

   Constructs MARC XML for new or updated records:

   ```ruby
   def build_bib(record, mms)
     marc = Nokogiri::XML(record)
     # ... (code to build XML structure)
     data.root.add_child(marc.at_css('record'))
     data.to_xml
   end

   def build_holding(code, id)
     # ... (code to construct holdings XML)
     builder.to_xml
   end
   ```

## Improvement Ideas

To enhance the plugin's functionality and flexibility, I propose the following improvements:

1. **MARCXML Export Enhancement**
   - Modify the ArchivesSpace MARCXML export to include all necessary data for bib, holdings, and item records.
   - Add configuration options for field inclusion.

2. **MARCXML Parser**
   - Create a new class to parse MARCXML and extract bib, holdings, and item data:

   ```ruby
   class MarcXMLParser
     def parse(xml)
       doc = Nokogiri::XML(xml)
       {
         bib: extract_bib_data(doc),
         holdings: extract_holdings_data(doc),
         items: extract_item_data(doc)
       }
     end

     private

     def extract_bib_data(doc)
       # Implementation
     end

     # Other extraction methods...
   end
   ```

3. **Enhanced Alma API Integration**
   - Expand `AlmaIntegrator` to handle all record types:

   ```ruby
   class AlmaIntegrator
     def create_or_update_bib(data)
       # Implementation
     end

     def create_or_update_holdings(bib_id, data)
       # Implementation
     end

     def create_or_update_item(holdings_id, data)
       # Implementation
     end
   end
   ```

4. **Two-way Synchronization**
   - Implement functionality to pull changes from Alma back to ArchivesSpace.

5. **Improved Error Handling and Logging**
   - Implement robust error handling and detailed logging for better troubleshooting.

These enhancements are untested, but could make the plugin more flexible, powerful, and easier to maintain.
```
