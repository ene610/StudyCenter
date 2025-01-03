# Introduction

All organizations rely on information to make decisions, answer questions, and function efficiently. The problem for most organizations is not a lack of information, but the challenge of finding and extracting the information from the massive set of documents, databases, and other sources in which the information is stored.

For example, suppose _Margie's Travel_ is a travel agency that specializes in organizing trips to cities around the world. Over time, the company has amassed a huge amount of information in documents such as brochures, as well as reviews of hotels submitted by customers. This data is a valuable source of insights for travel agents and customers as they plan trips, but the sheer volume of data can make it difficult to find relevant information to answer a specific customer question.

![A diagram showing how a travel agent searches for information to help customer plan a trip.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-azure-cognitive-search-solution/media/travel-agent.png)

To address this challenge, Margie's Travel can implement a solution in which the documents are indexed and made easy to search. This solution enables agents and customers to query the index to find relevant documents and extract information from them.

## Azure AI Search

Azure AI Search provides a cloud-based solution for indexing and querying a wide range of data sources, and creating comprehensive and high-scale search solutions. With Azure AI Search, you can:

- Index documents and data from a range of sources.
- Use cognitive skills to enrich index data.
- Store extracted insights in a knowledge store for analysis and integration.

By the end of this module, you'll learn how to:

- Create an Azure AI Search solution
- Develop a search application
# Manage capacity

To create an Azure AI Search solution, you need to create an **Azure AI Search** resource in your Azure subscription. Depending on the specific solution you intend to build, you may also need Azure resources for data storage and other application services.

## Service tiers and capacity management

When you create an Azure AI Search resource, you must specify a _pricing tier_. The pricing tier you select determines the capacity limitations of your search service and the configuration options available to you, as well as the cost of the service. The available pricing tiers are:

- **Free (F)**. Use this tier to explore the service or try the tutorials in the product documentation.
- **Basic (B)**: Use this tier for small-scale search solutions that include a maximum of 15 indexes and 2 GB of index data.
- **Standard (S)**: Use this tier for enterprise-scale solutions. There are multiple variants of this tier, including **S**, **S2**, and **S3**; which offer increasing capacity in terms of indexes and storage, and **S3HD**, which is optimized for fast read performance on smaller numbers of indexes.
- **Storage Optimized (L)**: Use a storage optimized tier (**L1** or **L2**) when you need to create large indexes, at the cost of higher query latency.

Note

It's important to select the most suitable pricing tier for your solution, because you can't change it later. If you find that the pricing tier you have chosen is no longer suitable for your solution, you must create a new Azure AI Search resource and recreate all indexes and objects.

### Replicas and partitions

Depending on the pricing tier you select, you can optimize your solution for scalability and availability by creating _replicas_ and _partitions_.

- _Replicas_ are instances of the search service - you can think of them as nodes in a cluster. Increasing the number of replicas can help ensure there is sufficient capacity to service multiple concurrent query requests while managing ongoing indexing operations.
    
- _Partitions_ are used to divide an index into multiple storage locations, enabling you to split I/O operations such as querying or rebuilding an index.
    

The combination of replicas and partitions you configure determines the _search units_ used by your solution. Put simply, the number of search units is the number of replicas multiplied by the number of partitions (R x P = SU). For example, a resource with four replicas and three partitions is using 12 search units.

Tip

