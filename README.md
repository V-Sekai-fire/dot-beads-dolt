# dot-beads-dolt

Dolt data plane for the weftspun beads issue graph.

Beads gitignores its embedded Dolt database, so the issues and memories in
`.beads/embeddeddolt/` never reach `dot-beads`. This repository is where they
go instead, pushed with `bd dolt push` and fetched with `bd dolt pull`.

Nothing checks this out. It is a remote, not a workspace path, so it carries
no entry in the goal manifest. The checkout is `dot-beads`, placed at `.beads`.

## The data is not on this branch

It is under `refs/dolt/data`, which is not a branch, so a plain `git clone`
returns this README and nothing else. That is what the storage format does;
it is not a sign the data is missing. Measured on 2026-09-20: 8.7 MB of chunk
files there, against an 82 KB ordinary clone.

Neither a Download-ZIP nor a release tarball is a backup of this repository,
for the same reason. Two things do carry the data:

    git clone --mirror https://github.com/V-Sekai-fire/dot-beads-dolt.git

    mkdir recovery && cd recovery && mkdir .beads
    cp <workspace>/.beads/config.yaml .beads/
    bd bootstrap

The second is the one that gives back a working database. It runs
`dolt clone git+https://...` underneath. A full recovery was measured on
2026-09-20: 5,239 chunks over the network into an empty directory, returning
every issue and every memory.

Run it from a short path. Dolt writes a cache path with a 64-character chunk
id in it, and on Windows a deep working directory overruns MAX_PATH; the
error names a hooks directory and is followed by credential hints, so it
reads as an authentication failure rather than a path-length one.
