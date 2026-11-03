# ReSPEC — Reusable Template Package

**Review date:** 2026-11-02
**Package role:** template
**Template version:** 0.1.0
**Base compatibility:** minimum/tested 0.1.0

## Observed implementation

- Includes reusable schemas, generic prompt layers, export profiles, validation and
  catalog tools, tests, and lifecycle documentation.
- The template role forbids character-instance records and project image-generation
  records. Sample character names are declared in the local Sample manifest; the shared
  validator has no hard-coded sample identity.
- Prompt sidecars verify source hashes and exact recomposition. Asset export applies
  Python watermark profiles and metadata checks before marking output ready for human
  review.
- No user-specific character records, images, private logs, or project-owner names are
  present in this checkout.

## Validation

- 12/12 unit tests pass.
- The role-specific contract validator passes.
- Git whitespace validation passes for the prepared working-tree changes.

Release packaging and publication are controlled by the repository owner.