You can learn more about pricing tiers and capacity management in the [Azure AI Search documentation](https://learn.microsoft.com/en-us/azure/search/search-sku-tier).
# Understand search components

An AI Search solution consists of multiple components, each playing an important part in the process of extracting, enriching, indexing, and searching data.

## Data source

![A diagram showing a conceptual illustration of a data source.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-azure-cognitive-search-solution/media/data-source.png)

Most search solutions start with a _data source_ containing the data you want to search. Azure AI Search supports multiple types of data source, including:

- Unstructured files in Azure blob storage containers.
- Tables in Azure SQL Database.
- Documents in Cosmos DB.

Azure AI Search can pull data from these data sources for indexing.

Alternatively, applications can push JSON data directly into an index, without pulling it from an existing data store.

## Skillset

![A diagram a conceptual illustration of a skillset.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-azure-cognitive-search-solution/media/skillset.png)

In a basic search solution, you might index the data extracted from the data source. The information that can be extracted depends on the data source. For example, when indexing data in a database, the fields in the database tables might be extracted; or when indexing a set of documents, file metadata such as file name, modified date, size, and author might be extracted along with the text content of the document.

While a basic search solution that indexes data values extracted directly from the data source can be useful, the expectations of modern application users have driven a need for richer insights into the data. In Azure AI Search, you can apply artificial intelligence (AI) _skills_ as part of the indexing process to enrich the source data with new information, which can be mapped to index fields. The skills used by an indexer are encapsulated in a _skillset_ that defines an enrichment pipeline in which each step enhances the source data with insights obtained by a specific AI skill. Examples of the kind of information that can be extracted by an AI skill include:

- The language in which a document is written.
- Key phrases that might help determine the main themes or topics discussed in a document.
- A sentiment score that quantifies how positive or negative a document is.
- Specific locations, people, organizations, or landmarks mentioned in the content.
- AI-generated descriptions of images, or image text extracted by optical character recognition.
- Custom skills that you develop to meet specific requirements.

## Indexer

![A diagram showing a conceputal illustration of an indexer.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-azure-cognitive-search-solution/media/indexer.png)

The _indexer_ is the engine that drives the overall indexing process. It takes the outputs extracted using the skills in the skillset, along with the data and metadata values extracted from the original data source, and maps them to fields in the index.

An indexer is automatically run when it is created, and can be scheduled to run at regular intervals or run on demand to add more documents to the index. In some cases, such as when you add new fields to an index or new skills to a skillset, you may need to reset the index before re-running the indexer.

## Index

![A diagram showing a conceputal illustration of  an index.](https://learn.microsoft.com/en-gb/training/wwl-data-ai/create-azure-cognitive-search-solution/media/index.png)

The index is the searchable result of the indexing process. It consists of a collection of JSON documents, with fields that contain the values extracted during indexing. Client applications can query the index to retrieve, filter, and sort information.

Each index field can be configured with the following attributes:

- **key**: Fields that define a unique key for index records.
- **searchable**: Fields that can be queried using full-text search.
- **filterable**: Fields that can be included in filter expressions to return only documents that match specified constraints.
- **sortable**: Fields that can be used to order the results.
- **facetable**: Fields that can be used to determine values for _facets_ (user interface elements used to filter the results based on a list of known field values).
- **retrievable**: Fields that can be included in search results (_by default, all fields are retrievable unless this attribute is explicitly removed_).

# Understand the indexing process

The indexing process works by creating a **document** for each indexed entity. During indexing, an _enrichment pipeline_ iteratively builds the documents that combine metadata from the data source with enriched fields extracted by cognitive skills. You can think of each indexed document as a JSON structure, which initially consists of a **document** with the index fields you have mapped to fields extracted directly from the source data, like this:

- **document**
    - **metadata_storage_name**
    - **metadata_author**
    - **content**

When the documents in the data source contain images, you can configure the indexer to extract the image data and place each image in a **normalized_images** collection, like this:

- **document**
    - **metadata_storage_name**
    - **metadata_author**
    - **content**
    - **normalized_images**
        - **image0**
        - **image1**

Normalizing the image data in this way enables you to use the collection of images as an input for skills that extract information from image data.

Each skill adds fields to the **document**, so for example a skill that detects the _language_ in which a document is written might store its output in a **language** field, like this:

- **document**
    - **metadata_storage_name**
    - **metadata_author**
    - **content**
    - **normalized_images**
        - **image0**
        - **image1**
    - **language**

The document is structured hierarchically, and the skills are applied to a specific _context_ within the hierarchy, enabling you to run the skill for each item at a particular level of the document. For example, you could run an optical character recognition (_OCR_) skill for each image in the normalized images collection to extract any text they contain:

- **document**
    - **metadata_storage_name**
    - **metadata_author**
    - **content**
    - **normalized_images**
        - **image0**
            - **Text**
        - **image1**
            - **Text**
    - **language**

The output fields from each skill can be used as inputs for other skills later in the pipeline, which in turn store _their_ outputs in the document structure. For example, we could use a _merge_ skill to combine the original text content with the text extracted from each image to create a new **merged_content** field that contains all of the text in the document, including image text.

- **document**
    - **metadata_storage_name**
    - **metadata_author**
    - **content**
    - **normalized_images**
        - **image0**
            - **Text**
        - **image1**
            - **Text**
    - **language**
    - **merged_content**

The fields in the final document structure at the end of the pipeline are mapped to index fields by the indexer in one of two ways:

1. Fields extracted directly from the source data are all mapped to index fields. These mappings can be _implicit_ (fields are automatically mapped to in fields with the same name in the index) or _explicit_ (a mapping is defined to match a source field to an index field, often to rename the field to something more useful or to apply a function to the data value as it is mapped).
2. Output fields from the skills in the skillset are explicitly mapped from their hierarchical location in the output to the target field in the index.
# Search an index

After you have created and populated an index, you can query it to search for information in the indexed document content. While you could retrieve index entries based on simple field value matching, most search solutions use _full text search_ semantics to query an index.

## Full text search

Full text search describes search solutions that parse text-based document contents to find query terms. Full text search queries in Azure AI Search are based on the _Lucene_ query syntax, which provides a rich set of query operations for searching, filtering, and sorting data in indexes. Azure AI Search supports two variants of the Lucene syntax:

- **Simple** - An intuitive syntax that makes it easy to perform basic searches that match literal query terms submitted by a user.
- **Full** - An extended syntax that supports complex filtering, regular expressions, and other more sophisticated queries.

Client applications submit queries to Azure AI Search by specifying a search expression along with other parameters that determine how the expression is evaluated and the results returned. Some common parameters submitted with a query include:

- **search** - A search expression that includes the terms to be found.
- **queryType** - The Lucene syntax to be evaluated (_simple_ or _full_).
- **searchFields** - The index fields to be searched.
- **select** - The fields to be included in the results.
- **searchMode** - Criteria for including results based on multiple search terms. For example, suppose you search for _comfortable hotel_. A searchMode value of _Any_ returns documents that contain "comfortable", "hotel", or both; while a searchMode value of _All_ restricts results to documents that contain both "comfortable" and "hotel".

Query processing consists of four stages:

1. _Query parsing_. The search expression is evaluated and reconstructed as a tree of appropriate subqueries. Subqueries might include _term queries_ (finding specific individual words in the search expression - for example _hotel_), _phrase queries_ (finding multi-term phrases specified in quotation marks in the search expression - for example, _"free parking"_), and _prefix queries_ (finding terms with a specified prefix - for example _air*_, which would match _airway_, _air-conditioning_, and _airport_).
2. _Lexical analysis_ - The query terms are analyzed and refined based on linguistic rules. For example, text is converted to lower case and nonessential _stopwords_ (such as "the", "a", "is", and so on) are removed. Then words are converted to their _root_ form (for example, "comfortable" might be simplified to "comfort") and composite words are split into their constituent terms.
3. _Document retrieval_ - The query terms are matched against the indexed terms, and the set of matching documents is identified.
4. _Scoring_ - A relevance score is assigned to each result based on a term frequency/inverse document frequency (TF/IDF) calculation.

Note

For more information about querying an index, and details about **simple** and **full** syntax, see [Query types and composition in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-query-overview) in the Azure AI Search documentation.
# Apply filtering and sorting

It's common in a search solution for users to want to refine query results by filtering and sorting based on field values. Azure AI Search supports both of these capabilities through the search query API.

## Filtering results

You can apply filters to queries in two ways:

- By including filter criteria in a _simple_ **search** expression.
- By providing an OData filter expression as a **$filter** parameter with a _full_ syntax search expression.

You can apply a filter to any _filterable_ field in the index.

For example, suppose you want to find documents containing the text _London_ that have an **author** field value of _Reviewer_.

You can achieve this result by submitting the following _simple_ **search** expression:

```
search=London+author='Reviewer'
queryType=Simple
```

Alternatively, you can use an OData filter in a **$filter** parameter with a _full_ Lucene search expression like this:

```
search=London
$filter=author eq 'Reviewer'
queryType=Full
```

Tip

OData **$filter** expressions are case-sensitive!

### Filtering with facets

_Facets_ are a useful way to present users with filtering criteria based on field values in a result set. They work best when a field has a small number of discrete values that can be displayed as links or options in the user interface.

To use facets, you must specify _facetable_ fields for which you want to retrieve the possible values in an initial query. For example, you could use the following parameters to return all of the possible values for the **author** field:

```
search=*
facet=author
```

The results from this query include a collection of discrete facet values that you can display in the user interface for the user to select. Then in a subsequent query, you can use the selected facet value to filter the results:

```
search=*
$filter=author eq 'selected-facet-value-here'
```

## Sorting results

By default, results are sorted based on the relevancy score assigned by the query process, with the highest scoring matches listed first. However, you can override this sort order by including an OData **orderby** parameter that specifies one or more _sortable_ fields and a sort order (_asc_ or _desc_).

For example, to sort the results so that the most recently modified documents are listed first, you could use the following parameter values:

```
search=*
$orderby=last_modified desc
```

Note

For more information about using filters, see [Filters in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-filters). For information about working with results, including sorting and hit highlighting, see [How to work with search results in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-pagination-page-layout).
# Enhance the index

With a basic index and a client that can submit queries and display results, you can achieve an effective search solution. However, Azure AI Search supports several ways to enhance an index to provide a better user experience. This topic describes some of the ways in which you can extend your search solution.

## Search-as-you-type

By adding a _suggester_ to an index, you can enable two forms of search-as-you-type experience to help users find relevant results more easily:

- _Suggestions_ - retrieve and display a list of suggested results as the user types into the search box, without needing to submit the search query.
- _Autocomplete_ - complete partially typed search terms based on values in index fields.

To implement one or both of these capabilities, create or update an index, defining a suggester for one or more fields.

After you've added a suggester, you can use the **suggestion** and **autocomplete** REST API endpoints or the .NET **DocumentsOperationsExtensions.Suggest** and **DocumentsOperationsExtensions.Autocomplete** methods to submit a partial search term and retrieve a list of suggested results or autocompleted terms to display in the user interface.

Note

For more information about suggesters, see [Add autocomplete and suggestions to client apps](https://learn.microsoft.com/en-us/azure/search/search-autocomplete-tutorial) in the Azure AI Search documentation.

## Custom scoring and result boosting

By default, search results are sorted by a relevance score that is calculated based on a term-frequency/inverse-document-frequency (TF/IDF) algorithm. You can customize the way this score is calculated by defining a _scoring profile_ that applies a weighting value to specific fields - essentially increasing the search score for documents when the search term is found in those fields. Additionally, you can _boost_ results based on field values - for example, increasing the relevancy score for documents based on how recently they were modified or their file size.

After you've defined a scoring profile, you can specify its use in an individual search, or you can modify an index definition so that it uses your custom scoring profile by default.

Note

For more information about scoring profiles, see [Scoring Profiles](https://learn.microsoft.com/en-us/azure/search/index-add-scoring-profiles) in the Azure AI Search documentation.

## Synonyms

Often, the same thing can be referred to in multiple ways. For example, someone searching for information about the United Kingdom might use any of the following terms:

- United Kingdom
- UK
- Great Britain*
- GB*

_*To be accurate, the UK and Great Britain are different entities - but they're commonly confused with one another; so it's reasonable to assume that someone searching for "United Kingdom" might be interested in results that reference "Great Britain"._

To help users find the information they need, you can define _synonym maps_ that link related terms together. You can then apply those synonym maps to individual fields in an index, so that when a user searches for a particular term, documents with fields that contain the term or any of its synonyms will be included in the results.

For more information about synonym maps, see [Synonyms in Azure AI Search](https://learn.microsoft.com/en-us/azure/search/search-synonyms) in the Azure AI Search documentation.