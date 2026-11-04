# HADA Content Studio Template

An agent-independent template for managing reusable, sourced knowledge and creating
infographics for many kinds of mini-projects. Its portable character, item, appearance,
asset, prompt, and provenance data can also be reused by HADA Story Studio; Story adds
its own continuity and timeline model.

Content Studio is a specialized template based on the HADA Base 0.1.1 contract. Its own
template version is tracked separately. The initial production module is infographics.

AI-generated images are non-reproducible source masters and are never direct external
publication files. Accepted masters and reusable character reference sheets are
preserved. Python produces destination-specific watermarked derivatives; publication
records capture where each derivative was used. `build/` is reserved for byte-identical
reproducible results.

See `AGENTS.md` and `SPEC.md` for the operating rules and implementation contract.
Read the project-root `WHY.md` before significant work. When the owner states or adopts
a durable reason, run `python tools/record_why.py --root PROJECT_ROOT` to append it
without replacing earlier entries. `config/template-manifest.json` defines version and
file ownership.

## Workflows

- [Shared data model](docs/DATA_MODEL.md): mini-project, knowledge, character/item, and
  Story-compatible identifiers.
- [Prompt system](docs/PROMPT_SYSTEM.md): layered prompt composition and private
  resolution records, pre-generation prompt archives, and review history.
- [Prompt review checklist](docs/PROMPT_REVIEW_CHECKLIST.md): agreed briefs, candidate
  scoring, evidence, revision links, evaluator identity, and image-generation gate.
- [Image lifecycle](docs/ASSET_LIFECYCLE.md): accepted source intake, watermark/export
  profiles, metadata checks, and post-publication records.

From the project root, run `python tools/validate.py` to check versions, schemas,
relationships, hashes, prompt resolutions and review archives, image derivatives, and
publication records.
Run `python tools/catalog.py` to print a stable overview of the project's mini-projects.
