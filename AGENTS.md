## graphify

This project has a graphify knowledge graph at graphify-out/.

Rules:
- When working on Graphify itself, use the repository's existing Graphify guidance. For codebase questions, prefer scoped graph queries where available; use the report for broad orientation. Do not use the graph as evidence when the task concerns the graph's correctness itself.
- If graphify-out/wiki/index.md exists, navigate it instead of reading raw files
- After modifying code files in this session, run `graphify update .` to keep the graph current (AST-only, no API cost)

## Base44 dev environment

- **Run:** `docker compose -f docker-compose.base44.yml up -d` — builds the image, runs `graphify extract worked/example --code-only` + `graphify cluster-only`, then serves the interactive `graph.html` on port 3000.
- **No external credentials needed** — code-only extraction uses tree-sitter AST (fully local). To enable LLM community naming or semantic doc/paper/image extraction, set an API key (e.g. `GOOGLE_API_KEY`) via the Base44 secrets dashboard.
- **Editable install:** the source is bind-mounted at `/app`; `pip install -e .` in the image means edits to `graphify/` are reflected without rebuilding.
- **Re-run graphify after source edits:** the container runs graphify once at startup. To regenerate the graph after changing graphify's own code, restart the service (`docker compose -f docker-compose.base44.yml restart graphify`).
- **Change the corpus:** edit the `command:` in `docker-compose.base44.yml` to point `graphify extract` at a different directory.
