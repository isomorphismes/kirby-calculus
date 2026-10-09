# Reference code — source index

This folder currently contains **links and provenance notes, not vendored third-party code**. The [existing-code survey](../notes/existing-code.md) explains what each project supplies, what was inspected, and what remains untested.

| Reference | Start reading here | Role / reuse status |
| --- | --- | --- |
| Neil Strickland, Owl | [`pants.js`](https://github.com/NeilStrickland/owl/blob/bdb4d8f9c56f6a43d1f7dfba8fca5c02541ee01b/pants.js), [`LICENSE`](https://github.com/NeilStrickland/owl/blob/bdb4d8f9c56f6a43d1f7dfba8fca5c02541ee01b/LICENSE) | Closest pants geometry; MIT code; source excerpt inspected |
| Strickland's teaching example | [`demos/pants.html`](https://github.com/NeilStrickland/knots_and_surfaces/blob/e42c1de297da08f13ebe31f52b183b4bf87c1d9a/demos/pants.html) | Shows use of Owl; separate repository/license scope |
| homotopy.io | [`homotopy-graphics/src/geom.rs`](https://github.com/homotopy-io/homotopy-rs/blob/master/homotopy-graphics/src/geom.rs), [`LICENSE`](https://github.com/homotopy-io/homotopy-rs/blob/master/LICENSE) | Compositional geometry and time; BSD-3-Clause source, separate documentation terms |
| Andrew Stacey, TQFT | [`tqft_code.dtx`](https://github.com/loopspace/TQFT/blob/master/tqft_code.dtx) | 2D boundary-aware cobordism drawing; LPPL 1.3c+ |
| MetaKnight | [`kirbyClass.py`](https://github.com/mattuff/metaknight/blob/master/kirbyClass.py), [`LICENSE.txt`](https://github.com/mattuff/metaknight/blob/master/LICENSE.txt) | Kirby-move algorithms; MIT; semantic/precondition audit required |
| Frank Swenton, KLO | [Author's demonstrations/documentation](https://community.middlebury.edu/~mathanimations/klo/) | Interaction reference; reusable source/license not established |
| Knottingham | [Repository](https://github.com/lennart-finke/knottingham) | Browser knot/link editing; MIT first-party code with separately licensed dependencies |
| PLink / Spherogram | [PLink](https://github.com/3-manifolds/PLink), [Spherogram API](https://snappy.computop.org/spherogram.html) | Encodings, editing, computational comparisons; precise package licenses still to inspect |

## Before importing anything

Record the upstream owner, full revision, exact paths, license notices, and original authors. Mark whether the result is an unchanged copy, a modification, a translation, or an independent implementation informed by the source. Preserve the applicable original notices rather than replacing them with this repository's terms.

Read the semantic caveats in the survey before treating any function name as a specification. In particular, pants naming can reverse the input/output convention; visual tube joins are not automatically mesh gluing; and omitted higher handles affect what a Kirby move claims to preserve.

No reference above was built or interactively tested in the 2026-10-09 research pass. Source availability and observed source content are not the same as a tested implementation.

Individual acknowledgments and links to the associated work are in the [survey credits](../notes/existing-code.md#credits-and-provenance).
