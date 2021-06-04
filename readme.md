# SSWG Collection + Generator

This repository hosts the code for generating the SSWG [Package Collection](https://github.com/apple/swift-evolution/blob/main/proposals/0291-package-collections.md),
reflecting the SSWG incubated libraries and tools also listed on https://swift.org/server#projects.

The tool uses docker to invoke the [Package Collection Generator](https://github.com/apple/swift-package-collection-generator) published by Apple,
having the input captured in `packages.json` and output as `collection.json`.

The resulting `collection.json` is the collection shared with the community.
As such it's underlying URL (https://raw.githubusercontent.com/swift-server/sswg-collection/main/collection.json) needs to stay stable.

The collection is made available to users from https://swiftserver.group/collection/sswg.json which redirects to the underlying content in this repository.

The tool is run by a daily (TBD) CI job such that changes to the package list or the package details are reflected quickly.

## Development

To invoke the tool locally use `docker-compose -f docker/docker-compose.yaml run generate`

Note `GITHUB_API_TOKEN` is used to interact with GitHub and obtain metadata about the packages.

Checkouts are cached in a `.cache` directory to speed up subsequent runs.
