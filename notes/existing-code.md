# Existing code: pants, cobordisms, and Kirby diagrams

Research pass: 2026-10-09. This supplements [the proposed visualizations](pants-copants.md) and [the Akbulut reading map](akbulut.md).

**Main finding:** Neil Strickland already has a specifically named `pants.js` module with pants meshes, three boundary-circle positions, and connecting tubes. We should examine this before inventing a mesh generator. homotopy.io supplies a different, complementary precedent: deriving geometry and movies from compositional mathematical data.

**Review limits:** Source excerpts were inspected for Strickland's pants module, homotopy.io's geometry construction, MetaKnight's moves, and Stacey's TQFT definitions. Other entries were checked through their authors' documentation, repository descriptions, or license files. No application was built or interactively tested in this pass. Nothing below certifies mathematical correctness, current browser compatibility, or performance on our phones. No third-party implementation has been copied into this repository.

## 1. Closest geometric match: Neil Strickland's pants module

[Source repository: NeilStrickland/owl](https://github.com/NeilStrickland/owl) · [teaching repository](https://github.com/NeilStrickland/knots_and_surfaces) · [author's course index](https://neilstrickland.github.io/knots_and_surfaces/).

The teaching example is [`demos/pants.html`](https://github.com/NeilStrickland/knots_and_surfaces/blob/e42c1de297da08f13ebe31f52b183b4bf87c1d9a/demos/pants.html). Its source creates six Babylon.js scenes and calls `owl3.pants.example[i]`. The heading describes closed orientable surfaces: these are assembly examples, not a complete directed-cobordism editor.

The teaching repository's `demos/owl` submodule pins the following revision, which was used for this inspection:

- Teaching revision: `e42c1de297da08f13ebe31f52b183b4bf87c1d9a`.
- Owl revision: `bdb4d8f9c56f6a43d1f7dfba8fca5c02541ee01b`.
- [Exact `pants.js` inspected](https://github.com/NeilStrickland/owl/blob/bdb4d8f9c56f6a43d1f7dfba8fca5c02541ee01b/pants.js), blob `81c6ec52668b366a3e17ecd8e1a69cd5dc2efe1e`.
- [Exact license inspected](https://github.com/NeilStrickland/owl/blob/bdb4d8f9c56f6a43d1f7dfba8fca5c02541ee01b/LICENSE): MIT, copyright 2020 Neil Strickland. The separate course-material license must not be confused with this code license.

### What the code actually supplies

`owl3.pants` records a centre, three `circle_centres`, and a `top` point specifying its local placement. Its `plot(scene)` transforms stored vertex positions and normals and submits triangle indices through Babylon's mesh interface. The first 260 lines also contain:

| Entry point | What to study |
| --- | --- |
| `rough_sector.embedding(s,t)` | A simpler geometric construction alongside the stored mesh |
| `outline(scene)` | Explicit boundary circles and a skeletal overview |
| `plot(scene)` | Separating mesh data from placement and rendering |
| `map(f)` | Transforming placement data; not a general isotopy guarantee |
| `sprout(i)` | Placing an adjacent pants piece at a selected boundary |
| `pants_tube` | Connector geometry with direction, bend, length, curvature |
| `pants_tube.joiner(c1,n1,c2,n2)` | Constructing a connector from endpoint centres and directions |

### What we could model on it

First reproduce one piece, show its three circles, and let the camera orbit independently. Next examine adjacent pieces and tube connections. The mesh positions, indices, and geometric formulas are a more direct starting point than choosing a new general-purpose modeling package.

What we still need is **semantic gluing**: stable boundary IDs, orientations, incoming/outgoing roles, collar parameterizations, and a record of which boundaries were identified. Placing two surfaces so they appear to meet does not prove that their triangle meshes have been welded or that an abstract bordism has been composed.

Likewise, this inspected excerpt does not supply the particular Morse function, critical-point bookkeeping, or split/merge time control in our proposal. Add those as independent data rather than deriving them from the camera pose.

The demo imports an unpinned Babylon preview build. A reproducible adaptation should pin dependencies. Reusing the mathematical geometry would not oblige us to choose Babylon.js as the renderer for the eventual application.

**First checks before adopting the geometry:** count connected components and boundary cycles, compute Euler characteristic, check vertex links as well as edge incidence, verify orientability, and inspect for self-intersections. These checks have not yet been run.

## 2. Compositional geometry and movies: homotopy.io

[homotopy-io/homotopy-rs](https://github.com/homotopy-io/homotopy-rs) · [application](https://homotopy.io/) · [tutorial](https://github.com/homotopy-io/homotopy-rs/blob/master/TUTORIAL.md).

The project constructs composites in finitely generated semistrict n-categories. Its documented displays include 2D and 3D geometry and 4D diagrams presented as movies of 3D geometry. It uses Rust compiled to WebAssembly. The project distinguishes its BSD-3-Clause source license from its CC BY 4.0 documentation license.

The particularly relevant inspected source is [`homotopy-graphics/src/geom.rs`](https://github.com/homotopy-io/homotopy-rs/blob/master/homotopy-graphics/src/geom.rs), blob `5a38845b153f0cce6ba519ceb06c3eafeed43331`. This blob identifies the reviewed contents; the branch URL may subsequently change.

`VertData` includes four-coordinate positions, boundary flags, and a mathematical generator. `Geometry` distinguishes points, curves, areas, and volumes. `CubicalGeometry::new` extracts a mesh and layout from a diagram, with different coordinate assignments for static and animated displays. This is concrete evidence of a mathematical object being converted into geometry, rather than mathematical meaning being stored only in screen coordinates.

**Our adaptation idea:** study the separation of mathematical diagram, layout, geometry, and movie time. Specify our own generators and relations for the intended bordism category. Do not silently identify its categorical presentation with a Kirby calculus or treat it as a proof checker for arbitrary smooth 4-manifold equivalence.

This is an architectural reference, not a reason to import the whole application to draw one pair of pants. Its available SVG/TikZ exports also suggest keeping a conventional diagram view beside the rotatable one.

## 3. Conventional pants/co-pants diagrams: Andrew Stacey's TQFT library

[loopspace/TQFT](https://github.com/loopspace/TQFT) · [annotated source `tqft_code.dtx`](https://github.com/loopspace/TQFT/blob/master/tqft_code.dtx) · [documentation source `tqft.tex`](https://github.com/loopspace/TQFT/blob/master/tqft.tex) · [CTAN record](https://ctan.org/pkg/tqft).

This is actual diagram-generating code, not just a collection of pictures. The inspected definitions provide incoming/outgoing boundary counts and presets for pants, reversed pants, cylinders, cups, and caps. Boundary anchors and separate visible/hidden arcs make it useful for labeled, composable 2D schematics. Its source specifies LPPL 1.3c or later. The maintained interface uses `\usetikzlibrary{tqft}`; the older node-based package is retained for legacy documents.

**An important convention mismatch:** the inspected code calls **one input and two outputs** a `pair of pants`, whereas our initial notes use pants for **two inputs and one output**. Neither naming convention should become an accidental semantic rule. Translate by the ordered input/output data, not by the English preset name.

Our use would be a conventional companion view and publication export. A TikZ silhouette is not an arbitrary-camera 3D surface. Study how the library exposes boundary anchors and flow direction; do not attempt to recover a unique 3D surface from its image.

## 4. Actual Kirby-move code: MetaKnight

[mattuff/metaknight](https://github.com/mattuff/metaknight), by **Yael Eisenberg, Laura Stordy, and Matthew Uffenheimer**. [MIT license](https://github.com/mattuff/metaknight/blob/master/LICENSE.txt).

Start with `componentClass.py`, `strandClass.py`, `crossingClass.py`, `joinClass.py`, and [`kirbyClass.py`](https://github.com/mattuff/metaknight/blob/master/kirbyClass.py). The README explains the component/strand/crossing representation. The inspected `kirbyClass.py` blob was `6208cb2a2c64c71c60c631414ac312652b301b34`; the review included its handle creation, cancellation, and slide implementations.

In `handle_slide(h1,h2,sign)`, **h2 slides over h1**. The implementation constructs a parallel copy, changes crossings, and uses writhe, stored framing, and linking information. This is a useful white-box reference for combinatorial bookkeeping. It is not yet an audited move engine for our use.

### A concrete semantic issue to resolve

The no-argument `handle_creation()` creates an isolated zero-framed 2-handle; the corresponding single-handle cancellation branch removes one. This needs a precise convention about omitted higher handles.

For a standalone 0/1/2-handlebody, adding a zero-framed unknot to the empty 4-ball presentation is **not** a diffeomorphism-preserving move: it produces S² × D², with boundary S² × S¹, rather than B⁴ with boundary S³. Its Euler characteristic is 2 rather than 1. This is our mathematical check of the operation's interpretation, not a runtime result.

Introducing a *cancelling 2/3-handle pair* is a different statement and can explain such diagram conventions when the 3-handle is implicit. Our representation must say which statement it means. Do not copy a function named “creation” and assume its equivalence claim fits every kind of diagram.

Also reconcile the package's stored framing convention with our chosen surgery coefficient. The inspected slide computes expressions involving writhe minus the stored framing. A number called `framing` is insufficient documentation for a translation.

**What to borrow:** decomposition into handles, strands, and crossings; explicit move arguments; worked examples. **What to add or independently verify:** move preconditions, immutable before/after records, framing conventions, treatment of 3-handles, and comparison tests. For an oriented framed 2-handle link, test the chosen slide convention against the appropriate integral basis change Q′ = UᵀQU; this matrix check alone is not a full verification of the move.

## 5. Kirby and band-move interaction: Frank Swenton's KLO

[Author's KLO page and demonstrations](https://community.middlebury.edu/~mathanimations/klo/) · [historical Kirby Calculator page](https://community.middlebury.edu/~mathanimations/kirbycalculator/index-old.html).

KLO documents a particularly relevant interaction: draw the band specifying a handle slide, then specify its twist. It also supports dotted 1-handles, blow-up/down operations, diagram redrawing, and navigable move sequences. Its author explicitly notes limitations on checking user-drawn 1-handles. The dot/zero switch is described as surgery, not as a harmless display change.

**Status:** an application and demonstrations were located; a publicly reusable source repository and its license were not established in this pass. This does not prove that source is unavailable. Treat KLO as an interaction reference, not license-cleared code to copy.

What we can learn: make the band selectable, preserve the history of mathematical operations, and distinguish a diagram redraw from a topology-changing operation.

Two additional author-hosted resources connect to saddle movies: [Brendan Owens and Frank Swenton's ribbon-disk data](https://community.middlebury.edu/~mathanimations/klo/ribbondisks/) and [Lucia Karageorghis and Frank Swenton's doubly-slice data](https://community.middlebury.edu/~mathanimations/klo/doublyslice/). These are leads for worked move sequences, not verified reusable source-code assets.

## 6. Browser diagram manipulation: Knottingham

[lennart-finke/knottingham](https://github.com/lennart-finke/knottingham) · [author's application and manual](https://www.fi-le.net/knottingham/).

**Lennart Finke and Edmund Weitz** provide a browser knot/link editor with Bézier editing, crossing computation, undo, and SVG/JSON/TikZ export. This is a useful reference for manipulating the planar side of our proposed synchronized views. Review depth here is the project description, application documentation, and first-party license, not a full audit of the mathematical implementation.

Its own code is MIT licensed, but its README identifies Spherogram as a GPL-licensed dependency and describes WebAssembly/Pyodide and SageCell use. Do not label the entire dependency bundle MIT or assume all invariant computations work offline.

The application's attempt to reject non-Reidemeister changes is not a general proof certificate. Its documentation also warns that some discontinuous edits can break equivalence and that TikZ export does not preserve all crossing information automatically. Prefer an explicit mathematical interchange format for round trips, independently of the drawing export.

The README credits **Joshua Horowitz's Knot Identification Tool**, **Kyle Miller's KnotFolio**, and Paper.js as influences/dependencies. Keep those acknowledgments visible when following or adapting that work.

## 7. Diagram interchange and computation: PLink / Spherogram

[PLink repository](https://github.com/3-manifolds/PLink) · [PLink manual](https://3-manifolds.github.io/PLink/index.html) · [SnapPy's PLink documentation](https://snappy.computop.org/plink.html) · [Spherogram API documentation](https://snappy.computop.org/spherogram.html).

PLink, associated with **Marc Culler and Nathan Dunfield**, edits piecewise-linear link projections and offers a Bézier-smoothed display. Its preserve-diagram option restricts moves across edges/vertices; its representations and exports connect drawing to combinatorial data. **The smooth display is still 2D**, not a rotatable 3D link embedding.

Spherogram supplies `Link`/`Crossing` structures, PD and DT encodings, link operations, and invariants. `Link.view()` opens PLink; it is not evidence of a 3D viewer. Its documented `add_band` is a particular band operation, not a generic implementation of all Kirby handle slides.

These are promising sources of interchange examples and independent comparisons. Check orientation, component ordering, and framing conventions explicitly. In particular, the documented PD-code orientation caveat for two-crossing components deserves a round-trip fixture before such data is treated as lossless.

This pass reviewed documentation, not the whole implementation or individual distribution licenses. Verify the precise package and dependency licenses before importing code. SnapPy/PLink's acknowledged predecessor **Jeff Weeks's SnapPea** should remain credited.

## 8. What this changes in our approach

Do not begin by committing to one engine or translating an entire large application. The candidates solve different problems:

| Need | First reference | Missing work in our project |
| --- | --- | --- |
| Recognizable rotatable pants geometry | Strickland's `owl/pants.js` | Validate mesh; add boundary semantics and independent camera |
| Composition and time-sliced geometry | homotopy.io | Specify our category/presentation and connect it to our geometry |
| Conventional labeled cobordism picture | Stacey's TQFT | Normalize arities; synchronize with the same abstract object |
| Framed-link move algorithms | MetaKnight | Audit conventions, preconditions, and implicit higher handles |
| Legible sequences of handle/band moves | KLO | Study behavior; source reuse permission not established |
| Browser knot-editing interaction | Knottingham | Add handle/framing semantics; separate dependency obligations |
| Diagram encodings and comparison fixtures | PLink / Spherogram | Verify round trips and conventions; no implied 3D rendering |

A small comparative experiment, when we move beyond notes, would preserve Strickland's original geometry as a reference and put **our own labeled incoming/outgoing circles** over a single pants piece. Camera motion must leave those assignments unchanged. Then compare a 2D schematic of that same data with the 3D model. A later experiment can study composition or a Morse movie without conflating it with joining rendered tubes.

These are proposed experiments, not work completed by this research pass.

## Credits and provenance

Thank you to **Neil Strickland; Nathan Corbyn; Lukas Heidemann; Nick Hu; Chiara Sarti; Calin Tataru; Jamie Vicary; Andrew Stacey; Yael Eisenberg; Laura Stordy; Matthew Uffenheimer; Frank Swenton; Brendan Owens; Lucia Karageorghis; Lennart Finke; Edmund Weitz; Marc Culler; Nathan Dunfield; Joshua Horowitz; Kyle Miller; and Jeff Weeks** for the identified work and acknowledged antecedents.

This credit pass covers the works and named antecedents identified above, not an asserted audit of every bibliography or contributor list. Follow additional citations and preserve their individual credits as those sources are read. Preserve original license notices if code is later imported. Our analysis, a linked source, a copied code file, a modified code file, and a reproduced figure must remain distinct in the provenance record.
