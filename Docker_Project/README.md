## Functionalities

### Set up Ruuter instance

https://github.com/buerokratt/Data-Anonymizer/issues/61

Set up [Ruuter](Ruuter/) instance with a [docker-compose](docker-compose.yml) configuration.

Always run `docker-compose up -d` to start all docker containers.

### Set up ReSQL instance

https://github.com/buerokratt/Data-Anonymizer/issues/62

Set up [Resql](Resql/) instance, and added docker-compose containers for Resql and Postgres Database.

### Set up Data Model

https://github.com/buerokratt/Data-Anonymizer/issues/74

Add [Resql Query](Resql/templates/production/create_schema.sql) and a [bash script](Resql/listen_server.sh) to create database schema automatically.

### Upload private corpus to the database

https://github.com/buerokratt/Data-Anonymizer/issues/69

- Add [Ruuter DSL File](Ruuter/DSL/POST/corpora_info.yml) and [Resql Query](Resql/templates/production/insert_corpora_info.sql) to create a corpora info record.
- Add [Ruuter DSL File](Ruuter/DSL/POST/corpora.yml) and [Resql Query](Resql/templates/production/insert_corpora_task.sql) to create tasks in bulk (upload corpora).

### View list of Regex patterns added by user

https://github.com/buerokratt/Data-Anonymizer/issues/60

Add [Ruuter DSL File](Ruuter/DSL/GET/regex.yml) and [Resql Query](Resql/templates/production/list_regex.sql) to list regex patterns.

### Delete added Regex pattern from database

https://github.com/buerokratt/Data-Anonymizer/issues/63

Add [Ruuter DSL File](Ruuter/DSL/GET/delete_regex.yml) and [Resql Query](Resql/templates/production/delete_regex.sql) to delete a regex pattern.

### Add new Regex pattern to the database

https://github.com/buerokratt/Data-Anonymizer/issues/59

- Add [Ruuter DSL File](Ruuter/DSL/POST/regex.yml) and [Resql Query](Resql/templates/production/insert_regex.sql) to add a regex pattern.
- Add [Ruuter DSL File](Ruuter/DSL/GET/entity.yml) and [Resql Query](Resql/templates/production/list_entity.sql) to list entities.

### Add new entity

https://github.com/buerokratt/Data-Anonymizer/issues/89

Add [Ruuter DSL File](Ruuter/DSL/POST/entity.yml) and [Resql Query](Resql/templates/production/insert_entity.sql) to add an entity.

### Show list of sentences and Filter sentences by ID

https://github.com/buerokratt/Data-Anonymizer/issues/46
https://github.com/buerokratt/Data-Anonymizer/issues/47

- Add [Ruuter DSL File](Ruuter/DSL/GET/tasks.yml) and [Resql Query](Resql/templates/production/get_corpora.sql) to list corpora tasks based on pagination and filters.
- Add [Ruuter DSL File](Ruuter/DSL/GET/task.yml) and [Resql Query](Resql/templates/production/get_task.sql) to get a particular task detail.
- Add [Ruuter DSL File](Ruuter/DSL/GET/corpora_info.yml) and [Resql Query](Resql/templates/production/get_corpora_info.sql) to get latest corpora info.

### Label a sentence

https://github.com/buerokratt/Data-Anonymizer/issues/43

Add [Ruuter DSL File](Ruuter/DSL/POST/annotate.yml) and [Resql Query](Resql/templates/production/upsert_corpora_task.sql) to annotate a particular sentence with labels.

### Set up Label Studio

https://github.com/buerokratt/Data-Anonymizer/issues/45

