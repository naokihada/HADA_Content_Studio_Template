# ReSPEC — Observed Implementation

## Current status — 2026-11-04

Dev now contains the v0.1.1 prompt archive and review-gate implementation. The reusable
Template checkout now has the reviewed v0.1.1 files as local working-tree changes; its
release tree remains uncommitted. No push has been made.

## Baseline

**Review date:** 2026-11-02
**Status:** Phases 1–4 implemented; Sample and final cross-artifact review remain.

The repository originally contained `README.md`, `LICENSE`, the user-owned `WHY.md`,
and user-owned imported files under `AI/Logs/`. The latter files remain unmodified and
uncommitted. No schemas, asset tools, prompt resolver, infographic exporter, or
publication validator existed at baseline.

The initial implementation plan now records the Content Studio-specific requirements,
Base 0.1.0 compatibility, Story-compatible shared data layer, sample-only character
instance rule, and image-publication boundary in `SPEC.md`.

Phase 1 verification: `config/template-manifest.json` parses as JSON; the template ID,
Content Studio version, Base minimum/tested versions, `TEMPLATE_BASE.md`, and first
CHANGELOG heading agree. `git diff --check` passes. No character instance data was
added to Dev.

## Reconciliation

**SPEC_ONLY:** Sample illustration work and final cross-artifact review remain planned.
Each phase will update this record with observed behavior and validation evidence.

## Phase 2 — shared records and mini-project catalog

- **MATCH:** `schemas/common/records.schema.json` defines shared character, appearance,
  item and item-variant, character-item link, outfit, and asset-reference contracts.
  `schemas/content/` defines mini-project, sourced knowledge, infographic production,
  and publication records. Optional extension objects let Story add its own fields
  without changing shared IDs or copying records.
- **MATCH:** `CharacterItemLink` supports one item linked to multiple characters; a
  synthetic test links one uniform to two characters. Item variants remain attached to
  their parent item, including when selected by a link or outfit component. Chibi
  proportions are an `AppearanceVariant` retaining the same character ID.
- **MATCH:** `tools/catalog.py` lists mini-projects across arbitrary domains in stable
  order without writing a second index source.
- **MATCH:** Dev contains schemas and ephemeral tests only, no character records.
- **Validation:** 5/5 tests pass; `tools/validate.py` passes; Python compilation passes.

## Phase 3 — prompt composition and private provenance sidecars

- **MATCH:** `tools/resolve_prompt.py` composes shared, domain, medium, project, entity,
  and request layers in fixed order. It performs literal substitution, rejects missing
  and unused values, and writes a sidecar once without replacing existing files.
- **MATCH:** Each sidecar records exact prompt/profile/values/layer/reference hashes.
  `tools/validate.py` reloads those sources, verifies layer IDs/versions/order and
  substitutions, recomposes the prompt, and checks its exact hash.
- **MATCH:** Generic profile/layer examples and usage documentation are template-owned;
  Dev contains no character-specific prompt layers or character instance records.
- **Validation:** 8/8 tests pass; `tools/validate.py` passes; Python compilation passes.

## Phase 4 — immutable asset intake and Python export profiles

- **MATCH:** `tools/intake_asset.py` validates PNG/JPEG input, copies source bytes without
  editing or moving the input, records a source hash and reviewer, and stores accepted
  masters separately from retained discard candidates. Existing source/record targets
  are never overwritten.
- **MATCH:** `tools/export_image.py` accepts only an accepted master. The social example
  downsizes and writes a lossy JPEG; the website example preserves pixel dimensions and
  writes PNG. Both apply the configured logo and create durable sidecars.
- **MATCH:** The binary scanner checks PNG chunks and JPEG segments after re-encoding.
  Extra metadata blocks publication eligibility. `tools/record_publication.py` records
  only a verified derivative and performs no network operation.
- **Validation:** 12/12 tests pass; `tools/validate.py` passes; Python compilation
  passes. Repeated social export hashes match, while raw source bytes remain unchanged.

## Phase 5 — Sample character and capability infographic

- **MATCH:** The Sample repository declares one fictional `Cute Elf Girl`. Its chibi
  variant preserves the same character ID and identity anchors; a separate soft-cel
  appearance retains the first style study. A reusable clothing item, item variant,
  outfit, and character-item link are stored separately. The reusable validator uses
  optional manifest `sample_character_name`; it does not pin a user-specific name.
