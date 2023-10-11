# Styler

Tool to generate CSS classes, a bit like tailwind but less strict.

For cases where we cannot use tailwind because of whatever
constraints, e.g.: using Shiny forcing Bootstrap.

Styler will scan for `class=""`.

```html
<!--src/file.html-->
<div class="m-2 b-r-2 b-c-red b-w-1 pos-rel">
    <h1 class="t-bold t-red-400">Hello</h1>
</div>
```

```bash
styler -dir=src -out=styles.css -warn=false
```

## Install

```bash
go install github.com/devOpifex/styler
```

## Shorthands

You don't have to use the shorthands, 
e.g.: `d-f` and `display-flex` are both correct.
They simply translate to something else in the generated
CSS.

- `b`: `border`
- `c`: `color`
- `s`: `size`
- `r`: `radius`
- `m`: `margin`
- `p`: `padding`
- `w`: `width`
- `f`: `flex`
- `a`: `align`
- `j`: `justify`
- `i`: `items`
- `t`: `font` (text)
- `bk`: `background` (bg taken in many frameworks)
- `d`: `display`
- `pos`: `position`
- `rel`: `relative`
- `abs`: `absolute`
- `full`: `100%`
- `ov`: `overflow`
- `sh`: `shadow`

## How it works

- Special case for shadow takes `sm`, `md`, or `lg` suffixes.
- Support for `x`, `y`, `t`, and `b`, e.g.: `p-x-2`
- Tailwind's `hover:`, and `focus:` pseudo classes
- All tailwind's colors included, e.g.: `t-red-100`
- The last item in the string of attributes separated by `-` is the value, 
e.g.: `background-color-red` translates to `background-color:red;`
- Numeric values are divided by 4 and treated as `rem`, e.g.: `b-r-2` translates
to `border-radius:.25rem`, except for values `50` and `100` which are
treated as percentages.

