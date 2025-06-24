# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the Model Context Protocol (MCP) specification repository. MCP is a protocol that enables Large Language Model (LLM) applications to interact with external systems through a standardized client-server architecture. This repository contains the protocol specification, not the implementation SDKs.

## Key Commands

### Schema Development
- `npm run check:schema` - Validate both TypeScript and JSON schemas
- `npm run generate:json` - Generate JSON schemas from TypeScript definitions (run after modifying schema.ts)
- `npm run check:schema:ts` - Validate TypeScript compilation
- `npm run check:schema:json` - Ensure generated JSON matches TypeScript

### Documentation
- `npm run check:docs` - Validate documentation formatting and links
- `npm run format` - Auto-format MDX documentation files
- `npm run serve:docs` - Preview documentation locally (Mintlify)
- `npm run check:docs:links` - Check for broken internal links

### General
- `npm run check` - Run all validation checks (schema + docs)

## Architecture

### Protocol Structure
The MCP follows a client-server model where:
- **Hosts** (like Claude Desktop) initiate connections to servers
- **Clients** maintain 1:1 connections with servers
- **Servers** expose resources, tools, and prompts to clients

### Schema Organization
```
schema/
├── 2024-11-05/    # Historical version
├── 2025-03-26/    # Current stable version
├── 2025-06-18/    # Latest stable version
└── draft/         # Upcoming changes (work here for new features)
```

Schema changes are made in TypeScript (`schema.ts`) and JSON is generated from it. The protocol uses date-based versioning.

### Message Protocol
MCP uses JSON-RPC 2.0 with these message types:
- **Requests**: Require responses
- **Results**: Successful responses
- **Errors**: Failed responses
- **Notifications**: One-way messages

### Core Components
1. **Resources**: Expose data/content from servers
2. **Tools**: Enable LLMs to perform actions via servers
3. **Prompts**: Reusable prompt templates
4. **Sampling**: Servers can request LLM completions
5. **Roots**: Manage directory/file system access

### Documentation Structure
Documentation uses Mintlify and lives in `docs/`:
- `concepts/` - Core concept explanations
- `specification/` - Detailed protocol specs
- `tutorials/` - Step-by-step guides
- `quickstart/` - Getting started guides
- `sdk/` - SDK documentation references

## Development Workflow

1. For schema changes:
   - Modify TypeScript in `schema/draft/schema.ts`
   - Run `npm run generate:json` to update JSON
   - Run `npm run check:schema` to validate

2. For documentation:
   - Follow MDX format and existing structure
   - Update `docs.json` when adding pages
   - Run `npm run check:docs` before committing
   - Use `npm run format` to fix formatting

3. Contributing:
   - Follow the specification proposal process (Define → Prototype → Write)
   - Keep changes minimal and concrete
   - Base proposals on real implementation challenges

## Important Notes

- This is a specification repository - actual SDK implementations are in separate repos
- Schema changes require updating both TypeScript and generated JSON
- Documentation must be validated for formatting and broken links
- The protocol prioritizes simplicity and minimalism
- All contributions must align with existing architectural patterns