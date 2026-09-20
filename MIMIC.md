# Mimic fork

This branch is the maintained Blitz producer used by
[`moreveal/mimic`](https://github.com/moreveal/mimic).

- Upstream: [`DioxusLabs/blitz`](https://github.com/DioxusLabs/blitz)
- Fork: [`moreveal/blitz`](https://github.com/moreveal/blitz)
- Mimic branch: `mimic`
- Initial upstream base: [`e7bf7bca452bc9194ac5c9bcf2ac3c0ebcf02e09`](https://github.com/DioxusLabs/blitz/commit/e7bf7bca452bc9194ac5c9bcf2ac3c0ebcf02e09)

The `mimic` branch retains upstream Git history. Update it by fetching upstream
and merging an explicitly reviewed upstream revision:

```sh
git remote add upstream https://github.com/DioxusLabs/blitz.git
git fetch upstream
git switch mimic
git merge <reviewed-upstream-revision>
```

Resolve semantic conflicts here, run Mimic's correctness and performance gates,
push the resulting merge, and then update Mimic's pinned Cargo revision. Never
point Mimic at a moving branch.

## Mimic delta

Mimic uses `blitz-dom` as a renderer-free canonical style/layout producer. Its
changes expose and preserve products needed by CSSOM, geometry, visibility,
scrolling, observers and input while keeping Mimic's canonical DOM authoritative.
The retained changes include:

- authoritative focus, target, live-control, font and intrinsic-image inputs;
- canonical stylesheet URL and tree-order handling;
- resolved-style scalar and batch publication;
- inline, out-of-flow, skipped-content and table geometry products;
- CSS parent struts, atomic inline baselines and precise intrinsic metrics;
- renderer-independent caption, table and replaced-element behavior.

Mimic disables Blitz's renderer/GPU-facing default features and enables only
`system-fonts`. Patched Parley remains a separate dependency because it has a
different upstream repository.
