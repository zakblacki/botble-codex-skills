---
name: botble-code-review
description: Review Botble CMS code for correctness, security, Envato marketplace readiness, enum bugs, XSS, CSRF, CDN usage, BaseModel violations, inline JS/CSS, translation mistakes, N+1 queries, migration issues, and Botble-specific table, form, badge, media, and ecommerce pitfalls.
---

# Botble Code Review

Review with a bug-first stance. Findings must be actionable, scoped, and grounded in file and line references when available.

## Severity

Critical:

- Botble enum comparisons without `getValue()` or string cast.
- `{!! !!}` output without `BaseHelper::clean()`.
- CDN assets such as googleapis, jsdelivr, unpkg, or cdnjs.
- SQL injection, missing CSRF protection, or unsafe cookie access.

High:

- Models not extending `BaseModel`.
- Inline JavaScript/CSS.
- Dead code, commented-out code, or avoidable duplication.
- Views over roughly 150 lines or controllers over roughly 200 lines when complexity is not split.

Medium:

- ID parameters not typed as `int|string`.
- Hardcoded user-facing strings.
- `bigInteger` or `unsignedBigInteger` foreign keys instead of `foreignId()`.
- Cookie reads without allowlist validation.
- N+1 queries from missing eager loads.

Low:

- Missing `Model::query()`.
- `setInterval` without cleanup.
- Noisy comments.

## Envato Marketplace Checks

- No CDN assets; bundle dependencies locally.
- No hardcoded license checks.
- All user-facing strings are translatable.
- No hidden external calls or remote asset dependencies.

## Botble-Specific Checks

- Badge classes pair `bg-{color}` with `text-{color}-fg`.
- Custom table rendering uses `FormattedColumn::make()`.
- Product eager loading includes both `image` and `images` when image accessors need them.
- Plugin `remove()` drops all plugin tables and cleans all plugin settings.
- Plugin translations use `trans()`, not `__()`.
- Media paths render through `RvMedia::getImageUrl()`.

## Output

Lead with findings ordered by severity. If there are no findings, say so and mention residual test or coverage risk.

## Load References

Read `references/review-checklist.md` when doing a full pass.
