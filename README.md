# workflows

Reusable workflows for CI/CD

### Subgraph Check

Checks a subgraph for breaking changes

```
jobs:
  subgraph_check:
    uses: sibipro/workflows/.github/workflows/subgraph-check.yml@v1
    with:
      graph: my-federated-graph

      // The path to a single graphql schema file
      schema_path: ./schema.graphql

      // Optionally pass a command to compile multiple `.graphql` files into a single schema file
      schema_build_cmd: cat ./graphql/*.graphql > schema.graphql

      // The URL that your gateway uses to communicate with the subgraph in a managed federation architecture.
      routing_url: http://my-subgraph.com
    secrets:
      APOLLO_KEY: ${{ secrets.APOLLO_KEY }}
```
