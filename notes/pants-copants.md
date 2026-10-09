# Camera-rotatable pants and co-pants

Initial mathematical and rendering design, 2026-10-09. This is a proposal, not a claim of a completed viewer.

## 1. What the object is

Take an **oriented, genus-zero compact connected surface with three boundary circles**, conventionally a sphere with three open disks removed:

- P = S² minus three open disks;
- b(P) = 3, g(P) = 0;
- χ(P) = 2 - 2g - b = **-1**.

An elementary 2-dimensional bordism in **2Cob** becomes:

- **Pants / merge:** P : (S¹ ⊔ S¹) → S¹, with two incoming circles and one outgoing circle.
- **Co-pants / split:** P : S¹ → (S¹ ⊔ S¹), with one incoming circle and two outgoing circles.

Here source/target conventions include the appropriate induced orientations on boundaries; the unoriented *shape* can be the same. In a 2D oriented TQFT, these map respectively to multiplication μ : A ⊗ A → A and comultiplication Δ : A → A ⊗ A.

Crucial distinctions:

1. Turning the **camera** around changes **neither** the mathematical bordism nor the input/output assignments.
2. Flipping the **height/time direction** and exchanging designated incoming/outgoing collars presents the reversed bordism. This is a different operation from rotating the mesh.
3. Co-pants are **not the inverse** of pants. Gluing a split to a merge, μ ∘ Δ : S¹ → S¹, produces a genus-one cobordism with two boundary circles, not the identity cylinder. This can be verified by χ = -1 + (-1) = -2, b = 2, hence g = 1.

Smallest falsifiable demonstration: show three labeled circles, a smoothly rotatable surface, and an explicit time-reverse switch that changes arrows without silently changing the camera.

## 2. Six alternative geometric presentations

### A. Planar domain embedded in 3D (most reliable first mathematical model)

Start with a **closed disk minus two disjoint interior open disks**; triangulate once, preserve its three combinatorially identified boundary cycles, then continuously deform its vertices via an embedding into R³ to get a recognizable pants form.

* Benefits: source topology is obvious; vertex/edge/face data and boundary identification survive camera rotation.
* Limitation: a flat starting pose does not look like trousers until deformed. Need prove/guard against self-intersections during deformation.
* A valid deformation is an isotopy of the embedded surface, not just arbitrary vertex morphing.

### B. Thickened three-arm tree / Y-pipe (most legible 3D silhouette)

Embed a tree with one trivalent vertex and three terminal branches in R³. A sufficiently small regular tubular neighborhood of the tree is topologically a **3-ball**. Its boundary is S². Remove three disjoint surface disks near the terminal branches: the remaining surface is **exactly a pair of pants**.

* The 3D tubes, junction, and terminal openings produce a good rotatable shape.
* Surface smoothness is a separate geometric problem: use blends/fillets with radius smaller than local branch separation, and check the mesh is still embedded.
* Important: an untrimmed tube capped at all three ends gives a **sphere**, not pants; the **three open boundary collars** must remain.
* Keep the tree, collars, and boundary cycles as reference geometry independent of rendering.

### C. Morse/saddle movie (best explanation of merge and split)

Choose a Morse height h : P → [0,1] that is a product coordinate near its boundary collars and has **one index-1 critical point** in the interior. In suitable local coordinates near the saddle, h = h₀ + x² - y² (or the negative).

* At regular times, show the level circles h⁻¹(t), plus the whole surface ghosted behind them.
* Moving forward merges two circles to one; reversing time splits one into two. The saddle is the topological event, not a crossfade.
* At the critical time the *level set* is singular; the full 2-manifold P is smooth. Do not use the singular level contour as if it were the surface itself.
* A time scrubber and a freely rotatable camera are independent controls.

### D. Ribbon/band cobordism movie (bridge to knot theory)

