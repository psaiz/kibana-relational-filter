# kibana-relational-filter
Kibana Relational Filter

This is a kibana plugin to create filters based on different indices. It creates a new visualization, the relational-filter, which can be included in dashboards. The visualization comes with two display options: a standard table and a drop-down menu. 

Imagine any of the following scenarios: 

 * Your company has a list of all the sales and another list with all the customers. You want to get a list of all the sales to customers of a particular country
 * You have list of movies and actors, and you want to get all the movies with an actor that has won an Oscar
 * 

All these scenarios are quite easy to solve with relational databases. The current approach to solve them with elasticsearch and kibana is to denormalize the data: create a single document type with the replication of all the information that might be needed. Elasticsearch does offer parent-child relation (see https://www.elastic.co/guide/en/elasticsearch/reference/5.2/mapping-parent-field.html). At the time of writting this plugin, Kibana does not support it. 

This plugin offers a different alternative to do all these relational queries. The approach is to keep the two types of documents separate, even on different indices,  and then create a visualization that will do the select on the first type of document, and apply the filter to the second. 

Coming back to the examples, this would be the approach:

* Create a document type with sales, which include an attribute like 'user'.  Create a different document type with users, which includes, at least, 'user' and 'country'. Create a relational-filter visualization on the users, displaying the field 'country', and applying the restriction on the 'user'.
* Create a document type with the movies, which include a list user 'actor'. Create a different document type with actors, with at least a field call 'actor' and another with 'awarded_oscar'. Create a relational-filter on the actors, displaying the field 'awarded_oscar', and applying the restricion on 'user'.


And here you have a couple of screen shots of those two use cases:




# TODO

This is the very first draft of the plugin. There are quite a lot of possible improvements, like:

 * Add multi select possibilities
 * Add option to include the document type of the filter in the query
 * Offer multiple filters on different documents
