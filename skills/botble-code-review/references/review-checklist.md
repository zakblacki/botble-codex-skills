# Review Checklist

## Fast Search Patterns

Search for:

- `->value`
- `=== .*Enum::`
- `{!!`
- `DB::`
- `__\(`
- `cdnjs|jsdelivr|unpkg|googleapis`
- `onclick=|style=`
- `unsignedBigInteger|bigInteger`
- `Column::make`
- `setInterval`
- `$_COOKIE`
- `webpack.mix.js|npm run prod|npm run watch`

## False Positives

- `__()` is acceptable in theme JSON translation contexts.
- `where('status', SomeEnum::VALUE)` is acceptable because bindings use raw constants.
- Request input values are raw strings and do not need enum instances.
- Trusted framework-rendered HTML such as `RvMedia::image()` is not equivalent to unsanitized user content.

## Findings Format

State:

- Impact.
- Exact location.
- Why Botble conventions make this unsafe or wrong.
- Minimal fix.