Consider a **surface in S³ × [0,1]**, from a link in S³ at the start to a link at the end. A local saddle/band move can merge two components or split one: the trace is an elementary pair-of-pants surface.

* Show a 3D link in each time slice, and the attached band. Then show a projected 3D overview of the **4D** surface movie, with time/slice coloring.
* The embedded surface lives in **four dimensions**; a 3D projection may have crossings that are artifacts of projection. Track the fourth coordinate and over/under information.
* Natural next step: connect band moves, ribbon surfaces, branched covers, and the Akbulut–Kirby paper on branched covers of surfaces in 4-manifolds.

### E. Kirby handle / framed-link presentation (different mathematical object)

A Kirby picture represents 4D handle attachments via **1-handle markings and framed link components in dimension 3**, usually drawn on a 2D page. Render the framed attaching link as a rotatable 3D curve together with a **ribbon or chosen framing vector field**; keep the standard planar Kirby diagram synchronized.

* The pants surface itself is **not** a Kirby diagram.
* Display a 2-handle slide as a specified band sum with a framed push-off. Recompute the framing and linking matrix.
* Store whether a move preserves the boundary 3-manifold, a diffeomorphism type of a given 4-manifold, or only a relation with extra blow-up/down: do not use a generic “same manifold” indicator.
* An apparent crossing can change when the camera crosses a projection-singular direction; the 3D link is unchanged.

### F. Higher-dimensional analogue: slices, never a fake full-dimensional mesh

Define the (n+1)-dimensional sphere-pants object as an (n+1)-ball with the interiors of two smaller, disjoint (n+1)-balls removed. Its boundary consists of three n-spheres, as an abstract cobordism from two spheres to one (or reversed).

* n = 1 gives the familiar **2D** pants surface, drawable in R³.
* n = 2 gives a **3D** cobordism with **2-sphere** boundaries: it can be shown as a solid with cutaways and nested boundary surfaces.
* n = 3 gives a **4D** cobordism with **3-sphere** boundaries: use 3D slices, projections, and level-set movies. A 3D camera alone cannot rotate or display all four spatial coordinates.
* Distinguish this object from **P × D²**, which is a particular 4D thickening of the 2D surface with corners/vertical boundary, not automatically the same cobordism of closed 3-manifolds.

## 3. Abstract data before display data

An **Idriç-flavored type sketch**, not executable syntax:

    CircleObject  : OrientedClosedManifold 1
    Pants         : Bordism 2 (Circle ⊔ Circle) Circle
    CoPants       : Bordism 2 Circle (Circle ⊔ Circle)
    ReverseTime   : Bordism d Source Target -> Bordism d Target Source
    Camera        : Orientation3D × Projection × Zoom
    Render        : EmbeddedSurface3D -> Camera -> MeshImage

A real implementation also needs:

- A stable boundary component ID, role (incoming/outgoing), orientation and parameterization for each collar.
- The abstract cell complex / triangulation, plus an optional smooth embedding in R³.
- A height/Morse function, a finite list of critical points with index, and orientation of the movie.
- A camera pose distinct from the mathematical embedding (moving the camera should not mutate topology).
- For Kirby mode: an oriented framed link in a 3-manifold, a collection of dotted 1-handle circles, handle indices, the specified band when sliding, and which equivalence is asserted.

A renderer only receives a **projection/view of this structure**. Surface topology, cobordism direction, framing, and handle-slide witnesses must not live solely inside screen coordinates.

## 4. Concrete user interactions

| Action | Mathematical effect | Visual effect |
| --- | --- | --- |
| One-finger drag | None | Orbit camera around a **fixed** 3D surface |
| Pinch | None | Zoom |
| Time scrubber | Change regular level h⁻¹(t) shown | Trace circles merge/split at the Morse saddle |
| Pants ↔ co-pants | Swap in/out designation and reverse time orientation | Arrows, collars and movie direction update; optional camera pose stays fixed |
| Boundary highlight | None | Select one of three labeled S¹ collars |
| Show dual diagram | None | Synchronize tree, mesh, saddle slice and planar schematic |
| Kirby handle slide (later) | An explicitly recorded 2-handle slide | Framed curves, band and linking-matrix evidence update |

