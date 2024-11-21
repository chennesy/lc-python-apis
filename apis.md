---
title: "APIs & OpenAlex"
teaching: 15
exercises: 2
---

::::::::::::::::::::::::::::::::::::: objectives

- Explain some common uses for APIs (Application Programming Interfaces).
- Conduct a search for a scholarly work using the OpenAlex web interface. 
- Navigate the documentation for the OpenAlex API. 
- Identify a few key elements for making RESTful API calls via URLs.

::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is an API?
- What is OpenAlex?
- Why do organisations create APIs?

::::::::::::::::::::::::::::::::::::::::::::::::::


## What is OpenAlex?

OpenAlex is an open index of over 250 million scholarly works from around the world. It is developed by [OurResearch](https://ourresearch.org/), a nonprofit dedicated to open research. They also developed the [Unpaywall](https://unpaywall.org/) browser extension, for example.

:::::::::::::::::::::::::::::::::::::::  challenge

### Search OpenAlex

Use [OpenAlex](https://openalex.org/) to retrieve a list of all of the scholarly works from 2023 that were published by authors affiliated with a specific institution. For example, you could look for 2023 publications from University of Minnesota authors.

Tips: 

1. If you start to type the name of an institution in the search box you will see options to choose items from the database. 
2. On the search results screen, you can select the big blue "+" button to add or remove filters from your search. 
3. You can manually construct a search by Institution and Year by starting from the [Search Results page](https://openalex.org/works?page=1) and using the filter button to add each element of your query.

:::::::::::::::  solution

### Solution
You can find the 2023 works by University of Minnesota authors by creating a search where:

1. institution "is" _University of Minnesota_ and
2. year "is" _2023_.

![](fig/umn_2023.png){alt="Screenshot of the filters used to retrieve 2023 University of Minnesota publications."}
:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## What is an API?
Any user of the OpenAlex web interface can search for scholarly works and display their results in the web browser. OpenAlex also has an [API, or Application Programming Interface](https://glosario.carpentries.org/en/#api), which allows for computer programs--rather than a website user--to access contents of the database and download the content in different structured formats. The OpenAlex API provides a way for computer scripts to interact with the OpenAlex servers, and ultimately to access more information than a user of the website could manually access.

Many different websites and publishers provide APIs to their content. 

- Newspapers such as the [New York Times](https://developer.nytimes.com/apis) and the [Guardian](https://open-platform.theguardian.com/) have APIs that allow developers of other websites or apps to programmatically integrate content from their papers on their sites/apps, for example. 
- Government agencies often provide API access to their data: [data.europa.eu](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/#dataeuropaeu-apis), for example, provides a central portal for programmatic access to open data from the EU, national, regional, local and geospatial data sources. 
- Web and social media companies often offer APIs so that other websites and apps can easily republish or integrate their content: see, for example, the [TikTok](https://developers.tiktok.com/), [Google Maps](https://developers.google.com/maps/apis-by-platform), [Slack](https://api.slack.com/), and [Facebook/Meta APIs](https://developers.facebook.com/docs/).

One reason publishers create APIs is to allow them to clearly define limits on how their content can be re-used. The New York Times API, for example, does not allow access to the full-text from their articles via the API, and only accepts 500 requests per day and 5 requests per minute (via [the FAQ](https://developer.nytimes.com/faq)). 

### API calls

A "call" to an API is the action of programmatically requesting data from an external server, following the API's defined protocols. That sounds very complex, but in fact many API calls use URLs to query databases, which you can view in your web browser. 

The OpenAlex API provides an "institution" search, for example, that consists of a URL that begins with ```https://api.openalex.org/institutions?search=``` and is followed by keywords from the name of a university or college. To make an API call for the University of Tokyo, for example, you could direct your browser to: [https://api.openalex.org/institutions?search=university+of+tokyo](https://api.openalex.org/institutions?search=university+of+tokyo). The API results show a structured response that the web browser doesn't display in a user-friendly way, but we'll explore different ways to parse, clean, analyze, and visualise that data throughout this lesson.   

Most web APIs that use URLs in this way are known as RESTful (Representational State Transfer) APIs. RESTful APIs rely on constructing URL strings to get the responses you want. 

- [URLs (Uniform Resource Locators)](https://glosario.carpentries.org/en/#url) are strings of characters that point to a data resource online. When we use a web browser, URLs usually point to markup language files such as HTML, which are rendered in your web browser so that they're easy for you to interact with. When we use a URL to make an API call, however, the response is often in a format that a web browser doesn't display for human consumption.
- [HTTP (Hypertext Transfer Protocol) requests](https://glosario.carpentries.org/en/#http_request) provide for different methods (GET, HEAD, POST, etc.) to interact with online data. We'll exclusively be making HTTP GET requests to "get" data from the RESTful OpenAlex API. Other HTTP methods, such as DELETE, can be used by developers who have the permissions to modify the database itself via HTTP requests.

## OpenAlex API

[The OpenAlex technical documentation site](https://docs.openalex.org/) provides an [overview of the API](https://docs.openalex.org/how-to-use-the-api/api-overview), including example HTTP Request URLs you can use for making calls to the API. API documentation is an essential tool to help you learn to query the API. API documentation also often spells out for you different requirements for using the API (such as creating a free or paid account) and technical limitations about how often and how much data you can access.  

:::::::::::::::::::::::::::::::::::::::  challenge

### OpenAlex Documentation

Use the [OpenAlex API documentation](https://docs.openalex.org/) to find out:

- Do you need an account to use the API?
- Is it free to use the API?
- How many API calls can you make per day and per second?

:::::::::::::::  solution

### Solution
The [Rate limits and authentication page](https://docs.openalex.org/how-to-use-the-api/rate-limits-and-authentication) notes: 

- The OpenAlex API is free and requires no authentication or account to use. You can add your email address to your API calls to get in the "polite pool", however, which gives you access to faster API response times.
- For free accounts, the rate limits are: 100,000 calls each day and 10 requests per second. 
- It's also possible to subscribe to a Premium plan and raise the API limits. And the docs note: "if you're an academic researcher we can likely [raise your API limits] for free."


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

- OpenAlex is an open index of scholarly works, authors, institutions, and more. 

::::::::::::::::::::::::::::::::::::::::::::::::


