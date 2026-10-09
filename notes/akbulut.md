# Selman Akbulut: first reading map

Research notes, begun 2026-10-09. These are *notes about* the cited works, not transcriptions or redistributions of their figures.

## Identification and attribution

**Selman Akbulut is very probably the person intended.** In his 2022 autobiographical essay, Robion C. Kirby said that the framed-link pictures were called “Kirby calculus” even though “others, especially Akbulut, developed it far beyond what I had done.” That verifies unusually strong credit from Kirby; it does **not** verify a verbatim claim that Akbulut was “the best practitioner.” [Kirby, *My professional life*, section 3](https://celebratio.org/Kirby_RC/article/982/).

There is a useful counterpoint in Akbulut's own short note, [*Kirby calculus?*](https://www.selmanakbulut.com/kirby.pdf). He objects to reducing 4-manifold research to clever-looking moves on diagrams. Handle decompositions and slides are techniques; a proof has to say what manifold or structure those techniques establish. Adopt that attitude here.

Kirby also specifically credits Akbulut with introducing the **dotted unknot notation for a 4-dimensional 1-handle** in his memoir. The dot encodes removing a thickened spanning disk, rather than an ordinary 0-framed 2-handle. Changing a dot to a zero has a legitimate *surgery/dual-handle* interpretation in specific constructions, but is **not** a free move preserving an arbitrary 4-dimensional handlebody.

**Casson connection:** Akbulut and **John D. McCarthy** wrote an exposition of **Andrew J. Casson's invariant** in 1990. This confirms Akbulut's connection with Casson's work; it does not make Andrew Casson a coauthor of that book. The recollection about a Casson coauthor remains unverified. [Publisher record](https://www.jstor.org/stable/j.ctt7ztjbw).

## Mathematical objects to keep distinct

1. **Framed surgery link in the 3-sphere.** A link with integer framings gives an oriented closed 3-manifold by Dehn surgery. Kirby's original equivalence result uses 2-handle slides and addition/removal of an isolated plus- or minus-one-framed unknot. This is a theorem about **the resulting 3-manifold**, not a promise that the corresponding 4-dimensional traces are diffeomorphic.
2. **4-dimensional 0/1/2-handlebody.** Start with a 4-ball, add 1-handles (dotted unknots or pairs of attaching 3-balls), and 2-handles (framed attaching curves). A 2-handle is a copy of D² × D² attached along S¹ × D². The framing cannot be inferred merely from the shape of an unmarked curve.
3. **Mazur-type contractible handlebody.** The simple handle count is one 0-handle, one 1-handle, one 2-handle, so the Euler characteristic is 1 - 1 + 1 = 1. When the 2-handle's attaching circle goes algebraically once over the 1-handle, it kills the fundamental-group generator; the *geometric* number of traversals can differ, and the handles need not cancel geometrically. Boundaries can be nontrivial homology 3-spheres.
4. **Cork twist.** A contractible smooth 4-manifold W, an appropriate boundary diffeomorphism f, and an embedding in a surrounding smooth manifold M are part of the data. Remove W and reglue by f; in a cork example the smooth structure of M changes. Do not conflate an arbitrary Mazur manifold with a cork. Definitions vary across the literature; Akbulut's [*Corks* (2025 version)](https://arxiv.org/abs/2406.15369) explicitly distinguishes loose corks from Stein corks.
5. **Pictures versus evidence.** Store each handle move with a named operation, local attachment data, framing updates, source/target objects, and a justification. A continuously rotated model is a way to *inspect* this data, not the data itself.

## Prioritized reading / experiments

### A. The source of the calculus

**Robion C. Kirby**, “A calculus for framed links in S³,” *Inventiones Mathematicae* **45** (1978), 35–56. [DOI](https://doi.org/10.1007/BF01406222) · [author-hosted PDF](https://math.berkeley.edu/~kirby/papers/Kirby%20-%20A%20calculus%20for%20framed%20links%20in%20S%5E3%20-%20MR0467753.pdf).

* Study the two generating operations and what kind of equivalence they prove.
* Visual experiment: a 2-handle slide by band-summing a framed push-off to another attaching circle; update the ribbon representing the framing, not just the centerline.
* Distinguish 3-manifold surgery equivalence, 4-manifold diffeomorphism, and changes to marked boundary data.

### B. Handlebody notation and Mazur manifolds

**Selman Akbulut and Robion Kirby**, “Mazur manifolds,” *Michigan Mathematical Journal* **26** (1979), 259–284. [PDF hosted by Kirby](https://math.berkeley.edu/~kirby/papers/Akbulut%20and%20Kirby%20-%20Mazur%20manifolds%20-%20MR0544597.pdf).

* Work through the dotted-circle representation of a 1-handle, algebraic versus geometric passage of an attaching circle through it, and the boundary homology-sphere calculations.
* First proposed interactive example: one dotted circle + one framed attaching circle, shown in a linked 3D strand view and the orthodox 2D Kirby projection.
* Preserve the original labeling of their families W⁺(ℓ,k) and W⁻(ℓ,k). Never guess a member's framing from a generic cork thumbnail.

### C. Casson's invariant, separately

**Selman Akbulut and John D. McCarthy**, *Casson's Invariant for Oriented Homology Three-Spheres: An Exposition*, Princeton University Press, Mathematical Notes **36** (1990). [Publisher/library record](https://www.jstor.org/stable/j.ctt7ztjbw).

* An invariant of oriented integral homology 3-spheres, historically based on SU(2) representation-space constructions.
* Useful later: select a 3-manifold by framed surgery, then show which invariants belong to its boundary, not to arbitrary choices of handle presentation.
* The invariant is due to Andrew Casson; the exposition is written by Akbulut and McCarthy.

### D. The exotic smooth-structure step

**Selman Akbulut**, “A fake compact contractible 4-manifold,” *Journal of Differential Geometry* **33** (1991), 335–356. [DOI](https://doi.org/10.4310/jdg/1214446320) · [author's paper list](https://www.selmanakbulut.com/vita/pub.html).

**Selman Akbulut**, “An exotic 4-manifold,” *Journal of Differential Geometry* **33** (1991), 357–361. [Author PDF](https://www.selmanakbulut.com/papers/29.pdf).

* First understand the distinction between a diffeomorphism **relative to a prescribed boundary identification** and an unmarked diffeomorphism.
* Animate cutting and regluing only with the boundary map explicitly attached to the object; a camera rotation is not a cork twist.
* Distinguish the relative construction of the first paper from the stronger smooth-structure distinction in the second.

### E. Akbulut's reference book and updates

**Selman Akbulut**, *4-Manifolds*, Oxford University Press (2016). [DOI / contents](https://doi.org/10.1093/acprof:oso/9780198784869.001.0001).

Start with chapter 1 (carving, slides, cancellation, ribbon carving) and chapter 10 (corks, anticorks, plugs), then chapters 2–3 (building and gluing manifolds). Treat the book's original pictures as references **to redraw from first principles**, not as assets to rehost.

**Selman Akbulut**, “Corks,” arXiv:2406.15369 (updated 2025). [Author's short note](https://arxiv.org/abs/2406.15369). This explicitly revisits terminology and the distinction between the original Mazur construction and a cork.

**Selman Akbulut and Kouichi Yasui**, “Corks, Plugs and exotic structures,” *Journal of Gökova Geometry Topology* **2** (2008), 40–82. [Akbulut's publications](https://www.selmanakbulut.com/vita/pub.html).

### F. Supplementary exposition / original presentations

**Robert E. Gompf and András I. Stipsicz**, *4-Manifolds and Kirby Calculus*, American Mathematical Society, Graduate Studies in Mathematics **20** (1999). [DOI](https://doi.org/10.1090/gsm/020). Especially chapters 4–6: handlebodies, moves, worked examples.

**Selman Akbulut**, [personal publication and lecture index](https://www.selmanakbulut.com/) and 2014 Simons Center lectures: [“Corks, Plugs and exotic structures”](https://scgp.stonybrook.edu/video_portal/video.php?id=1278), [“Handlebodies of exotic 4-manifolds”](https://scgp.stonybrook.edu/video_portal/video.php?id=1291) (slides linked on that page). The lecture recordings are not redistributable without the Simons Center's consent.

**Robion C. Kirby**, [memoir, section 3](https://celebratio.org/Kirby_RC/article/982/) is the primary source for the historical identification. **Selman Akbulut**, [“Kirby calculus?”](https://www.selmanakbulut.com/kirby.pdf), is an essential corrective about interpretation.

## Visual tasks these readings suggest

* **Framed link + 3D ribbon:** freely rotate the actual embedding; derive each over/under crossing from the current camera projection; show linking and framing numbers in a separate panel.
* **Handle slide with receipts:** record the band, source component, target component, framed push-off, and before/after linking matrix; make the mathematical move inspectable.
* **Dotted circle / feet of a 1-handle:** two visualization conventions for the same 1-handle; explicitly label a dot-to-zero change as surgery when appropriate.
* **Cork demonstration:** show the 4D object by 3D handle data and a time-ordered sequence of 3D boundary and handle pictures. Never pretend a single 3D mesh displays an exotic smooth structure.

Continue in [pants / co-pants notes](pants-copants.md) for the simpler, rigorous surface-cobordism prototype.

## Credit and reuse

Thanks to **Selman Akbulut**, **Robion C. Kirby**, **Andrew J. Casson**, **John D. McCarthy**, **Robert E. Gompf**, **András I. Stipsicz**, and **Kouichi Yasui** for the works specifically identified here. Additional source authors should be named individually when their works enter the notes. Link primary sources; do not copy third-party diagrams or copyrighted book chapters into this repository.
