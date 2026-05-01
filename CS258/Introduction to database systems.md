# Principal functions of a DBS
- Store data
- Model data
- Access data: query + update
- Analyse data
- Secure data

Data can be structured (tables) or unstructured (raw data, ie json)


# On data modelling

You should be concerned with :
- What are the data items that i care to know of
- What are the data items attributes
- Relationships between data items

A relation is a table of values
Rows -> entries in the table, some entity or relationship
Each column is a characteristic or attribute of interest of the entity 


Key of relation must be a uniquely identifiable attribute


Order of attributes and tuples is not important

Domain constraints of an attribute can also be NULL, ie spouse name for single people 

Super key is basically what determines the tuple, 2 tuples cannot share a super key

Candidate key is a minimal super key



Functional dependencies:

basically when one attribute depends on another, ie name depends on id

They are transitive



# Related


