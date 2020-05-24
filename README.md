# Response2Schema

A quick 'n easy way to generate your OpenAPI spec based on a JSON object. Useful for bootstrapping your component
 schemas. This is intended to be a starting point for writing your specification, as the tool cannot infer types such
  as enum, oneOf, maximum/minimum, and so on. It also does not support generating endpoints or error responses. All
   it does is take your JSON object and turns it into an OpenAPI schema object, along with a simply example spec that
    you can expand on.
    
Supports generating an OpenAPI spec in `JSON` or `yaml`.

# Installation

`composer require --dev dsuurlant/response2schema`

# Usage

Just point Response2Schema to your input json file, and tell it where to put the output OpenAPI spec.

It will automatically format it to json or yaml based on the extension of the output path.

`./vendor/bin/response2schema response.json openapi.yaml`

# Example

Given a very simple response:

```json
{
    "id": 1,  
    "name": "Example Response"
}
```

Response2Schema generates the following spec:

```yaml
openapi: 3.0.0
info:
  title: 'OpenAPI specification automatically generated by Response2Schema.'
  description: 'Please adapt this specification to your own needs.'
  version: 1.0.0
paths:
  /resource:
    get:
      description: 'Description of the endpoint'
      operationId: getResource
      responses:
        '200':
          description: 'Description of this response.'
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Resource'
components:
  schemas:
    Resource:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
```

It will always generate the example endpoint and a schema named 'Resource'.

The best way to use this tool is to take this as a starting point, or copy-paste the schema definition to your own
 OpenAPI spec.
 
# Credits

Built and maintained by [Daniëlle Suurlant](https://github.com/dsuurlant).

Relies heavily on the awesome PHP OpenAPI library [cebe/php-openapi](https://github.com/cebe/php-openapi).
