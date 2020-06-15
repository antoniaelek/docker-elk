# Elastic Stack

## Requirements

- [Docker](https://www.docker.com/community-edition#/download)
- [Docker Compose](https://docs.docker.com/compose/install)

## Usage

### Bringing up Elastic Stack

Start the stack using `docker-compose`:

```posh
PS> cd .\elastic-stack\
PS> docker-compose up
```

If this is the first time the stack is started, you'll have to create a Logstash index pattern. Give the stack some time to initialize and then run the following commands in PowerShell:

```posh
$Headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
$Headers.Add("Content-Type", "application/json")
$Headers.Add("kbn-version", "6.8.10")
Invoke-RestMethod "http://localhost:5601/api/saved_objects/index-pattern" `
      -Method Post `
      -Headers $Headers `
      -Body '{"attributes":{"title":"logstash-*","timeFieldName":"Timestamp"}}'
```

### Publishing log events using Serilog

Publishing log events to Logstash using Serilog Http Sink to [http://localhost:31311](http://localhost:31311).

### Using Kibana to render the log events

Access the Kibana web UI by hitting [http://localhost:5601](http://localhost:5601) with a web browser.

## Credit

The `elastic-stack` directory is a cloned from [serilog-sinks-http-sample-elastic-stack](https://github.com/FantasticFiasco/serilog-sinks-http-sample-elastic-stack).
