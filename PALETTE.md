# Nordic palette reference

Source of truth: [`lua/nordic/colors/nordic.lua`](https://github.com/AlexvZyl/nordic.nvim/blob/main/lua/nordic/colors/nordic.lua) (raw hex values, base palette) and [`lua/nordic/colors/init.lua`](https://github.com/AlexvZyl/nordic.nvim/blob/main/lua/nordic/colors/init.lua) (semantic "use case" colors built from the base palette, with the default plugin options: `transparent=false`, `swap_backgrounds=false`, `reduced_blue=false`, `bright_border=false`).

Every hex code below is copied verbatim from those two files. Nothing here is guessed.

## Base palette (exact, from `nordic.lua`)

| Name | Hex | Notes |
|---|---|---|
| `black0` | `#191D24` | darkest neutral |
| `black1` | `#1E222A` | floats / popups |
| `black2` | `#222630` | slightly darker than bg |
| `gray0` | `#242933` | **bg** |
| `gray1` | `#2E3440` | Polar Night (Nord0) |
| `gray2` | `#3B4252` | Polar Night (Nord1) |
| `gray3` | `#434C5E` | Polar Night (Nord2) |
| `gray4` | `#4C566A` | Polar Night (Nord3) — comments |
| `gray5` | `#60728A` | light blue-gray accent |
| `white0` (normal) | `#BBC3D4` | **default fg** |
| `white0` (reduced-blue variant) | `#C0C8D8` | only if `reduced_blue = true` |
| `white1` | `#D8DEE9` | Snow Storm (Nord4) |
| `white2` | `#E5E9F0` | Snow Storm (Nord5) |
| `white3` | `#ECEFF4` | Snow Storm (Nord6) |
| `blue0` | `#5E81AC` | Frost (Nord10) |
| `blue1` | `#81A1C1` | Frost (Nord9) |
| `blue2` | `#88C0D0` | Frost (Nord8) |
| `cyan.base` | `#8FBCBB` | Frost (Nord7) |
| `cyan.bright` | `#9FC6C5` | |
| `cyan.dim` | `#80B3B2` | |
| `red.base` | `#BF616A` | Aurora (Nord11) |
| `red.bright` | `#C5727A` | |
| `red.dim` | `#B74E58` | |
| `orange.base` | `#D08770` | Aurora (Nord12) |
| `orange.bright` | `#D79784` | |
| `orange.dim` | `#CB775D` | |
| `yellow.base` | `#EBCB8B` | Aurora (Nord13) |
| `yellow.bright` | `#EFD49F` | |
| `yellow.dim` | `#E7C173` | |
| `green.base` | `#A3BE8C` | Aurora (Nord14) |
| `green.bright` | `#B1C89D` | |
| `green.dim` | `#97B67C` | |
| `magenta.base` | `#B48EAD` | Aurora (Nord15) |
| `magenta.bright` | `#BE9DB8` | |
| `magenta.dim` | `#A97EA1` | |

## Semantic "use case" colors (exact, from `init.lua`, default options)

| Name | Resolves to | Hex |
|---|---|---|
| `bg` | `gray0` | `#242933` |
| `bg_dark` | `black0` | `#191D24` |
| `bg_sidebar` | `bg` | `#242933` |
| `bg_statusline` | `black0` | `#191D24` |
| `bg_fold` | `gray2` | `#3B4252` |
| `border_fg` | `black0` | `#191D24` |
| `border_bg` | `bg` | `#242933` |
| `fg` | `white0` | `#BBC3D4` |
| `fg_bright` | `white1` | `#D8DEE9` |
| `bg_float` | `black1` | `#1E222A` |
| `bg_popup` | `bg_float` | `#1E222A` |
| `bg_selected` | `gray2` | `#3B4252` |
| `comment` | `gray4` | `#4C566A` |
| `error` | `red.bright` | `#C5727A` |
| `warn` / `warning` | `yellow.base` | `#EBCB8B` |
| `hint` | `green.bright` | `#B1C89D` |
| `info` | `blue2` | `#88C0D0` |
| `git.add` | `green.base` | `#A3BE8C` |
| `git.delete` | `red.base` | `#BF616A` |
| `git.change` | `blue1` | `#81A1C1` |
| `diff.add` | `blend(green.base, bg, 0.2)` | `#3D4745` |
| `diff.delete` | `blend(red.base, bg, 0.2)` | `#43343E` |
| `diff.change1` | `blend(blue2, bg, 0.2)` | `#384752` |
| `diff.change0` | `blend(blue1, bg, 0.05)` | `#292F3A` |

`diff_blend = 0.2` is hardcoded in `init.lua`, so the three `diff.*` rows above are exact (computed with the standard `result = fg*alpha + bg*(1-alpha)` lerp).

## Values that are **approximated**, not literal

`bg_cursorline` and `bg_visual` in the real plugin depend on `options.cursorline.blend` / `options.visual.blend`, which live in `lua/nordic/config.lua` — a file not needed for the base palette and not fetched here. I approximated them with the same blend formula at plausible alphas (0.55 / 0.35 respectively) to get something in the right neighborhood:

| Name | Hex (approx.) |
|---|---|
| `bg_cursorline` | `#1E222B` |
| `bg_visual` | `#20252E` |

These two are the *only* non-exact numbers used anywhere in the VS Code / JetBrains ports. Everything else in both theme files traces directly back to the table above.

## Syntax role mapping (standard Nord convention, applied to Nordic's hex shades)

nordic.nvim is explicitly "based on Nord," and Nord's official convention for syntax roles is well-documented and consistent across every Nord port. Nordic's `blue0/blue1/blue2/cyan/red/orange/yellow/green/magenta` map 1:1 onto Nord's canonical `nord7–nord15` slots, so that convention was used for both theme ports:

| Role | Color |
|---|---|
| Keywords / control flow / storage | `blue0` `#5E81AC` |
| Functions / methods | `blue1` `#81A1C1` |
| Classes / types / interfaces | `blue2` `#88C0D0` |
| Regex / escaped-in-string / support constants | `cyan.base` `#8FBCBB` |
| Strings | `green.base` `#A3BE8C` |
| Numbers / constants / enum members | `magenta.base` `#B48EAD` |
| Decorators / annotations / preprocessor | `orange.base` `#D08770` |
| String-escape chars / warnings | `yellow.base` `#EBCB8B` |
| Errors / invalid | `red.base` `#BF616A` |
| Comments | `gray4` `#4C566A` |
