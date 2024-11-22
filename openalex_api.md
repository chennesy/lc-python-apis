---
title: "The OpenAlex API"
teaching: 45
exercises: 2
---

::::::::::::::::::::::::::::::::::::: objectives

- Import and utilize the requests library to send a GET request to OpenAlex.
- Make an API call for a single work in OpenAlex.
- Navigate the requests response object.
- Use JSON to format and examine data returned from the OpenAlex API.
- Use Python dictionary keys and values to pinpoint specific metadata.
- Use nested key access to navigate nested dictionary data structures.


::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- 

::::::::::::::::::::::::::::::::::::::::::::::::::


## API call for a scholarly work

Let's create an API call to obtain metadata related to a single scholarly work in OpenAlex. To send the GET request to OpenAlex with Python, we can import the ```requests``` library.

```python
import requests
```

Next, let's structure a URL to send a GET request about a scholarly work to OpenAlex.

OpenAlex provides a series of [entities](https://docs.openalex.org/api-entities/entities-overview) that we can use to asks for different kinds of data. In this case, we can use [the Works entity](https://docs.openalex.org/api-entities/works) to request data about things like journal articles, books, datasets, and theses that are indexed by OpenAlex. To access data from a single work, we can append any DOI (e.g., ```https://doi.org/10.18352/lq.10176```) to the base URL for Works (```https://api.openalex.org/works/```).

Once we have the URL and DOI ready, we can send it as a parameter of our GET request using the ```requests.get()``` function.

```python
base_url = 'https://api.openalex.org/works/'
doi = 'https://doi.org/10.18352/lq.10176'

# concatenate the URL and DOI strings using the + operator
response = requests.get(base_url + doi)
response
```

```output
<Response [200]>
```

The response object will output the HTTP response status code: in our case, `Response [200]` means the request succeeded.  

We can explore the response in greater depth by calling the `.text()` method, which shows the content of the response as a string. 

```python
response.text()
```

The output of `response.text()` is a very long unformatted string that is pretty difficult to read! Fortunately, `requests` includes a `.json()` method that is better for working with data that follows the key and value structure that we see here. 

JSON refers to [JavaScript Object Notation](https://glosario.carpentries.org/en/#json), and is a common structure for API responses to follow. In our case, the `.json()` method will format the response as a Python dictionary.

```python
response.json()
```

```output
{'id': 'https://openalex.org/W2560151723',
 'doi': 'https://doi.org/10.18352/lq.10176',
 'title': 'Library Carpentry: Software Skills Training for Library Professionals',
 'display_name': 'Library Carpentry: Software Skills Training for Library Professionals',
 'publication_year': 2016,
 'publication_date': '2016-11-01',
 'ids': {'openalex': 'https://openalex.org/W2560151723',
  'doi': 'https://doi.org/10.18352/lq.10176',
  'mag': '2560151723'},
 'language': 'en',
 'primary_location': {'is_oa': True,
  'landing_page_url': 'https://doi.org/10.18352/lq.10176',
  'pdf_url': 'http://www.liberquarterly.eu/articles/10.18352/lq.10176/galley/10667/download/',
  'source': {'id': 'https://openalex.org/S2736366396',
   'display_name': 'LIBER Quarterly The Journal of the Association of European Research Libraries',
   'issn_l': '2213-056X',
   'issn': ['2213-056X', '1435-5205'],
   'is_oa': True,
   'is_in_doaj': True,
   'is_core': True,
 ...
 ```
 
### Python dictionaries
 
This output shows metadata fields stored as 'keys' and the data as 'values', in the structure of a Python dictionary. Python dictionaries are key/value pairs that are wrapped in curly brackets--`{}`-- with the key and value delineated by a colon, and each key/value pair separated by a comma. The first two key/value pairs in the dictionary above, for example, are: 
 
 ```
 {'id': 'https://openalex.org/W2560151723',
 'doi': 'https://doi.org/10.18352/lq.10176',
 ```
 
 The string `id` is the first key, and the string `https://openalex.org/W2560151723` is its corresponding value. While these keys and values are both strings, Python dictionaries can contain other data types as keys and values as well. `2016` in the key/value pair `'publication_year': 2016,` for example, is an integer. 
 
 While we have a hint that we're dealing with a dictionary, since the output of `response.json()` begins with a curly bracket, we can check by calling the `type()` function. First let's save the JSON response to a new variable:
 
 ```python
 json_response = response.json()
 type(json_response)
 ```
 
  ```output
  dict
  ```
  
To look at the list of all of the keys in the dictionary, we can call:
  
  ```python
json_response.keys()
 ```
 
  ```output
dict_keys(['id', 'doi', 'title', 'display_name', 'publication_year', 'publication_date', 'ids', 'language', 'primary_location', 'type', 'type_crossref', 'indexed_in', 'open_access', 'authorships', 'institution_assertions', 'countries_distinct_count', 'institutions_distinct_count', 'corresponding_author_ids', 'corresponding_institution_ids', 'apc_list', 'apc_paid', 'fwci', 'has_fulltext', 'fulltext_origin', 'cited_by_count', 'citation_normalized_percentile', 'cited_by_percentile_year', 'biblio', 'is_retracted', 'is_paratext', 'primary_topic', 'topics', 'keywords', 'concepts', 'mesh', 'locations_count', 'locations', 'best_oa_location', 'sustainable_development_goals', 'grants', 'datasets', 'versions', 'referenced_works_count', 'referenced_works', 'related_works', 'abstract_inverted_index', 'cited_by_api_url', 'counts_by_year', 'updated_date', 'created_date'])
  ```

To look at a value associated with a specific key, we can add the key in square brackets (in the same way we refer to a column from a Pandas DataFrame). 

``` python
json_response['title']
```

``` output
'Library Carpentry: Software Skills Training for Library Professionals'
```

The values of some keys in our `json_response` are actually another Python dictionary! We refer to these as nested dictionaries. 

``` python
json_response['primary_location']
```

``` output
{'is_oa': True,
 'landing_page_url': 'https://doi.org/10.18352/lq.10176',
 'pdf_url': 'http://www.liberquarterly.eu/articles/10.18352/lq.10176/galley/10667/download/',
 'source': {'id': 'https://openalex.org/S2736366396',
  'display_name': 'LIBER Quarterly The Journal of the Association of European Research Libraries',
  'issn_l': '2213-056X',
  'issn': ['2213-056X', '1435-5205'],
  'is_oa': True,
  'is_in_doaj': True,
  'is_core': True,
  'host_organization': 'https://openalex.org/P4310318591',
  'host_organization_name': 'Utrecht University Library Open Access Journals (Publishing Services)',
  'host_organization_lineage': ['https://openalex.org/P4310318591'],
  'host_organization_lineage_names': ['Utrecht University Library Open Access Journals (Publishing Services)'],
  'type': 'journal'},
 'license': 'cc-by',
 'license_id': 'https://openalex.org/licenses/cc-by',
 'version': 'publishedVersion',
 'is_accepted': True,
 'is_published': True}
```

To drill down and take a closer look at these nested dictionary values, we can keep adding keys using the same square bracket notation. The title of this publication, 'LIBER Quarterly The Journal of the Association of European Research Libraries', for example, is nested under two more keys: `source` and `display_name`. To look at that value we can call:

``` python
json_response['primary_location']['source']['display_name']
```
 
``` output
'LIBER Quarterly The Journal of the Association of European Research Libraries'
```


## API call for an institution

- [The Institutions entity](https://docs.openalex.org/api-entities/institutions) represents Universities and other organisations to which authors claim affiliations. This provides a way to query the API by institution and retrieve data about the organisation.

 Works, Authors, Sources, Institutions, Topics, Publishers, Funders, and Geo. Each entity allows you to construct queries using the entity as a search field, and to explore the entity "object," which contains data related to each entity type.
 

::::::::::::::::::::::::::::::::::::: keypoints 

-  

::::::::::::::::::::::::::::::::::::::::::::::::