Set up [Label Studio Frontend](Label-Studio/) React Application, and add docker-compose configuration. Environment Variable for Backend (Ruuter Application) should be set up [here](docker-compose.yml#L43). The website url for this application should be added list of [whitelisted urls](Ruuter/src/main/resources/application.yml#L27) for Ruuter.

### Setup React Application for Data Management Frontend Application

https://github.com/buerokratt/Data-Anonymizer/issues/93

Set up [Data Management Frontend](dm/) React Application, and add docker-compose configuration. Environment Variables for [Backend (Ruuter Application)](docker-compose.yml#L58) and [Label Studio Frontend](docker-compose.yml#L59) should be configured.

### Define routes for Anonymizer and Training Pages

https://github.com/buerokratt/Data-Anonymizer/issues/94

Define [routes](dm/src/App.js) for [Anonymizer](dm/src/components/Anonymizer.js) and [Training](dm/src/components/Treening.js) components.

### Implement UI Design for Page Header, Navigation, Drawer and Footer

https://github.com/buerokratt/Data-Anonymizer/issues/95

Add UI Components for [Header](dm/src/components/Header.js), [Navigation Mobile Drawer](dm/src/components/Drawer.js), [Footer](dm/src/components/Footer.js) and [Github Section](dm/src/components/GithubSection.js)

### Implement UI Design for Anonymizer Page

https://github.com/buerokratt/Data-Anonymizer/issues/98

Add UI Component for [Anonymizer](dm/src/components/Anonymizer.js) Page.

### Implement UI Design for Training Page

https://github.com/buerokratt/Data-Anonymizer/issues/96

Add UI Component for [Training](dm/src/components/Treening.js) Page.

### UI Backend API Integration

https://github.com/buerokratt/Data-Anonymizer/issues/97

Add [Services](dm/src/RestService.js) to call Backend REST APIs, integrate Anonymizer and Training Pages, and add website url of this application to list of [whitelisted urls](Ruuter/src/main/java/ee/buerokratt/ruuter/controller/DslController.java#L28) for Ruuter.

### Add i18n support to Data Management Interface front end app

https://github.com/buerokratt/Data-Anonymizer/issues/79

Install [i18next](dm/package.json#L10) and [react-i18next](dm/package.json#L13) packages, add [translations](dm/src/translations/et.json), and transform all text in the UI utilize the translations. Languages can be modfied [here](dm/src/index.js#L10).

### Train a custom model

https://github.com/buerokratt/Data-Anonymizer/issues/65

- Add [Model Training Service](ml-training-service) and a [docker-compose configuration](docker-compose.yml#L66).
- Add Ruuter DSL Files to [train model](Ruuter/DSL/POST/train.yml) and [get training status](Ruuter/DSL/GET/training_status.yml).
- Add a [Ruuter DSL File](Ruuter/DSL/POST/update_corpora_info.yml) and [Resql Query](Resql/templates/production/upsert_corpora_info.sql) to update a corpora info record [after training is done](ml-training-service/executor/ner_trainer.py#L98).
- Add a [Ruuter DSL File](Ruuter/DSL/GET/trained_corpora_info.yml) and [Resql Query](Resql/templates/production/get_trained_corpora_info.sql) to get latest trained corpora details.

The system allows for fine-tuning one of the NER models with additional data to adapt the model to a specific domain. Machine learning models are quite context sensitive so it is possible that in a specific domain the performance decreases and it can be improved by manually labelling additional data and teaching the model to recognize entities better in this new context.

#### Requirements for data

The data used for training the model must meet the following criteria:

1. Diversity - the data chosen for training should cover the variation in actual usage scenario as completely as possible. The best way to do this is label an immense amount of data, but as this is often not feasible, the sample labelled should be chosen at random from a diverse set of in-domain documents.
2. Volume - there needs to be a sufficient amount of data to train the model on. Because the amount required depends on a number of factors, it is not possible to say exactly how much is enough, but a rough estimate can be given. For a model with the complexity of the ones used here, more than 200 samples should be labeled - the more the better.
3. Accuracy - quality beats quantity in machine learning in most cases and it is especially true in the case of fine-tuning with a small amount of data. The data should be labelled correctly or the machine will learn to repeat the mistakes.

#### Process

1. Select a sample of data for labelling
2. Upload the corpus from the UI
3. Label the corpus manually in the labelling interface
4. Start training the model

Training time depends on the volume of data and your hardware. It scales about linearly with the nr of CPU cores available and the volume of data.  
As a result one of the four models in the system will be fine-tuned and the old version replaces with the new, just trained one.

### Anonymize/pseudonymize a sentence

https://github.com/buerokratt/Data-Anonymizer/issues/64

Add [Anonymizer Service](anonymisation_internal), docker-compose configurations and Ruuter [DSL File](Ruuter/DSL/POST/pseudonymise.yml) to pseudonymise a sentence. The prediction endpoint in Anonymizer Service can be found [here](anonymisation_internal/anonymisation_api/anonymise/accept_request.py). Relevant models should be placed inside [models folder](anonymisation_internal/anonymisation_api/anonymise/models/).

### Automatically pre-label uploaded corpus

https://github.com/buerokratt/Data-Anonymizer/issues/66

Add Ruuter DSL Files to to [pre-label list of corpora sentences](Ruuter/DSL/POST/annotate_corpora.yml) and [get prelabelling status](Ruuter/DSL/GET/prelabelling_status.yml), and a [ReSQL](Resql/templates/production/get_latest_corpora.sql) query to get full corpora. The annotation endpoint (/annotate_corpora) in Anonymizer Service can be found [here](anonymisation_internal/anonymisation_api/anonymise/accept_request.py).

### Make script to upload a new public NER corpus

https://github.com/buerokratt/Data-Anonymizer/issues/73

Add [script](Upload_Corpora_Git_Script) to upload latest corpora to GitHub. Steps to execute the script:

```
cd Upload_Corpora_Git_Script
npm install
GIT_OWNER="<GIT_OWNER_ID>" GIT_REPO="<GIT_REPO_ID>" GIT_TOKEN="<GIT_PERSONAL_ACCESS_TOKEN>" API_URL="<RUUTER_URL>" node index.js
```

### Entity Recognition models based on search engine

https://github.com/buerokratt/Data-Anonymizer/issues/76

In this system Search is implemented through Regexes, as exactly matching a word is a case of matching regular expressions. For example the system uses multiple lists of entities to find street names, organizations, people, countries, etc. in text. The lists used can be seen in `./Docker_Project/anonymisation_internal/anonymisation_api/anonymise/gazetteers`.  
The end user can customize this functionality by adding their own regex requiring exactly matching one of a number of elements in a list. For example a regex for matching workdays:  
`(?:^|(?<=[.|,|;|:|\s|!|?]))(esmaspäev|teisipäev|kolmapäev|neljapäev|reede)(?=[.|,|;|:|\s|!|?]|$)`

### Machine-learning-based NER models

https://github.com/buerokratt/Data-Anonymizer/issues/77

The system uses 4 separate machine learning based models for performing Named Entity Recognition (NER) on the input text. These entities are used in downstream tasks for anonymization and pseudonymization. The models are hosted on [Huggingface](https://huggingface.co/buerokratt)

1. bert-truecaser - fixes casing in a sentence as wrong casing can have significant impact on downstream machine learning tasks.
2. ner_old - base NER model, trained on wikipedia data, recognizing 3 entities: person, organization, location.
3. ner_new - fine-tuned NER model, trained additionally on manually labelled data, recognizing 11 entities: person, organization, location, product, date, time, event, money, percentage, title, geopolitical entity.
4. ner_gdpr - fine-tuned NER model, trained additionally on manually labelled data, recognizing the same 11 entities as ner_new, but trained on a different data set.

Each model has its strengths and weaknesses and they are combined in this system so that they would cover each others weaknesses and recognize the entities as well as possible while remaining as specific as possible.  
Generally the 4th model takes precedence as it is the most accurate on the full set of entities. If it found nothing, the 3rd model's results take precendece. This is important and the 3rd model is the one that can be fine-tuned with manually labelled data.

The system expects the models to be in the following directories:

1. /models/bert-truecaser
2. /models/bert_old
3. /models/bert_new
4. /models/gdpr_model

### Entity Recognition models based on regular expressions (regex)

https://github.com/buerokratt/Data-Anonymizer/issues/78

Where possible and useful, the system uses regular expressions (regexes) to find specific entities that have a well defined pattern, such as URLs, email addresses, phone numbers, etc. A lot of regexes have been pogrammed into the system during development, but it is possible for the end user to add their own patterns for entities so that the system would also find those in text.  
The system expects the new regular expression to follow [Python's re module specification](https://docs.python.org/3/library/re.html). Nothing special here.

Some examples of the regexes used in the system:

- Addresses: `")((\s*(tänav|tee|rada|põik|maantee|tn|mnt|pst|puiestee)\s*[1-9]([0-9]{1,2}[a-z]?)?(\s*-\s*[0-9]{1,3})?)|(\s(tänav|tee|põik|maantee|tn|mnt|pst|puiestee|rada))|(\s[1-9]([0-9]{1,2}[a-z]?)?(\s*-\s*[0-9]{1,3})?))(?=[.|,|;|:|\s|!|?]|$)"`
- Urls: `"(http|ftp|https):\/\/([\w_-]+(?:(?:\.[\w_-]+)+))([\w.,@?^=%&:\/~+#-]*[\w@?^=%&\/~+#-])"`

The regexes defined and generated can be seen in `./Docker_Project/anonymisation_internal/anonymisation_api/anonymise/utils/utils.py`

### Create tests for the back end

https://github.com/buerokratt/Data-Anonymizer/issues/102

- Add [Testing Framework](testing-framework) to run E2E Ruuter & Resql Tests.
- Add separate [docker-compose file](docker-compose.test.yml) to run test instances of resql, ruuter, db and the framework itself.
- Add [file](docker_test_run.sh) to pause running production resql & ruuter containers, start test containers, run tests and resume the production containers after succssful execution.
  To execute testing suite, run `./docker_test_run.sh`.

### Evaluation results

Results on RIA dataset (test set):

<pre>
processed 31371 tokens with 2124 phrases; found: 2339 phrases; correct: 1746.
accuracy:  85.20%; (non-O)
accuracy:  97.21%; precision:  74.65%; recall:  82.20%; FB1:  78.24
             DATE: precision:  60.80%; recall:  71.33%; FB1:  65.64  176
            EVENT: precision:  47.83%; recall:  65.67%; FB1:  55.35  92
              GPE: precision:  84.21%; recall:  87.11%; FB1:  85.63  361
              LOC: precision:  59.13%; recall:  60.18%; FB1:  59.65  115
            MONEY: precision:  24.24%; recall:  57.14%; FB1:  34.04  33
              ORG: precision:  72.19%; recall:  78.04%; FB1:  75.00  320
              PER: precision:  93.42%; recall:  93.71%; FB1:  93.56  638
          PERCENT: precision:  72.73%; recall:  88.89%; FB1:  80.00  22
             PROD: precision:  51.94%; recall:  62.21%; FB1:  56.61  206
             TIME: precision:  46.67%; recall:  63.64%; FB1:  53.85  30
            TITLE: precision:  72.54%; recall:  87.46%; FB1:  79.30  346

</pre>

### Deployment should happen with docker-compose up command

https://github.com/buerokratt/Data-Anonymizer/issues/145

- To deploy project with default environment variables run `docker-compose up -d`.
- Backend (Ruuter Application) url could be configured on [Label Studio Client](docker-compose.yml#L43) and [Data Management Client](docker-compose.yml#L58) docker configs. The website urls for Label Studio and Data Management Frontends application could be added to list of [whitelisted urls](Ruuter/src/main/resources/application.yml#L27) for Ruuter Application. Label Studio Frontend url should also be be setup as a [Data management client docker config](docker-compose.yml#L59)
