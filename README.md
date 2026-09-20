# dot-beads-dolt

Dolt data plane for the weftspun beads issue graph.

Beads gitignores its embedded Dolt database, so the issues and memories in
`.beads/embeddeddolt/` never reach `dot-beads`. This repository is where they
go instead, pushed with `bd dolt push` and fetched with `bd dolt pull`.

Nothing checks this out. It is a remote, not a workspace path, so it carries
no entry in the goal manifest. The checkout is `dot-beads`, placed at `.beads`.
