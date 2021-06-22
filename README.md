# 基于网络角色的知识图谱缺失知识补全方法

&emsp;&emsp; 知识图谱作为人工智能技术的重要组成部分，被广泛应用于智能问答、智能搜索、个性化推荐等领域中。然而，知识图谱由于其动态增长的特性，始终存在着数据稀疏的问题，影响着人工智能模型的精度。知识图谱中知识的缺失问题亟待解决，知识图谱补全的概念得到了学术界和工业届的广泛关注。


&emsp;&emsp;现有的知识图谱补全方法大多依赖于知识图谱中实体间的关系，然而，真实知识图谱中部分实体由于较为罕见有较少的关系可达，这使得学习得到的向量表示质量较低，从而影响模型的精度。此外，由于处理非离散数据类型的属性值具有一定的挑战性，现有的先进的关系学习模型大多忽略了这些属性信息，在属性预测方面的研究较少。并且，现有的知识补全模型大都是基于原知识图谱中的三元组结构，这需要用户具有知识图谱的背景，才能迅速理解预测结果，忽视了可理解性的重要性。基于现有的工作背景，本文提出了一种基于网络角色的知识图谱缺失知识补全方法，来解决上述问题，主要研究内容如下：
	

（1）提出一种基于网络角色的知识图谱实体嵌入方法。根据实体间不同层面的相似等效性，从同质性、属性相似性、结构相似性三个方面来进行实体角色发现，生成不同的实体路径，得到语义丰富的实体嵌入表示，解决了表示学习受知识图谱中关系稀疏影响较大的问题。
	

（2）提出一种基于实体标签的知识补全方法。将画像标签结果作为预测模型的输入输出，用户通过少量的实体画像标签就可以快速理解预测结果，增强了结果的可理解性。同时将连续值属性离散化，利用模糊预测代替属性值的精确预测，属性预测的结果由确切的数值变为值域范围。
	

（3）设计并实现基于网络角色的知识补全系统。该系统能够搜索查询目标实体，动态显示知识图谱中的实体画像标签补全的结果。同时，显示利用本研究的方法预测出的的标签补全结果的拟合度情况。
	

&emsp;&emsp;综上所述，本文研究了基于网络角色的知识图谱缺失知识补全方法：首先基于实体角色相似性生成实体嵌入表示，该实体嵌入表示用于生成实体画像标签。然后以实体标签作为知识补全模型的输入输出，进行标签预测任务，在真实的知识图谱数据集上进行实验，结果表明该方法的预测效果明显优于大多数现有模型。最后，设计并实现了知识图谱补全系统。

## Knowledge Graph Completion Based on Network Role
As an important part of artificial intelligence technology, knowledge graph has been widely used in intelligent question-answering, intelligent search, personalized recommendation and other fields.
However, due to the dynamic growth of knowledge graph, the existence of data sparsity affects the accuracy of artificial intelligence model.The problem of incompleteness of knowledge graph needs to be solved urgently. The concept of knowledge graph completion has been widely concerned in academia and industry.
	
	

Most of the existing knowledge graph completion methods rely on the relations between entities in the knowledge graph. However, some entities in the real knowledge graph are rare and have fewer relations, which leads to low quality of entity representation learned, thus affecting the accuracy of the model.
In addition, due to the challenge of processing non-discrete attribute values, most of the existing advanced relational learning models ignore these attribute information, and there are few researches on attribute prediction.
Moreover, existing knowledge completion models are based on the triples of the knowledge graph, which requires users who have the background of the knowledge graph to quickly understand the prediction results, ignoring the importance of comprehensibility.	Based on the existing researches, a novel knowledge graph completion method based on network role is proposed to solve the above problems. The main content is as follows:
	
	
(1) A knowledge graph entity embedding method based on network role is proposed.
According to the different similarities between entities, the entity role is discovered from three aspects of homogeneity, attributive similarity and structural similarity.Then different entity paths are generated to obtain representations of entities which have rich semantic information, solving the problem that the representation learning is negatively affected by the sparse relation in the knowledge graph.
	
	
(2) A novel knowledge graph completion method based on entity label is proposed.
With entity labels as the input and output of the  model, users can quickly understand the prediction results through a small number of entity labels, which enhances the comprehensibility of the results.
At the same time, the non-discrete attribute value is discretized, and the fuzzy prediction is used to replace the exact prediction of the attribute value, so the result of attribute prediction is changed from the exact value to the range.
	
(3) Design and implement a knowledge graph completion system based on network role.
The system can search the target entity and display the completion result of entity profiles in the knowledge graph dynamically.
At the same time, the degree of fitting of the corresponding label prediction results are shown.


In summary, a novel knowledge graph completion method based on network role is proposed: Firstly, the entity representations which are generated based on the entity role similarity, are used to generate the entity profiles. Then, with the entity labels as the input and output of knowledge graph completion model, new entity labels are predicted. Experimental results on real knowledge graph datasets show that the prediction performance of the proposed method is better than most existing models. Finally knowledge graph completion system is designed and implemented.


## Dataset

In our experiments, we use two real-world knowledge graph to evaluate knowledge graph completion: 

(1) **FB15k**, which is a subset of Freebase, a curated KB of general facts. We use original training, validation and test set splits as provided by [*Bordes et al. (2013b)*](https://proceedings.neurips.cc/paper/2013/file/1cecc7a77928ca8133fa24680a88d2f9-Paper.pdf).

(1) [**FB15k-237**](https://www.microsoft.com/en-us/download/details.aspx?id=52312), which is a subset of FB15k.As the dataset of the early knowledge completion task, FB15k has some problems of test set leakage. The inverse relation triplet prediction based on simple rule reasoning can achieve the effect of advanced model.
Therefore, FB15k-237 removes the inverse relationship in FB15K and only includes symmetric/antisymmetric and combinatorial relations.

(3) [**DBpedia**](https://wiki.dbpedia.org/downloads-2016-10), which is a domain-independent encyclopedic dataset covering a broad range of descriptions of entities, such as people, location and company. 



## Code
This method performs data analysis and storage operations for some data formats such as rdf/n3/nt..., and other training related information can be found in [deepwalk](https://github.com/phanein/deepwalk)

Our core code is in the folder called entity_profiling-master. It contains 3 parts: **HAS_master**, **Entity_Profiles** and **KGC**.

### HAS-master/src/
- `H-path.py` generates H-path based on homogeneity, and H method generates entity vectors;

- `A-path.py` generates A-path based on attribute similarity, and A method to generate entity vectors;

- `S-path.py` generates S-path based on structural similarity, and S method to generate entity vectors;

- `HAS_combine_seq.py`  is used to merge the paths of all entities, and then use the language model;

- `findneighbors.py` is used to find neighbors in the cube of a entity;

The rest of the files is used to process the data information in the sqlite table. For example,dividing labels into string type labels and numeric type labels.


### Entity_Profiles/src/main/java/

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

### KGC
- Requirements

TensorFlow (1.4)