Always let an action cause a **legible** response even if a single pixel is invisible (outline, label, marker motion, change in multiple adjacent pixels, or a displayed invariant). This is an interface choice, not a redefinition of the topological invariants.

## 5. Tests before an elaborate visual design

1. **Topology of each mesh:** exactly one connected orientable 2-manifold with boundary; **three boundary components**; Euler characteristic **-1**; hence genus 0. Check every edge has one or two incident triangles as appropriate, consistent orientation, and no unexpected pinch or self-intersection.
2. **Bordism bookkeeping:** source and target each receive the intended circles and orientations. Applying the time-reverse control twice restores the original labels.
3. **Composition:** glue a merge after a split to obtain χ = -2, b = 2 and genus 1; do not simplify to the identity cylinder. Gluing along identified circles must respect collars/parameterizations.
4. **Morse movie:** away from the saddle, the regular level sets are disjoint embedded circles; across the one critical level, the count changes **2↔1**. Mesh topology itself remains P throughout.
5. **Camera independence:** moving camera leaves boundary IDs, genus, Euler characteristic, Morse data and any framed-link invariants unchanged.
6. **Framings in Kirby mode:** preserve linking and self-framing conventions when the camera rotates. For a framed 2-handle link with linking matrix Q, an oriented integral basis handle slide has Q' = Uᵀ Q U for its elementary unimodular matrix U (using a consistently chosen basis); do not apply the same naive formula to dotted 1-handles without extra setup.
7. **Readable view:** when a boundary collar is rear-facing, use ghosted arcs / labels or an inset; avoid hiding an entire branch behind the surface. Test a narrow portrait Android screen as well as desktop.

## 6. Suggested order of presentation

Start with **B** (recognizable Y-shaped pants, three boundary circles) while keeping **A** as the provable combinatorial source. Add **C** as a time-sliced inset to convey the actual bordism. Then connect to **D** (a band-surgery movie) before introducing **E** (Akbulut's dotted circles, framed 2-handles and slides). Treat **F** as a separate dimension-up exploration.

This keeps the same semantic object visible as **planar domain**, **rotatable 3D surface**, **Morse movie**, and **source/target cobordism** before claiming any 4D equivalence.

## Reading links and reuse

- [Selman Akbulut, *4-Manifolds* (2016)](https://doi.org/10.1093/acprof:oso/9780198784869.001.0001), especially the early handlebody chapters.
- [Selman Akbulut and Robion C. Kirby, *Mazur manifolds* (1979)](https://math.berkeley.edu/~kirby/papers/Akbulut%20and%20Kirby%20-%20Mazur%20manifolds%20-%20MR0544597.pdf).
- [Robert E. Gompf and András I. Stipsicz, *4-Manifolds and Kirby Calculus* (1999)](https://doi.org/10.1090/gsm/020).
- [Robion C. Kirby, *A calculus for framed links in S³* (1978)](https://doi.org/10.1007/BF01406222).
- [Selman Akbulut, *Kirby calculus?*](https://www.selmanakbulut.com/kirby.pdf) — important caution about mistaking handle diagrams for proofs.
- [Wikimedia Commons: *Pair of pants cobordism (pantslike)*](https://commons.wikimedia.org/wiki/File:Pair_of_pants_cobordism_(pantslike).svg) — reference visual only; verify asset license separately if importing.
- [Kirby and Akbulut bibliography / reading notes](akbulut.md).

Thanks to **Selman Akbulut**, **Robion C. Kirby**, **Robert E. Gompf**, and **András I. Stipsicz** for the referenced mathematical work. All rendering geometry proposed here should be original, with source links and clear distinction between inspiration and implementation.
