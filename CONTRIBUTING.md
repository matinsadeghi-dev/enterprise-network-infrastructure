# Contributing and editing guidelines

This is a learning project. Contributions should improve clarity and technical accuracy without claiming that simulated connectivity has been tested unless it has actually been verified.

## Guidelines

- Keep `index.html` self-contained (plain HTML and CSS) unless there is a clear reason to add a build tool.
- Update `docs/ADDRESSING-PLAN.md` and `docs/TOPOLOGY.md` whenever device names or addresses change.
- Mark unknown IPs as unknown rather than guessing them.
- Verify commands against the router/switch model and the current Packet Tracer configuration before calling them tested.
- Keep topology labels readable and ensure all endpoints appear in the diagram and device inventory.
- Do not commit credentials, private keys, access tokens, or unrelated personal data.

## Suggested workflow

1. Make a focused change.
2. Verify HTML opens in a browser.
3. Test relevant settings in Packet Tracer where possible.
4. Check `git diff` and `git status`.
5. Commit with a clear message describing the change.
