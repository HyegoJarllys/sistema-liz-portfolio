**Quickstart — Safe Demonstration**

This quickstart provides a sanitized and non-production demonstration of how the Sistema LIZ conversational API behaves.

The examples below are illustrative and do not connect to a live environment.
They exist solely to demonstrate the API contract, request flow, and response structure.

**Prerequisites**

No cloud account or credentials are required.

To follow the examples, you only need:

Basic familiarity with HTTP APIs

Any HTTP client (cURL, Postman, or similar)

**API Endpoint (Placeholder)**

POST https://<backend-host>/chat

The actual production endpoint is intentionally omitted.

**Request Format**

Headers
Content-Type: application/json

***Body Parameters**
Field	    Type	    Required	    Description
message	    string	    Yes	        User question or request
user_id	    string	    Yes	        Anonymous or hashed identifier

**Example Request**
{
  "message": "How can I submit a formal service request?",
  "user_id": "anonymous_user_001"
}
**Response Format**

Success Response (200)
{
  "response": "According to the official service guidelines, formal requests must be submitted through the institutional portal.",
  "sources": [
    "Public Service Manual v2.1"
  ]
}

**Response Fields**
Field	        Type	                  Description
response	    string	            Generated answer grounded in documents
sources	        array of string	    Documents used to generate the response

**Error Handling**

The API follows standard HTTP semantics.

**Common Error Codes**
Status	    Meaning 	    Description
400	    Bad Request	        Invalid or missing fields
429	    Too Many Requests	Rate limit exceeded
500	    Internal Error  	Unexpected server error
503	    Service Unavailable	Temporary dependency failure

**Example Error Response**
{
  "error": "Service temporarily unavailable. Please retry later."
}

**Analytics Behavior (Implicit)**

From the client’s perspective, analytics are invisible.

Internally:

Interaction metadata is published after the response is returned

Analytics processing is fully asynchronous

Failures in analytics never affect the user response

This design guarantees predictable latency and high availability.

**What This Quickstart Does NOT Show**

To keep this repository safe and vendor-neutral, the following are intentionally excluded:

Authentication mechanisms

Real endpoints or credentials

Prompt configuration

Document ingestion or indexing logic

Internal classification rules

These elements are discussed conceptually in the architecture documentation.

**Next Steps**

For architectural decisions and trade-offs, see:
docs/02-architecture.md

For API details and constraints, see:
docs/03-api.md

For analytics and dashboards, see:
docs/04-analytics.md