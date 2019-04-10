[![LUNR Lab.](https://www3.cs.stonybrook.edu/~junkang/images/new_lunr_logo4_small.png)](http://lunr.cs.stonybrook.edu/)

# PoMo: Post-Modifier dataset

### Overview

   PoMo is the dataset introduced in our paper *PoMo: Generating Entity-Specific Post-Modifiers in Context* from NAACL 2019. 
   
   Our paper(arXiv version) has been released here: [https://arxiv.org/abs/1904.03111](https://arxiv.org/abs/1904.03111)


### Post-Modifier Generation Task
   
   Post-modifier is a short phrase that comes after an entity in a sentence to describe the entity in detail. It can be found easily in many news articles. For example, in the below sentence, `the MIT professor and antiwar activist` is the post-modifier of `Noam Chomsky`.
     
   
   >Noam Chomsky, the MIT professor and antiwar activist, said Dr. Melman helped mobilize what once was weak and scattered resistance to war and other military operations. 
   
    
   We formulate post-modifier generation task as a data-to-text generation problem, where the data is the context (a sentence without a post-modifier) and the set of known facts about the target entity. The text to be generated is a post-modifier that is relevant to the rest of the information conveyed in the text. Below example shows the input and output of the task.
     
   

   <a href="https://www3.cs.stonybrook.edu/~junkang/images/pm_gen_large.png"><img src="https://www3.cs.stonybrook.edu/~junkang/images/pm_gen_large.png" alt="Image of post-modifier generation task" width="500px"/></a>

### Download

   The dataset can be downloaded from [https://github.com/StonyBrookNLP/PoMo](https://github.com/StonyBrookNLP/PoMo)

### Citation

   Please use the following bibtex entry:

   ```
   (Coming soon)
   ```

### Dataset Information
   - Dataset Split

      The dataset is split into train/valid/test, along with their Wikidata entities. The split was done randomly but there is no entity overlap accross the splits. The splits show similar distribution of entity occupations. 

   - Dataset Sizes

      - train: 220,615 (Unique Entities: 55,367)
      - valid:   5,200 (Unique Entities: 1,257)
      -  test:   5,242 (Unique Entities: 1,342)

   - Dataset Fields

      - Post modifer instances (*.pm)
        - These files (train.pm/test.pm/valid.pm) have following fields: (tab separated)
          - sent_wo_post_modifier: A sentence without a post modifier
          - entity_name: The entity that the post modifier depends on
          - post_modifier: The post modifier
          - sent: A full sentence with the post modifier
          - wiki_id: Wikidata ID. Use this to look up the Wikidata entity from the accompanying file.
          - prev_sent: The previous sentence before [sent]. "n/a" if [sent] is the first sentence.
          - next_sent: The next sentence after [sent]. "n/a" if [sent] is the last sentence.
          - context_relevance_score: Crowd sourced context sensitivity of the post-modifier of this instance to its context
            - 1:Not relevant, 5:Relevant   // For train, this field is set as 0.
          - file_info: This field contains the source of each instance: filepath and line number. 
                       Since it is unique, it is used as an ID for each instance. 
                       If the value of this field starts with a year (1987-2007), it indicates the instance is from NYT corpus.
                       For instances extracted from CNN and DailyMail, this value starts with "cnn" and "dm" respectively.


      - Wikidata entity (*.wiki)
        - These files (train.wiki/test.wiki/valid.wiki) have following fields: (tab separated)
          - Wikidata ID
          - entity_name: The Wikidata entity's label
          - aliases: aliases of the label. “,” separated if there are more than one. 
          - descriptions: description of the Wikidata entity. “,” separated if there are more than one. 
          - claims: processed claims of this entity in JSON. 
            - A list of   
              ```
              {
                 "property": [<field_name>,<value>],
                 "qualifiers": [<field_name>,<value>]
                 "use":[<fileinfo_of_pm_instance>, ...]    // A list of fileinfos whose post-modifiers contain information of this claim. 
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
                    ],
                  }
                ```

### Data Sources

   We used various data sources to construct PoMo. 
  
   - CNN and DM
     - Used the tokenized CNN and DailyMail articles from: [https://github.com/JafferWilson/Process-Data-of-CNN-DailyMail](https://github.com/JafferWilson/Process-Data-of-CNN-DailyMail)
   - NYTimes
     - Used the LDC's NYT corpus from 1987 to 2007: [http://www.ldc.upenn.edu](http://www.ldc.upenn.edu)
   - Wikidata
     - Used the Wikidata dump from: [https://www.wikidata.org/wiki/Wikidata:Database_download](https://www.wikidata.org/wiki/Wikidata:Database_download)  (Dump date: 2018/06/25)


### Contributors
   
   - [Jun Seok Kang](https://www3.cs.stonybrook.edu/~junkang/) (Stony Brook University)
   - [Robert L. Logan IV](https://rloganiv.github.io/) (University of California, Irvine)
   - [Zewei Chu](http://people.cs.uchicago.edu/~zeweichu/) (University of Chicago)
   - [Yang Chen](https://edchengg.github.io/) (University of Chicago)
   - [Dheeru Dua](https://ddua.github.io/src/index.html) (University of California, Irvine)
   - [Kevin Gimpel](https://ttic.uchicago.edu/~kgimpel/) (Toyota Technological Institute at Chicago)
   - [Sameer Singh](http://sameersingh.org/) (University of California, Irvine)
   - [Niranjan Balasubramanian](https://www3.cs.stonybrook.edu/~niranjan/) (Stony Brook University)
      
   
