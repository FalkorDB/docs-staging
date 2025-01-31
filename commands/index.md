---
title: "Commands"
description: Commands overview
has_children: true
---

## Overview

### FalkorDB Features

FalkorDB exposes graph database functionality within Redis using the [openCypher](https://opencypher.org/) query language. Its basic commands accept openCypher queries, while additional commands are exposed for configuration or metadata retrieval.

### FalkorDB API

Command details can be retrieved by filtering for the [module](/commands/?group=graph) or for a specific command, e.g., `GRAPH.QUERY`.
The details include the syntax for the commands, where:

*   Optional arguments are enclosed in square brackets, for example `[timeout]`.
*   Additional optional arguments are indicated by an ellipsis: `...`

Most commands require a graph key name as their first argument.
