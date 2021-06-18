## Entity_Profiles/src/main/java/

- `RDFDatabase.java` Parsing raw data(eg:.rdf/.nt/.ttl).

- `creat_base_table.java`  Build 3 tables: property\_triples\_table, property\_mid\_support, relations\_triples. 
`property_triples_table` Statistics Attribute triple.Subject and object must have type. `property_mid_support`: Summary table of attribute information,Convenient for later inquiry.
`relations_triples`: Statistics relation triple.Subject and object must have type.

- `make_support.java` Statistical support value of attribute (the type of the attribute is string).

- `Numerical_discretization.java`: Continuous numerical discretization.

- `filter_support.java` Filter attribute values of support(According to your respective needs).

- `cosine_similarity.java` Obtain the vector of the entity through the HAS(H,A,S,HAS) model, Counting the cosine similarity of an entity with a property set.

- `salience.java` Use the pagerank algorithm to find the center of each entity. Use the center of the entity to find the first relationship label.

- `filter_relations.java` Filter relations according to the values of the salience(According to your respective needs).

- `relation_property.java` Create the relation_property labels.

- `relation_similarity.java` Obtain the vector of the entity through the HAS(H,A,S,HAS) model, Counting the cosine similarity of an entity with a relational set.

- `resort_labels.java` Label-set resorting. Distinctive labels are listed in front to make final tags set.

- `attach_tags.java` Label the entity after creating the final tag set.
