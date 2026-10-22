# Testing Tools

Read this before testing performance, accessibility or security.

## Web Applications

| Area | Tools |
|---|---|
| Layout, interaction and visual checks | Playwright, run in Chromium, Firefox and WebKit |
| Links | lychee or linkinator |
| HTML validity | W3C Nu HTML Checker |
| Page performance (public pages) | PageSpeed Insights (mobile and desktop scores), WebPageTest |
| Page performance (login-only or undeployed pages) | Lighthouse or Lighthouse CI with mobile and desktop emulation |
| Real-user performance | Search Console Core Web Vitals report |
| Accessibility | axe-core, WAVE, Lighthouse Accessibility, Playwright accessibility tree snapshots |
| Screen readers | VoiceOver (macOS and iOS), NVDA, JAWS, TalkBack (manual, builder task) |
| Colorblindness | Chrome DevTools rendering emulation |
| Structured data | Google Rich Results Test, Schema Markup Validator |
| Link previews | Facebook Sharing Debugger, LinkedIn Post Inspector |
| Bundle size | vite-bundle-visualizer or webpack-bundle-analyzer (in build only) |
| Memory leaks | Chrome DevTools Memory panel (heap snapshots) |
| API and backend load | k6 |
| Database | Supabase Performance Advisor, `EXPLAIN ANALYZE`, `pg_stat_statements` |
| Database security | Supabase Security Advisor |
| Headers and caching | `curl -I`, Mozilla HTTP Observatory, securityheaders.com |
| HTTPS and certificates | SSL Labs |
| Dependencies | `npm audit`, GitHub Dependabot |
| Secrets | Gitleaks |
| Image and GIF optimization | ffmpeg, gifsicle, SVGO |
| Production errors (optional) | Sentry, configured to strip personal data |

## Native and Desktop Applications

| Area | Tools |
|---|---|
| iOS and macOS accessibility | Xcode Accessibility Inspector |
| Android accessibility | Android Accessibility Scanner |
| iOS and macOS performance and memory | Xcode Instruments, Xcode Organizer metrics |
| Android performance and memory | Android Studio Profiler, Android vitals |
| Windows accessibility | Accessibility Insights for Windows |
| Desktop (Electron or Tauri) | Chrome DevTools for the web layer, plus the platform tools above |

## When a Tool Is Unavailable
If a tool cannot run in the current environment, run the static checks that can, and list the rest under "Unverified checks" in the delivery summary.
