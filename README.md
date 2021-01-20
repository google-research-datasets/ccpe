# CCPE-M: Coached Conversational Preference Elicitation dataset for Movies

## COPYRIGHT NOTICE

This is the work of Filip Radlinski, Krisztian Balog, Bill Byrne and Karthik Krishnamoorthi from Google LLC, made available under the Creative Commons Attribution 4.0 License. A full copy of the license can be found at https://creativecommons.org/licenses/by/4.0/

## DATA COLLECTION METHODOLOGY

This corpus consists of dialogues between two paid crowd-workers using a Wizard-of-Oz methodology. One worker plays the role of an "assistant", while the other plays the role of a "user". The "assistant" is tasked with eliciting the "user" preferences about movies following a Coached Conversational Preference Elicitation (CCPE) methodology. In particular, the assistant is required to ask questions designed so as to minimize the bias in the terminology the "user" employs to convey his or her preferences, and obtain these in as natural language as possible. Each dialog is annotated with entity mentions, preferences expressed about entities, descriptions of entities provided, and other statements of entities (see ontology below).

A full description of the data, methodology, and analyses as well as sample conversations and user instructions can be found in [the associated research paper](https://www.aclweb.org/anthology/W19-5941/), which can be cited as:
```
@inproceedings{radlinski-etal-2019-ccpe,
  title = {Coached Conversational Preference Elicitation: A Case Study in Understanding Movie Preferences},
  author = {Filip Radlinski and Krisztian Balog and Bill Byrne and Karthik Krishnamoorthi},
  booktitle = {Proceedings of the Annual Meeting of the Special Interest Group on Discourse and Dialogue ({SIGDIAL})},
  year = 2019
}
```

## EXPLANATION OF DATA FILES

The dialogue corpus is provided in JSON format in the file data.json.

Each conversation has the following fields:
* conversationId: A unique random ID for the conversation. The ID has no meaning.
* utterances: An array of utterances by the workers.

Each utterance has the following fields:
* index: A 0-based index indicating the order of the utterances in the conversation.
* speaker: Either USER or ASSISTANT, indicating which role generated this utterance.
* text: The raw text as written by the ASSISTANT, or transcribed from the spoken recording of USER.
* segments: An array of semantic annotations of spans in the text.

Each semantic annotation segment has the following fields:
* startIndex: The position of the start of the annotation in the utterance text.
* endIndex: The position of the end of the annotation in the utterance text.
* text: The raw text that has been annotated.
* annotations: An array of annotation details for this segment.

Each annotation has two fields:
* annotationType: The class of annotation (see ontology below).
* entityType: The class of the entity to which the text refers (see ontology below).

## EXPLANATION OF ONTOLOGY

In the corpus, preferences and the entities that these preferences refer to are annotated with an annotation type as well as an entity type.

Annotation types fall into four categories:
* ENTITY_NAME: These mark the names of relevant entities mentioned.
* ENTITY_PREFERENCE: These are defined as statements indicating that the dialog participant does or does not like the relevant entity in general, or that they do or do not like some aspect of the entity. This may also be thought of the participant having some sentiment about what is being discussed.
* ENTITY_DESCRIPTION: Neutral descriptions that describe an entity but do not convey an explicit liking or disliking.
* ENTITY_OTHER: Other relevant statements about an entity that convey relevant information of how the participant relates to the entity but do not provide a sentiment. Most often, these relate to whether a participant has seen a particular movie, or knows a lot about a given entity.

Entity types are marked as belonging to one of four categories:
* MOVIE_GENRE_OR_CATEGORY for genres or general descriptions that capture a particular type or style of movie.
* MOVIE_OR_SERIES for the full or partial name of a movie or series of movies.
* PERSON for the full or partial name of an actual person.
* SOMETHING_ELSE for other important proper nouns, such as the names of characters or locations.

## CHANGES
2019-09-20: Fixed unicode decoding error resulting in a small number of startIndex and endIndex corrections.
