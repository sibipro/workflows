# workflows

Reusable workflows for CI/CD

## Subgraph Check

Checks a subgraph for breaking changes

```yml
jobs:
  subgraph_check:
    uses: sibipro/workflows/.github/workflows/subgraph-check.yml@v1.3
    with:
      graph: my-federated-graph
      name: my-subgraph
      schema_path: ./schema.graphql

      # Optionally pass the graph variant to check against (default: current)
      variant: current

      # Optionally pass a command to compile multiple `.graphql` files into a single schema file
      schema_build_cmd: cat ./graphql/*.graphql > schema.graphql
    secrets:
      APOLLO_KEY: ${{ secrets.APOLLO_KEY }}
```

## Subgraph Publish

Publishes a subgraph schema from a file

```yml
jobs:
  subgraph_publish:
    uses: sibipro/workflows/.github/workflows/subgraph-publish.yml@v1.3
    with:
      graph: my-federated-graph
      name: my-subgraph
      schema_path: ./schema.graphql

      # Optionally pass the graph variant to check against (default: current)
      variant: current

      # Optionally pass a command to compile multiple `.graphql` files into a single schema file
      schema_build_cmd: cat ./graphql/*.graphql > schema.graphql
    secrets:
      APOLLO_KEY: ${{ secrets.APOLLO_KEY }}
```

## Subgraph Publish via Introspection

Publishes a subgraph schema by introspecting the running subgraph.

```yml
jobs:
  subgraph_publish:
    name: Run Subgraph Introspect and Publish
    uses: sibipro/workflows/.github/workflows/subgraph-publish-via-introspection.yml@v1.3
    with:
      graph: my-federated-graph
      name: my-subgraph-name
      introspection_url: http://my-subgraph.com

      # Optionally pass the graph variant to check against (default: current)
      variant: current
    secrets:
      APOLLO_KEY: ${{ secrets.APOLLO_STUDIO_KEY }}
```

## Deploy image to ECS service

Updates a services's task definition with a new image and redeploys that service

```yml
jobs:
  deploy:
    name: Deploy
    uses: sibipro/workflows/.github/workflows/deploy-image-to-ecs-service.yml@v1.3
    with:
      task_definition: task-definition.json
      container_name: my-container-name
      image: ghcr.io/my-image
      service: my-service-name
      cluster: my-cluster-name
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