- **MATCH:** Exact prompt sidecars and four private source masters stay in Sample. The
  Japanese feature infographic was rendered twice with byte-identical output
  (`sha256:39d316501206d909f27f7488b946564ef5a9aa50fa32744035e22d6716ee1dba`), then
  preserved as a master. Website and social derivatives were exported and passed
  metadata checks. Their status remains `ready_for_human_review`; no publication record
  or network upload was created.
- **MATCH:** Public Template contains no character instance records, image assets,
  imported conversation logs, or project-owner name. Its role manifest forbids
  character and generation records. Template and Sample stay at their original Git
  commits with local working-tree changes only.
- **Validation:** Dev, Template, and Sample each pass 12/12 tests and
  `tools/validate.py`. Dev Python compilation and all three `git diff --check` checks
  pass. Website guide is 1600 × 2320 PNG; social guide is 497 × 720 JPEG. Character
  website derivatives preserve their corresponding source dimensions.

## Phase 6 — three ReSPEC loops

1. **Data and contract:** versions, role manifests, one Sample character, same-ID
   appearance variants, and independent many-to-many item/outfit records match SPEC.
   The name-specific validator was generalized and test fixtures were made role-local.
2. **Prompts and media:** prompt resolution hashes and references validate; generated
   originals remain private; all five derivatives have clean metadata scans. The first
   chibi attempt did not meet the requested proportion, so its provenance was retained
   as a style study and a clear 2.5-head chibi was generated for the infographic.
3. **Privacy and repository boundaries:** Template contains no local character or
   generated image files; imported Dev `WHY.md` and AI logs were not staged. Only Dev
   phase files are eligible for a checkpoint commit. Template/Sample remain
   uncommitted, and no push was made.

## Phase 7 — prompt archive and review gate

- **MATCH:** Dev stores project briefs, a prompt review YAML, and the exact selected
  prompt under each infographic production's private `prompts/` directory. Candidate
  text and hashes, fixed rubric evidence, hard checks, revision-to-finding changes,
  runtime evaluator metadata, and final selection are recorded before generation.
- **MATCH:** `tools/validate.py` checks rubric totals, candidate sequence and limit,
  score arithmetic and hard-gate capping, revision lineage, evaluator consistency,
  selected prompt text/hash, prompt-resolution linkage, and the required review gate.
  `tools/intake_asset.py` rejects generation intake without a completed review when the
  project enables `prompt_review_required`; it also records optional generation
  arguments with the source-file hash in the private generation record.
- **MATCH:** Projects without the new setting retain their historical behavior. Existing
  prompt and generation records were not rewritten or rescored. Template-role validation
  rejects private project and prompt records.
- **Validation:** `python tools/validate.py` passes in Dev and Template; Python syntax
  checks pass in Dev and in-memory for the read-only Template checkout; `git diff --check`
  passes in both. Unit tests were not run. Template and Sample remain uncommitted; no push
  was made.

## Phase 8 — Base 0.1.1 WHY lifecycle alignment

- **MATCH:** The public Template now includes the generic root WHY placeholder, shared
  append-only recorder, agent lifecycle rules, and validator checks for both required
  files. No Dev WHY history was copied.
- **MATCH:** Its manifest, SPEC, and TEMPLATE_BASE.md retain Content Studio v0.1.1 and
  report Base minimum 0.1.0/tested 0.1.1.
- **Validation:** `python -B tools/validate.py` passes; in-memory syntax compilation
  passes for the recorder and validator; `git diff --check` passes. Unit tests were not
  added or run. The Template working tree remains uncommitted; no push was made.

## v0.1.1 release readiness — 2026-11-04

- **Status:** Preparation remains incomplete. The manifest still declares `role: dev` and `contains_user_data: true`, and policy/implementation conflict hunks remain unresolved.
- **Completed:** Conflict-free template-owned changes were merged and missing declared policy/profile files were added. Dev WHY history and AI logs were not copied.
- **Validation:** `python -B tools/validate.py` and `git diff --check` pass. Unit tests were not run.
- **Boundary:** No release commit, tag, or push was made.
