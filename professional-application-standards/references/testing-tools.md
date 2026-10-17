# Testing Tools

Read this before testing performance, accessibility or security.

## Web Applications

| Area | Tools |
|---|---|
| Layout, interaction and visual checks | Playwright (or another headless browser) |
| Page performance | Lighthouse, PageSpeed Insights, WebPageTest |
| Accessibility | axe-core, WAVE, Lighthouse Accessibility |
| Colorblindness | Chrome DevTools rendering emulation |
| Bundle size | vite-bundle-visualizer or webpack-bundle-analyzer (in build only) |
| Memory leaks | Chrome DevTools Memory panel (heap snapshots) |
| API and backend load | k6 |
| Database | Supabase Performance Advisor, `EXPLAIN ANALYZE`, `pg_stat_statements` |
| Database security | Supabase Security Advisor |
| Security headers | Mozilla HTTP Observatory, securityheaders.com |
| HTTPS and certificates | SSL Labs |
| Dependencies | `npm audit`, GitHub Dependabot |
| Secrets | Gitleaks |
| Production errors (optional) | Sentry, configured to strip personal data |

## Native and Desktop Applications

| Area | Tools |
|---|---|
| iOS and macOS accessibility | Xcode Accessibility Inspector |
| Android accessibility | Android Accessibility Scanner |
| iOS and macOS performance and memory | Xcode Instruments |
| Android performance and memory | Android Studio Profiler |
| Windows accessibility | Accessibility Insights for Windows |
| Desktop (Electron or Tauri) | Chrome DevTools for the web layer, plus the platform tools above |

## When a Tool Is Unavailable

If a tool cannot run in the current environment, run the static checks that can, and list the rest under "Unverified checks" in the delivery summary.
