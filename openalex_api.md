---
title: "The OpenAlex API"
teaching: 45
exercises: 2
---

::::::::::::::::::::::::::::::::::::: objectives

- 

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- 

::::::::::::::::::::::::::::::::::::::::::::::::::


## API calls for scholarly works

The OpenAlex API is structured around a series of [entities](https://docs.openalex.org/api-entities/entities-overview): Works, Authors, Sources, Institutions, Topics, Publishers, Funders, and Geo. Each entity allows you to construct queries using the entity as a search field, and to explore the entity "object," which contains data related to each entity type. 

- [The Works entity](https://docs.openalex.org/api-entities/works), for example, represents scholarly documents like journal articles, books, datasets, and theses that are indexed in OpenAlex. You can create queries to [access a single work](https://docs.openalex.org/api-entities/works/get-a-single-work) or [lists of works](https://docs.openalex.org/api-entities/works/get-lists-of-works). The results of those queries will pull down [Work objects](https://docs.openalex.org/api-entities/works/work-object) that contain structured data related to the scholarly work.
- [The Institutions entity](https://docs.openalex.org/api-entities/institutions) represents Universities and other organisations to which authors claim affiliations. This provides a way to query the API by institution and retrieve data about the organisation.

::::::::::::::::::::::::::::::::::::: keypoints 

-  

::::::::::::::::::::::::::::::::::::::::::::::::


