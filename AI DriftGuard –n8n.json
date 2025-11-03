{
  "name": "AI DriftGuard – Facets Prototype",
  "nodes": [
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.3,
      "position": [
        -1072,
        128
      ],
      "id": "5b43b571-b9cf-44b2-b84f-79c13d0db49b",
      "name": "When chat message received",
      "webhookId": "9e69446e-6b6b-484d-9a8d-3a18b5a29790"
    },
    {
      "parameters": {
        "url": "https://mocki.io/v1/85998f5a-a701-46ef-bdd1-010e3fbfd850",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -864,
        128
      ],
      "id": "1b54953d-7a7d-494b-ac51-5d5367088e17",
      "name": "Fetch Dev Config"
    },
    {
      "parameters": {
        "url": "https://mocki.io/v1/42426a5a-c6a9-4aa7-915b-06612769ac6e",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -656,
        128
      ],
      "id": "664c68e6-609f-423a-b57d-20ffb895df19",
      "name": "Fetch Prod Config"
    },
    {
      "parameters": {
        "jsCode": "// Get JSON data from previous nodes\nconst dev = $items(\"Fetch Dev Config\")[0].json;\nconst prod = $items(\"Fetch Prod Config\")[0].json;\n\nconst drift = [];\n\nfor (const key in dev) {\n  if (dev[key] !== prod[key]) {\n    drift.push({\n      parameter: key,\n      dev_value: dev[key],\n      prod_value: prod[key]\n    });\n  }\n}\n\nreturn [{ json: { drift }}];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -448,
        128
      ],
      "id": "257687cb-7a1a-45e7-92c4-7e1575538e67",
      "name": "Code in JavaScript"
    },
    {
      "parameters": {
        "mergeByFields": {
          "values": [
            {
              "field1": "Fetch Dev Config",
              "field2": "Fetch Prod Config"
            }
          ]
        },
        "fuzzyCompare": true,
        "options": {}
      },
      "type": "n8n-nodes-base.compareDatasets",
      "typeVersion": 2.3,
      "position": [
        -208,
        240
      ],
      "id": "a219dfd3-8be3-4790-bd21-0a1ac114f3c8",
      "name": "Compare Datasets"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=You are an AI drift analyzer.\nAnalyze the configuration drift data between Dev and Prod environments below.\nSummarize the differences in a concise and clear way.\n\nDrift Data:\n{{ JSON.stringify($json, null, 2) }}\n",
        "hasOutputParser": true,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 2.2,
      "position": [
        272,
        240
      ],
      "id": "34751b50-edea-482e-b07d-993d0d85dfe7",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "value": "gpt-3.5-turbo",
          "mode": "list",
          "cachedResultName": "gpt-3.5-turbo"
        },
        "options": {
          "maxTokens": 512,
          "temperature": 0.7
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.2,
      "position": [
        224,
        512
      ],
      "id": "9c689eb6-29d8-4df8-b002-b690d357eb13",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "bbs5UEcxXicEA9m9",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "jsonSchemaExample": "{\n  \"summary\": \"string\",\n  \"differences\": [\n    {\n      \"parameter\": \"string\",\n      \"dev_value\": \"string\",\n      \"prod_value\": \"string\"\n    }\n  ]\n}\n"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.3,
      "position": [
        448,
        512
      ],
      "id": "be9e8576-acb0-4d1c-a7cc-fbdb65a3e59c",
      "name": "Structured Output Parser"
    },
    {
      "parameters": {
        "operation": "append",
        "documentId": {
          "__rl": true,
          "value": "1PA8uUkURwNhLavd1paXBcs7MuayGiIVKgktq49WrZQ8",
          "mode": "list",
          "cachedResultName": "AI DriftGuard – Facets Prototype",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1PA8uUkURwNhLavd1paXBcs7MuayGiIVKgktq49WrZQ8/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1PA8uUkURwNhLavd1paXBcs7MuayGiIVKgktq49WrZQ8/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "timestamp ": "={{$json.timestamp}}",
            "drift_type ": "={{$json.drift_type\n}}",
            "difference_summary ": "={{$json.difference_summary}}",
            "status ": "={{$json.status}}",
            "ai_comment": "={{$json.ai_comment}}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "timestamp ",
              "displayName": "timestamp ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "drift_type ",
              "displayName": "drift_type ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "difference_summary ",
              "displayName": "difference_summary ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "status ",
              "displayName": "status ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            },
            {
              "id": "ai_comment",
              "displayName": "ai_comment",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        800,
        208
      ],
      "id": "3edd9ea2-6bcf-4689-aa2d-71c935ae4454",
      "name": "Append row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "yDvWqa4sN8hBHgeo",
          "name": "Google Sheets account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "When chat message received": {
      "main": [
        [
          {
            "node": "Fetch Dev Config",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Fetch Dev Config": {
      "main": [
        [
          {
            "node": "Fetch Prod Config",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Fetch Prod Config": {
      "main": [
        [
          {
            "node": "Code in JavaScript",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code in JavaScript": {
      "main": [
        [
          {
            "node": "Compare Datasets",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Compare Datasets": {
      "main": [
        [],
        [],
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Structured Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "AI Agent",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "Append row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "50bf4c2c-96bb-40a2-9708-098dcf8ba9b7",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "c2b50a24f3da24f3dd79eac3e6b8ff158a6f0cb048a19e08f1bf57eb3025053d"
  },
  "id": "eN6WQ8quPS59YQNA",
  "tags": []
}
