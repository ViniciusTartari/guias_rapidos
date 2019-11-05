# WHAT IS A REST API?

Brief compilation of API and REST information.

## Summary

- [What is an API?](#What-is-an-API?)
- [What is REST?](#What-is-REST?)
- [HTTP Methods](#HTTP-Methods)
- [Endpoints](#Endpoints)
- [Authentication](#Authentication)
- [Headers](#Headers)
  - [Authentication](#Authentication)
  - [WWW-Authenticate](#WWW-Authenticate)
  - [Accept-Charset](#Accept-Charset)
  - [Content-Type](#Content-Type)
  - [Cache-Control](#Cache-Control)
- [RESTful Resources](#RESTful-Resources)
  - [Query Parameter](#Query-Parameter)
  - [Fragment Parameters](#Fragment-Parameters)
  - [Character Encoding](#Character-Encoding)
  - [Size Limits](#Size-Limits)

---

## What is an API?

- **A**pplication **P**rogram **I**nterface
- APIs are everywhere
- Contract provided by one piece of software to another
- Structured request and response

---

## What is REST?

- **Re**presentional **S**tate **T**ransfer
- **Architecture style** for designing networked applications
- Relies on a **stateless**, **client-server** protocol, almost always **HTTP**
- Treats server objects as resources that can be created or destroyed
- Can be used by virtually any programming language

---

## HTTP Methods

- **GET:** Retrieve data from a specified resource
- **POST:** Submit data to be processes to a specified resource
- **PUT:** Update a specified resource
- **DELETE:** Delete a specified resource
- **HEAD:** Same as get but does not return a body
- **OPTIONS:** Return the supported HTTP methods
- **PATCH:** Update partial resources

---

## Endpoints

Endpoints are the URI/URL where api/service can be accessed by a client application, for example:

- GET `http://url.com/api/users`
- GET `http://url.com/api/users/1` or `http://url.com/api/users/details/1`
- POST `http://url.com/api/users`
- PUT `http://url.com/api/users/1` or `http://url.com/api/users/update/1`
- DELETE `http://url.com/api/users/1` or `http://url.com/api/users/delete/1`

---

## Headers

The REST headers and parameters contain a wealth of information that can help you track down issues when you encounter them. HTTP Headers are an important part of the API request and response as they represent the meta-data associated with the API request and response. Headers carry information for:

- Request and Response Body
- Request Authorization
- Response Caching
- Response Cookies

### Authentication

Some APIs require authentication to use their services. This access can be free or paid and has credentials containing client authentication information for the requested feature.

```bash
curl -H "Authorization:token OAUTH-TOKEN" https://api.github.com

curl https://api.github.com/?access_token=OAUTH-TOKEN

curl 'https://api.github.com/users/whatever?client_id=xxxx&client_secret=yyyy'
```

### WWW-Authenticate

This is sent by the server if it needs a form of authentication before it can respond with the actual resource being requested. Often sent along with a response code of 401, which means ‘unauthorized’.

### Accept-Charset

This is a header which is set with the request and tells the server about which character sets are acceptable by the client.

### Content-Type

Indicates the media type (text/html or text/JSON) of the response sent to the client by the server, this will help the client in processing the response body correctly.

### Cache-Control

This is the cache policy defined by the server for this response, a cached response can be stored by the client and re-used till the time defined by the Cache-Control header.

---

## Parameters

In a REST request the resource is specified in the **URL** – **U**niform **R**esource **L**ocator. The **URL** is a special case of the **URI** – **U**niform **R**esource **I**dentifier – which consists of four parts:

`scheme_name:hierarchical_part?query#fragment`

---

## RESTful Resources

In any RESTful service it is very desirable to have all your resources structured by their hierarchy. These are then specified in the hierarchical part of the URL. The hierarchical parts are all **required**, and **unique**. This means that none of them can be omitted, and all of them can appear only once. Certain parts of the URL are going to be fixed (such as the server name, port, and endpoint), and certain parts are going to be parametrized. The parametrized parts are often denoted in code and in documentation by curly braces.

Consider, for example, a web service for ordering books. The data might be organized into customers, which contain orders, which in turn contain individual books. The resource URL might look like this:

`http://url/api/order_api/{customer_id}/{order_id}/{book_id}`

### Query Parameter

The query parameters are sometimes referred to as optional parameters; this is the first distinguishing feature from the hierarchical parameters: they are all optional. The second feature is that they are non-unique, meaning that you can specify any one parameter multiple times. The query parameters are separated from the hierarchical parameters by the question mark. The exact syntax of the actual parameters is not generically defined, but normally are a sequence of key-value pairs (separated by an equal sign), with the sequence separated by either a semicolon or an ampersand.

### Fragment Parameters

The fragment part of the URL, everything after a hash symbol, is information that is normally used only by the client, such as a browser, and not processed by the server. Therefore it is uninteresting when discussing REST parameters. The only interesting item is if you need to send the actual hash character as a value (instead of representing the hash control symbol) to one of the options. In that case you need to encode the URL.

### Character Encoding

Special characters are encoded in the URL, by a mechanism called “percent encoding”. In this mechanism, any character can be replaced by the percent symbol, followed by a two-digit hexadecimal value of the encoded character. If special characters (such as the hash character) need to be sent as actual data, they must be encoded. All other characters can optionally be encoded.

### Size Limits

Although the URI standard does not specify a maximum size of the URL, most clients enforce an arbitrary limit of 2000 characters. Sending data that is difficult to express in a hierarchical manner, and especially data that is larger than this 2000 character limit, should be transmitted in the body of the request. As was discussed in SOAP vs. REST the data in the body can be structured in any machine-readable format, but most often is structured as XML or JSON.

---

## Examples of APIs and documentation

[GItHub API Documentation](https://developer.github.com/v4/)

[Google APIs Explorer](https://developers.google.com/apis-explorer)

[Paypal API Documentation](https://developer.paypal.com/docs/api/overview/)
