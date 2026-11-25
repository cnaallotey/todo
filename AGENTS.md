<!-- voxium:start -->
## Architecture rules (managed by Voxium)

This project has an enforced architecture. Pull requests that break it fail the Voxium check. Read this before adding imports or new files.

### Layers, top to bottom
A module may import from itself or from any module listed below it. Never import upward.

1. `src` (src/**)

### Rules
* LAYER01 [block]: Modules may only import from their own module or from modules lower in the layer order: src. Why: A fixed dependency direction keeps lower layers reusable and stops circular knowledge between areas of the app.
* CYCLE01 [block]: Modules must not depend on each other in a cycle. Why: Cycles make modules impossible to change, test or extract on their own.
* SIZE01 [warn]: Source files should stay under 600 lines. Why: Very large files usually mix responsibilities and are hard for humans and agents to change safely.

### How to work within this
* Before importing across modules, check the layer order above. If the import points upward, move the shared code down or pass it in as a parameter.
* If the Voxium MCP server is available, use it: `get_rules_for_path` before editing a file, `check_import` before adding a cross module import, and `check_change` with your planned file contents before you finish.
* To suggest an architecture change, call `propose_architecture_change` on that server. You can suggest, you cannot approve.
* Do not edit anything in the `voxium/` folder or this block. Architecture changes need approval from a Team Leader. If you think the architecture should change, say so in your PR description and explain why.
<!-- voxium:end -->
