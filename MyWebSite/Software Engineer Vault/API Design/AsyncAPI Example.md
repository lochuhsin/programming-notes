---
Created: 2023-07-17 13:56
aliases: 
card link:
  - "[[AsyncAPI]]"
---
## Description
---

The examples below shows how to define WebSocket schema for pub sub communication.

```yaml
asyncapi: '2.6.0'
info:
  title: Dataverse Websocket API
  version: '1.0.0'

servers:
  data:
    url: wss://localhost:8000
    protocol: websocket

channels:
  ws/data:
    description: data related websocket
    publish:
      message:
        payload:
          type: object
          examples:
            - type: data.grounding_dino
              uuid: asdhfaklhklahsf123471987
              data:
                - val: [1, 2, 3, 4]
                  class_name: cat
                  bbox_confidence: 0.85
                  text_confidence: 0.87
                  metrics:
                    text_confidence:
                      this: 0.1
                      is: 0.1
                      a: 0.1
                      cat: 0.87
                    bbox_confidence: 0.85
            - type: data.sam
              uuid: asdhfaklhklahsf123471987
              data:
                embedding_file_url: www.there.is.no.picture

      bindings:
        grounding_dino:
          ws:
            $ref: '#/components/schemas/grounding_dino'
        sam:
          ws:
            $ref: '#/components/schemas/sam'

  ws/user:
    description: user related websocket
    publish:
      bindings:
        notification:
          ws:
            payload:
              $ref: "#/components/schemas/notification"

      message:
        name: notification channel
        payload:
          type: object
          examples:
            - has_unread: true

components:
  schemas:
    notification:
      type: object
      required: [has_unread]
      properties:
        has_unread:
          type: boolean

    grounding_dino:
      type: object
      required: [type, data, uuid]
      properties:
        type:
          type: string
          default: data.grounding_dino

        uuid:
          type: string

        data:
          type: array
          properties:
            dino_obj:
              type: object
              properties:
                val:
                  type: array
                class_name:
                  type: string
                text_confidence:
                  type: number
                bbox_confidence:
                  type: number
                metrics:
                  type: object
                  properties:
                    text_confidence:
                      type: object
                    bbox_confidence:
                      type: number

    sam:
      type: object
      required: [type, data, uuid]
      properties:
        type:
          type: string
          default: data.sam
        uuid:
          type: string

        data:
          type: object
          properties:
            embedding_file_url:
              type: string

```