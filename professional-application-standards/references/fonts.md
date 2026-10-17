# Fonts

Read this before choosing any font. Use a font from the Approved list, a font the user specifies, or a font that passes every Font Criteria rule.

## Banned Fonts

Never use these as a UI, display or body font.

**Original bans:** Inter, Geist, Space Grotesk, and any monospace font (monospace is allowed only to display actual code).

**Lookalikes:** Inter Tight, Inter Display, Roboto Flex, DM Sans, Manrope, Plus Jakarta Sans, Satoshi, General Sans, Figtree, Outfit, Onest, Instrument Sans, Hanken Grotesk, Albert Sans, Be Vietnam Pro, Sora, Urbanist, Lexend, Geologica, Space Mono, JetBrains Mono, Geist Mono, IBM Plex Mono.

**System stack:** Do not rely on `system-ui`, `-apple-system` or similar system font stacks as the chosen typeface. They may appear only as a fallback.

## Font Criteria

A font not on the Approved list may be used only if it has none of the following:
- A monospace or code-derived design.
- A neutral grotesque or geometric UI design with a very tall x-height, tight apertures and uniform strokes built to resemble Inter, Geist or SF Pro.
- Squared, tech-styled geometric letterforms resembling Space Grotesk.
- A license that blocks free web use or self-hosting.
- Fewer than four weights (at least regular, medium, semibold and bold) for a primary typeface.
- Poor legibility at 14px and below.
- Missing Latin Extended character support.
- A novelty, display or script style when used for body text.

## Approved Fonts

All are open-licensed and work across platforms when self-hosted.

**Sans-serif:**
- Source Sans 3
- IBM Plex Sans
- Libre Franklin
- Fira Sans
- Red Hat Text (with Red Hat Display for headings)
- Lato
- Nunito Sans
- Open Sans
- Noto Sans
- Atkinson Hyperlegible

**Serif:**
- Source Serif 4
- Literata
- Lora
- Merriweather
- Newsreader

## Usage

- One main typeface, two maximum only if necessary (for example, a serif for headings with a sans-serif for body text).
- Self-host font files where the platform allows. In native apps, bundle the font files with the application.
- When code must be displayed, a monospace font may be used for the code only. Use the platform's default monospace stack rather than a branded code font from the banned list.
