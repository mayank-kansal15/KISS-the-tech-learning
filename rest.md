# WHAT IS REST?
REST stands for Representational State Transfer. It’s a software architectural style for implementing web services. Web services implemented using the REST architectural style are known as the RESTful Web services.

In REST we transfer representation of a resource in a particular state at a point in time, that's why it is called REST. 
For example: GET /v1/articles/123, transfer article 123 representation in JSON format in the state when API is hit.

REST use HTTP as a communication protocol, HTTP is a stateless protocol so should be REST. It means two REST APIs should be treated completely independent on server, both APIs should be authenticated and authorized, don't store anything from the first API call in server memory to be used by further API calls.

RESTful APIs are written for consumers. The name and structure of URIs should convey meaning to those consumers. Although your internal data models may map neatly to resources, it isn't necessarily a one-to-one mapping. The key here is to not leak irrelevant implementation details out to your API! Your API resources need to make sense from the perspective of the API consumer. Design for your clients, not for your data.

Each resource in a service suite will have at least one URI identifying it. REST URIs should follow a predictable, hierarchical structure to enhance understandability. Predictable in the sense that they're consistent, hierarchical in the sense that data has structure—relationships.

## Example of REST APIs and how to read them.
- POST /v1/users, read as, create a user in the user collection.
- GET /v1/users, read as, get users from the user collection.
- GET /v1/users/123, read as, get the user 123 from the user collection.
- PUT /v1/users/123, read as, override the user 123 in the user collection.
- PATCH /v1/users/123, read as, modify the user 123 in the user collection.
- DELETE /v1/users/123 read as, delete the user 123 from the user collection.


# Resources in REST:
In REST we transfer resource representation, any information or functionality which a REST API server offers can be treated as a resource.

## How to name resources?
- Resource name should be noun not verb.
- Use lowercase to write resource name.
- In most of the cases use plural for resource name, because server offer resource collection, to identify a particular from the collection use ID. Example, /users, /orders, /posts, etc.
- For multi words resource name, use snake_case(separate words with underscore). snake_case is more readable than spinal-case(separate words with hyphen) and camelCase.
- Use singular resource name only when resource actually is a singleton. Example if a single configuration exist for a customer then /customers/{customer_id}/configuration.

## Resource identifier:
- For a particular resource ID, avoid using database sequence number. A UUID, Mongo Object ID, etc, is preferred.
- APIs specific to users or customer, where ID comes from token, etc, use mine in the path to convey that the path is related to a particular resource. Example: GET /users/mine/bank_accounts, here user id should come from JWT not from path. But in case of a admin API to list user bank account path will be like /admin/users/{user_id}/bank_accounts.

## Sub or nested resources:
Sub-resources represent a relationship from one resource to another. If cardinality is 1:1, then no additional information is required, otherwise, the sub-resource should provide a sub-resource ID for unique identification.

If a sub-resource can be treated independently in the system and offer a whole set of functionality then it should have it's own path instead of a sub-resource to parent. Example instead of /customers/mine/orders have /orders in the service.

If a sub resource can't exist without parent or doesn't make more sense without parent or doesn't offer functionality of it's own then keep it as a sub resource under parent. Example: /posts/{post_id}/comments, posts/{post_id}/comments/{comment_id}, /users/mine/bank_accounts(when we don't want to treat bank accounts independently in service and no functionality on bank accounts).

Avoid too much levels in path, no more than two levels of sub resources, if we see more than two levels means a sub resource is offering good number of functionalists and can be treated independently.







