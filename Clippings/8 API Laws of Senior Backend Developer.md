---
title: "8 API Laws of Senior Backend Developer"
source: "https://www.youtube.com/watch?v=-40xErgJIBg"
author:
  - "[[Cloud X Berry]]"
published: 2026-09-06
created: 2026-10-24
description: "In this video, Cloud X Berry explains REST API design in a simple and beginner-friendly way.You open an API you have never used before, and without reading a line of documentation you already know t"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=-40xErgJIBg)

In this video, Cloud X Berry explains REST API design in a simple and beginner-friendly way.  
  
You open an API you have never used before, and without reading a line of documentation you already know that GET /v2/orders/order\_id returns one order, that DELETE on the same URL removes it, and that a 404 means it was never there. None of that is luck. It is eight patterns the API followed, and they are the difference between an API people can guess and one they have to keep looking up.  
  
CHAPTERS  
  
  
0:08 1: Design around resources, not actions  
1:00 2: Make URLs predictable  
1:47 3: Use HTTP methods for their purpose  
3:04 4: Make status codes useful  
4:26 5: Keep error responses consistent  
5:10 6: Not everything belongs in the path  
6:03 7: Treat API changes carefully  
7:11 8: Keep formats consistent  
8:51 Recap  
  
WHO THIS IS FOR  
Developers who have shipped a few endpoints and want a set of rules they can defend in review, backend engineers inheriting an API that everyone on the team has to keep looking up, and anyone interviewing for a role where API design or system design comes up.  
  
#restapi #apidesign #backend #systemdesign #webdevelopment

## Transcript

**0:00** · Let's look at eight REST API patterns that can make your APIs easier to understand, easier to integrate, and easier to maintain. Number one, design around resources, not actions. Here's a common API design mistake. You see endpoints like get users, create order, and delete product. At first, these seem perfectly understandable, but the URL is now describing the action, while HTTP is already designed to describe the action.

### 1: Design around resources, not actions

**0:28** · A cleaner design is to use users, orders, and products as resources and let get, post, and delete describe what you're doing with them. This becomes especially useful as the API grows because the same resource can support multiple operations without inventing a different URL for every action. For example, an order can be retrieved, replaced, or deleted using the appropriate HTTP method. The important idea is simple. Let the URL identify the resource and let the HTTP method describe the operation.

**0:59** · Number two, make your URLs predictable.

### 2: Make URLs predictable

**1:03** · Here's another thing that looks small but makes a huge difference. Consistency in resource naming. Suppose one part of your API uses user, another uses customers, and another uses customer profiles. The individual endpoints might all work, but now every developer has to remember the naming rules. A better API follows a predictable structure.

**1:25** · Collections use consistent resource names such as users, orders, and products. And a specific resource can then be accessed using its identifier.

**1:33** · For multi-word resources, choose one convention and use it everywhere. The exact convention matters less than consistency because a developer shouldn't have to guess how your API is structured. A predictable API needs fewer instructions.

### 3: Use HTTP methods for their purpose

**1:47** · Number three, use HTTP methods for their actual purpose. Let's say you want to update a user. One API uses post, another uses put, another uses patch.

**1:59** · All three might technically work, but now the client has to understand your custom rules instead of relying on standard HTTP semantics. Get should retrieve data without changing the resource.

**2:12** · Post is commonly used to create a new resource or trigger processing that doesn't fit a straightforward resource update.

**2:18** · Put is generally used when you're replacing the representation of a resource.

**2:23** · Patch is for partial updates. And delete removes a resource.

**2:27** · There's also an important concept here.

**2:29** · Idempotency.

**2:30** · If you send the same get request five times, you should get the same kind of effect as sending it once.

**2:36** · The same general idea applies to put and delete. You can send the request again without repeatedly creating new effects.

**2:43** · Post is different. Sending the same create request twice may create two resources.

**2:48** · This matters because networks fail, clients retry, and timeouts happen. Your API should behave predictably when requests are repeated. So, don't choose HTTP methods just because they make the endpoint work. Choose them according to their intended semantics. Number four, make status codes useful.

### 4: Make status codes useful

**3:07** · Here's an API response that causes problems.

**3:10** · You return 200 OK, but the response body says that the operation failed because the product wasn't found. The HTTP response says success, while the body says failure. Now, the client has to inspect two different places to understand what happened. That's unnecessary. Use HTTP status codes to communicate the high-level result. A successful read might return 200. A successfully created resource can return 201.

**3:38** · An accepted request that will finish asynchronously can return 202.

**3:42** · A successful operation without a response body can return 204.

