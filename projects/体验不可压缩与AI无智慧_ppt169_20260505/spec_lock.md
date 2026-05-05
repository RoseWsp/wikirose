## canvas

- viewBox: 0 0 1280 720
- format: PPT 16:9

## colors

- bg: #0D1117
- secondary_bg: #161B22
- primary: #C9A96E
- accent: #4A9EFF
- secondary_accent: #8B5CF6
- text: #E6EDF3
- text_secondary: #8B949E
- text_tertiary: #484F58
- border: #30363D
- success: #3FB950
- warning: #F85149

## typography

- font_family: "Microsoft YaHei", "PingFang SC", Arial, sans-serif
- title_family: Georgia, SimSun, serif
- body_family: "Microsoft YaHei", "PingFang SC", Arial, sans-serif
- emphasis_family: Georgia, SimSun, serif
- code_family: Consolas, "Courier New", monospace
- body: 22
- title: 36
- subtitle: 28
- annotation: 16
- cover_title: 72
- hero_statement: 36

## icons

- library: chunk-filled
- inventory: user, robot, heart, shield, bolt, eye, star, cloud-rain, fire, door, lock-closed, target, book-open, sparkles, circle-checkmark

## images

- cover_bg: images/cover_bg.jpg
- mechanical_vs_flesh: images/mechanical_vs_flesh.jpg
- wall_not_door: images/wall_not_door.jpg

## page_rhythm

- P01: anchor
- P02: dense
- P03: dense
- P04: dense
- P05: breathing
- P06: dense
- P07: dense
- P08: breathing
- P09: dense
- P10: anchor

## forbidden

- Mixing icon libraries
- rgba()
- `<style>`, `class`, `<foreignObject>`, `textPath`, `@font-face`, `<animate*>`, `<script>`, `<iframe>`, `<symbol>`+`<use>`
- `<g opacity>` (set opacity on each child element individually)
- HTML named entities in text
