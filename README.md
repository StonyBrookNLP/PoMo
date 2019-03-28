# PostModifier

1. Overview

This dataset is for the hackathon at <em>2018 TTIC Workshop: Collaborative & Knowledge-backed Language Generation</em>. 
It is split into train/valid/test, along with their wikidata entities. The split was done randomly but we made sure that there's no entity overlap accross the splits and followed the similar distribution of entity clusters based on their occupation. 
Currently the dataset has post modifiers for <em>HUMAN</em> entities. 

2. Files
  - /dataset
    - /human         
      - train.pm
      - train.wiki
      - test.pm
      - test.wiki
      - valid.pm
      - valid.wiki


3. Dataset Fields
  - Post modifer dataset (*.pm)
    - A data file (train/test/valid) has following fields: (tab separated)
      - sent_wo_post_modifier: A sentence without a post modifier
      - entity_name: The entity that the post modifier depends on
      - post_modifier: The post modifier
      - sent: A full sentence with the post modifier
      - wiki_id: wikidata ID. Use this to look up the wikidata entity from the accompanying file.
      - prev_sent: The previous sentence before [sent]. "n/a" if [sent] is the first sentence.
      - next_sent: The next sentence after [sent]. "n/a" if [sent] is the last sentence.
      - file_info: This field contains the source info. It is unique within the dataset. 
                   The ones starts with year (1987-2007) are NYT, cnn for CNN and dm for DailyMail.


  - Wikidata entity (*.wiki)
    - A wikidata entity file(train.wiki/test.wiki/valid.wiki) has following fields:
      - wikidata ID
      - entity_name: The wikidata entity's label
      - aliases: aliases of the label. “,” separated if there are more than one. 
      - descriptions: description of the wikidata entity. “,” separated if there are more than one. 
      - claims: processed claims of this entity in JSON. 
        - A list of   
          ```
          {
          "property": [
              <field_name>,
              <value>],
          "qualifiers": [
              <field_name>,
              <value>]]
          }
          ```
              
        - For qualifiers, if there are more than one field, it is changed to a list of list as below:
            ```
              {
                "property": [
                  "member of sports team",
                  "Wiggins"
                ],
                "qualifiers": [
                  [
                    "start time",
                    "+2015-04-30T00:00:00Z"
                  ],
                  [
                    "end time",
                    "+2016-12-31T00:00:00Z"
                  ]
                ]
              }
            ```

4. Data Sources
  - CNN and DM
    Used the tokenized CNN and Daily Mail articles from: https://github.com/JafferWilson/Process-Data-of-CNN-DailyMail
  - NYTimes
    Used the LDC's NYT corpus: http://www.ldc.upenn.edu
  - Wikidata
    Use the wikidata dump from: https://www.wikidata.org/wiki/Wikidata:Database_download
    (Dump date: 2018/06/25)
    
5. Dataset Size
  * train: 220,615 (Entities: 55,367)
  * valid:   5,200 (Entities: 1,257)
  *  test:   5,242 (Entities: 1,342)

  
