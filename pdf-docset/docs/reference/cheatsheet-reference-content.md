# Reference content cheat sheet

Being a collection of guidance assembled throughout the migration of API documentation from ACOM to [docs.microsoft.com](http://docs.microsoft.com).

## Reference repos

The following GitHub repositories contain API reference content, some of which content developers edit directly (e.g. [overwrites](overwrite-troubleshooting.md) and [ref conceptual](#definitions) content).

| GitHub repository | Description |
| ----------------- | ----------- |
| [azure-docs-rest-apis](https://github.com/Azure/azure-docs-rest-apis) | Generated and hand-authored (overwrites & ref conceptual) content for REST APIs |
| [azure-docs-sdk-dotnet](https://github.com/Azure/azure-docs-sdk-dotnet) |Generated and hand-authored (overwrites & ref conceptual) content for .NET |
| [azure-docs-sdk-java](https://github.com/Azure/azure-docs-sdk-java) | Generated and hand-authored (overwrites & ref conceptual) content for Java |
| [azure-rest-api-specs](https://github.com/Azure/azure-rest-api-specs) | Source Swagger specs (\*.json); maintained by partner teams. |

## Reference repo layout

| Directory | Contents | Editable by/contact | Notes/intended usage |
| --------- | -------- | -------------------- | -------------------- |
| breadcrumb | toc.yml | Brady Gaster (bradyg) | Defines the breadcrumbing at top-left above the "Filter" box. |
| docs-ref-autogen   | generated API reference (\*.json) | continuous integration (generated--**do not manually edit**) | You can [link](#linking) to these, but **do not edit** them. These are generated by continous integration (CI) when new source is merged into *master* in one of the [reference repos](#reference-repos).
| docs-ref-conceptual | index.md, toc.md, ref conceptual (*.md) | content devs | Index (landing), ToC, and [ref conceptual topics](#definitions) for individual service APIs. |
| docs-ref-overwrite   | overwrite files (*.md) | content devs | Files containing the [overwrites](https://dotnet.github.io/docfx/tutorial/intro_overwrite_files.html) for the generated REST and managed reference content. |
| scripts | CI scripts | Jessie Huang (jehuan) | Scripts used by continuous integration (CI). |
| .| index.md | Bryan Lamos (bryanla) | All-up index (landing page) for [Azure REST API](https://docs.microsoft.com/rest/api/index) |

## Linking

To link from [ref conceptual](#definitions) to content within the same repo (such as specific REST operations, or other ref conceptual topics), use either of the following two formats:

* `[text](../../docs-ref-autogen/<service>/<file>.json#<anchor>`
* `[text](~/docs-ref-autogen/<service>/<file>.json#<anchor>`

Examples:
* `[Resource group operations](../../docs-ref-autogen/resources/resourcegroups.json)`
* `[Create a resource group](../../docs-ref-autogen/resources/resourcegroups.json#ResourceGroups_CreateOrUpdate)`
* `[Resource group operations](~/docs-ref-autogen/resources/resourcegroups.json)`
* `[Create a resource group](~/docs-ref-autogen/resources/resourcegroups.json#ResourceGroups_CreateOrUpdate)`

To link to the top-level node of a REST API, replace `docs-ref-autogen` with `docs-ref-conceptual`.

Example:
* `[Azure Search Management REST](~/docs-ref-conceptual/searchmanagement/index.md)`

To link to a service landing page in azure-docs-pr, use the following syntax. The slash afterward is required. This will load, by default, the 'index.md' file residing in that directory.

Example:
* `/azure/service-directory/`

## Metadata

Each topic that you place in your service's directory in [/docs-ref-conceptual](https://github.com/Azure/azure-docs-rest-apis/tree/master/docs-ref-conceptual) needs a metadata section at the top. Include the the triple-hyphens (`---`) before/after the fields.

```yaml
---
ms.assetid: leave BLANK
ms.title: page title | Microsoft Docs
ms.prod: get from list
ms.service: get from list
author: githubalias
ms.author: msalias
ms.manager: msalias
---
```

* Use only *one* of `ms.prod` or `ms.service`, do not use both.
* You can find the **get from list** list of available metadata field values at [aka.ms/skyeye/meta](https://aka.ms/skyeye/meta).

## Definitions

* **ref conceptual** -- Markdown topics that are REST API-specific for a service, but are not generated by CI ([example 1](https://github.com/Azure/azure-docs-rest-apis/blob/master/docs-ref-conceptual/documentdb/restful-interactions-with-documentdb-resources.md), [example 2](https://github.com/Azure/azure-docs-rest-apis/blob/master/docs-ref-conceptual/batchservice/Batch-Status-and-Error-Codes.md)).