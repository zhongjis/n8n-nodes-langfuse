# PROJECT KNOWLEDGE BASE

**Generated:** 2026-01-18
**Commit:** b5eaffa
**Branch:** master

## OVERVIEW

n8n community node for Langfuse prompt management. Fetches prompts from Langfuse API.

## STRUCTURE

```
./
├── nodes/Langfuse/      # Node implementation
├── credentials/         # API credentials definition
└── dist/               # Compiled output (generated)
```

## WHERE TO LOOK

| Task              | Location                               | Notes                                |
| ----------------- | -------------------------------------- | ------------------------------------ |
| Add new operation | nodes/Langfuse/Langfuse.node.ts        | Add to properties array with routing |
| Modify auth       | credentials/LangfuseApi.credentials.ts | Uses Basic Auth                      |
| Build commands    | package.json scripts                   | Uses tsc + gulp (icons)              |
| Lint rules        | .eslintrc.js                           | n8n community node standards         |

## CODE MAP

| Symbol      | Type  | Location                               | Role            |
| ----------- | ----- | -------------------------------------- | --------------- |
| Langfuse    | Class | nodes/Langfuse/Langfuse.node.ts        | Main node class |
| LangfuseApi | Class | credentials/LangfuseApi.credentials.ts | Auth handler    |

## CONVENTIONS

- **Routing-based API**: Uses `routing.request` for HTTP configuration (not execute method)
- **Display options**: Shows/hides fields based on resource/operation selection
- **Credential testing**: `/api/public/projects` endpoint validates auth
- **Prompt labels**: Default "production" for version selection
- **Node naming**: "Get Prompt (Langfuse)" as default

## COMMANDS

```bash
npm run build         # Compile TypeScript + build icons
npm run dev           # Watch mode for development
npm run lint          # ESLint with n8n rules
npm run format        # Prettier formatting
```

## NOTES

- No test infrastructure - relies on n8n integration testing
- Custom gulp task for icon building
- PrepublishOnly enforces strict package.json naming
- Credentials use Basic Auth (publicKey as username, secretKey as password)