**3:47** · And errors should communicate what actually happened. You can use 400 for an invalid request, 401 when authentication is missing or invalid, 403 when the client is authenticated but doesn't have permission, 404 when the requested resource doesn't exist, 409 when the request conflicts with the current state, 422 when the request fails business validation, and 429 when the client is sending too many requests.

**4:13** · The important thing isn't memorizing every status code. It's making the response understandable without inventing your own error protocol on top of HTTP.

**4:23** · Use the status code to tell the client what happened.

### 5: Keep error responses consistent

**4:26** · Number five, keep errors consistent.

**4:29** · Status codes tell you the category of the failure, but the client often needs more information. Compare an error that simply says something went wrong with a structured response that provides an error code, a useful message, and the status.

**4:41** · The second response is much easier for both humans and software to work with.

**4:46** · The client can display the message, the application can react to the error code, and developers can investigate the problem. For validation failures, the API can also return exactly which fields need attention instead of simply saying invalid request. The exact format can vary between systems.

**5:03** · The important thing is that errors should be structured and predictable.

**5:07** · Your API shouldn't make clients guess what went wrong. Number six, don't put everything into the URL path. Here's another common pattern. You start with a products endpoint, then you add a category to the path, then stock status, then price, then search, then sorting.

### 6: Not everything belongs in the path

**5:24** · Eventually, the URL starts becoming difficult to manage.

**5:27** · For filtering and optional criteria, query parameters are usually a better fit. The path identifies the resource, while the query parameters refine the result. But don't use query parameters to invent actions.

**5:40** · A request that uses a get operation but adds something like an action equals delete parameter is confusing because the HTTP method in the URL no longer clearly communicate what's happening.

**5:53** · Keep the responsibility clear.

**5:55** · Paths identify resources.

**5:57** · Query parameters refine them. HTTP methods describe the operation.

### 7: Treat API changes carefully

**6:03** · Number seven, treat API changes carefully.

**6:06** · APIs don't stay unchanged forever.

**6:09** · A response that looks perfect today might need to change 6 months from now.

**6:13** · Maybe you need to add new fields.

**6:15** · Maybe the response structure needs to change.

**6:18** · Maybe an existing field has the wrong meaning.

**6:21** · The dangerous part is making a breaking change without thinking about existing clients.

**6:26** · Suppose an earlier version returns a simple price field. And later, you want to replace it with a richer pricing structure.

**6:33** · That isn't just another field. The structure has changed, and existing clients may break. So, first ask whether the change actually needs a new version.

**6:42** · Adding a non-required field usually doesn't require breaking existing clients.

**6:47** · Changing or removing existing behavior might. When you do need versioning, make the strategy obvious and consistent. You might use a version in the URL, a request header, or another established mechanism. The specific strategy matters less than using one predictable approach and giving consumers a path to migrate.

**7:06** · Good API evolution means existing clients don't become collateral damage.

### 8: Keep formats consistent

**7:11** · Number eight, keep request and response formats consistent.

**7:15** · Here's something developers underestimate. Imagine one endpoint returns created\_at, another returns created\_at, and another returns created\_at.

**7:25** · All three are valid, but now every client has to remember which convention applies to which endpoint. The same problem happens with dates, pagination, error responses, property names, and response structures. Pick conventions and stick to them. For example, use JSON consistently, choose one naming convention for JSON properties, standardize error responses, and make pagination and filtering work in a predictable way. The goal is not to create a giant API rulebook. The goal is to make the next endpoint look familiar.

**7:57** · When a developer learns how one endpoint works, they should be able to make reasonable assumptions about the others.

**8:02** · Consistency is one of the best features an API can have. And there's one more thing worth remembering. A lot of developers focus on whether an API technically follows REST. That's useful, but it's not the most important goal.

**8:16** · Your API doesn't become good simply because it uses GET, POST, PUT, and DELETE. A good API is one that clients can understand without constantly checking documentation.

**8:26** · The resource names make sense. The methods behave predictably. The status codes mean something. Errors have a consistent structure. Filters work the same way across endpoints, and changes don't unexpectedly break existing consumers. That's what makes an API pleasant to work with. So when you're designing your next REST API, don't start by creating endpoints one at a time. Start by defining the patterns.

### Recap

**8:51** · How will you name resources? How will you represent collections? How will filtering work? Which HTTP methods will you use? How will errors look? How will status codes be handled? How will the API evolve? And what conventions should every endpoint follow? Because once those rules are clear, building the API becomes much easier. A good REST API doesn't just return the right data. It makes the right way to use it obvious.