## HAS-master/src/
- `H-path.py` generates H-path based on homogeneity, and H method generates entity vectors;

- `A-path.py` generates A-path based on attribute similarity, and A method to generate entity vectors;

- `S-path.py` generates S-path based on structural similarity, and S method to generate entity vectors;

- `HAS_combine_seq.py`  is used to merge the paths of all entities, and then use the language model;

- `findneighbors.py` is used to find neighbors in the cube of a entity;

The rest of the files is used to process the data information in the sqlite table. For example,dividing labels into string type labels and numeric type labels.
