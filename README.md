# A9 Observability

Small Express and MongoDB todo service instrumented with OpenTelemetry. HTTP and MongoDB spans are sent over OTLP/HTTP to Jaeger. Metrics are printed to the server console.

## Requirements

- Node.js and npm
- Docker Desktop running

## Setup (PowerShell)

```powershell
npm install
docker run -d --name a9-mongo -p 27017:27017 mongo
docker run -d --name jaeger -p 16686:16686 -p 4317:4317 -p 4318:4318 jaegertracing/jaeger:2.5.0
npm start
```

In a separate terminal:

```powershell
curl.exe http://localhost:3000/todo
curl.exe http://localhost:3000/todo/1
```

Open http://localhost:16686 and search for service `todo-service` to view traces.

## Endpoints

- `GET /todo` - list sample todos
- `GET /todo/:id` - get one todo by ID

## Notes

The application adds sample records when started; repeated starts append duplicates. Docker/Jaeger must be running before traces can be exported. The Jaeger UI displays traces, not all console metrics and application logs.
