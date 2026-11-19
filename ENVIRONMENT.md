<img width="1280" height="200" alt="Github-Banner_spot" src="https://github.com/user-attachments/assets/bec5a984-2f1f-44e7-b50d-cc6354d823cd" />

# 🧾 Environment Matrix

> Overview of services, ports, and key environment variables across the SPOT stack.

## Services (from `docker-compose.yml`)

| Service | External Port → Internal | Internal URL | Notes |
|---|---|---|---|
| `osmquery` | `3000 → 5000` | `http://osmquery:5000` | OSM Query API (PostGIS-backed). |
| `central_nlp` | `4000 → 8080` | `http://central_nlp:8080` | Central NLP orchestrator (LLM + tag search). |
| `chat_api` | `8000 → 8000` | `http://chat_api:8000` | Chat API: builds SPOT queries by conversation (any OpenAI-compatible LLM). |
| `osmtagsearch` | `5000 → 8080` | `http://osmtagsearch:8080` | Tag search API; uses Elasticsearch. |
| `elasticsearch` | `9200 → 9200` | `http://elasticsearch:9200` | Search backend for tag bundles. |

## Module Env Variables (by submodule)

### Central NLP API
- Runtime/OSM: `DATABASE_NAME`, `TABLE_VIEW`, `DATABASE_USER`, `DATABASE_PASSWORD`, `DATABASE_HOST`, `DATABASE_PORT`, `MAX_AREA`, `JWT_SECRET`, `TIMEOUT`
- Tag Search: `OSM_KG`, `SEARCH_ENGINE_HOST`, `SEARCH_ENGINE_INDEX`, `SENT_TRANSFORMER`, `MANUAL_MAPPING`, `SEARCH_CONFIDENCE`, `COLOR_MAPPING`
- LLM: `T5_ENDPOINT`, `CHATGPT_ENDPOINT`, `HF_LLAMA_ENDPOINT_PROD`, `HF_LLAMA_ENDPOINT_DEV`, `HF_ACCESS_TOKEN`, `PROMPT_FILE`, `PROMPT_FILE_DEV`, `SEARCH_ENDPOINT`, `COLOR_BUNDLE_SEARCH`
- Persistence: `MONGO_URI`, `MONGO_DB_NAME`, `MONGO_COLLECTION_NAME`

### Chat API
- LLM: `LLM_API_KEY`, `LLM_BASE_URL`, `LLM_MODEL`, `LLM_MODELS`, `LLM_TEMPERATURE`, `LLM_REASONING_EFFORT`, `LLM_MAX_TOOL_ROUNDS`, `LLM_TIMEOUT`, `LLM_TURN_TIMEOUT`
- SPOT: `SPOT_TAG_SEARCH_URL`, `SPOT_MAX_ENTITIES`, `SPOT_MAX_PROPERTIES`
- Server: `SPOT_API_KEY`, `SPOT_CORS_ORIGINS`, `SPOT_RATE_LIMIT`, `SPOT_DEBUG`

### OSM Query API
- DB: `DATABASE_NAME`, `TABLE_VIEW`, `DATABASE_USER`, `DATABASE_PASSWORD`, `DATABASE_HOST`, `DATABASE_PORT`
- Security: `JWT_SECRET`
- Server: `PORT`

### OSM Tag Search API
- ES: `ELASTICSEARCH_URL`, `ELASTICSEARCH_INDEX`, `SENT_TRANSFORMER`
- Optional: `OSM_KG`, `MANUAL_MAPPING`, `COLOR_MAPPING`
- Server: `PORT`

### Datageneration
- Providers: `OPENAI_API_KEY`, `OPENAI_ORG` (optional), `LLM_API_KEY`

### Unsloth Training
- Providers: `HF_TOKEN`