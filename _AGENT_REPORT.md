# Agent Report — SEO / OG / hreflang head-custom + jekyll-sitemap

**Branch:** ship2/MOhead  
**Date:** 2026-05-31  
**Agent:** ship-hardening (MOhead)

---

## Tasks completed

### 1. Full SEO head-custom (`_includes/head-custom.html`)

Previous state: ~27 lines — lang-bar CSS/JS + founder footer only. Zero OG/meta/schema/hreflang.

Ported the dysphagia-knowledge-hub template with these medicated-oil-specific substitutions:

| Item | Value |
|---|---|
| `site_url` | `https://yaoyoudaquan.cn` |
| `og:site_name` | `藥油大全 yaoyoudaquan.cn` |
| Organization name | `藥油大全知識庫` |
| Organization description | `香港常用藥油品牌、成分、用法、地區特色 — 完整知識庫。文化教育內容，CC BY 4.0。` |
| WebSite name | `藥油大全 — 香港藥油知識庫` |
| hreflang locales | `zh-Hans` / `zh-Hant-HK` / `en` + `x-default → /zh-hans/` |
| `og:image` | `/assets/img/og-default.png` (sibling agent generates this) |

Blocks added:
- Meta description (from `page.description`)
- Canonical link (from `page.canonical`)
- OpenGraph (title / description / type / url / image / site_name / locale)
- Twitter Card (summary_large_image)
- hreflang loop — explicit links for all 3 locales + x-default (zh-Hans is primary)
- Schema: Article (conditional on `page.title`)
- Schema: BreadcrumbList (conditional on `page.category and page.title`)
- Schema: Organization (every page)
- Schema: WebSite (every page)
- GSC + Baidu verification placeholders (commented out)

Bug avoided: existing lang-bar `innerHTML` already used double-quote style (`style="color:#666"`) — preserved as-is, no single-quote regression introduced.

`功效`/`治疗` cultural/educational content and disclaimers: untouched (no new health claims added).

### 2. jekyll-sitemap plugin

- `Gemfile`: added `gem "jekyll-sitemap"`
- `_config.yml`: added `plugins: [jekyll-sitemap]` block

The existing manual `sitemap.xml` is left in place; it will be superseded at build time by the plugin-generated version. No content was removed.

### 3. Build safety

- Valid Liquid throughout (all tags balanced, no raw/endraw issues)
- Valid YAML in `_config.yml` (indentation confirmed)
- No new health claims added; existing educational disclaimers untouched

---

## Files changed

- `_includes/head-custom.html` — 27 → 138 lines (full SEO block added)
- `Gemfile` — added `gem "jekyll-sitemap"`
- `_config.yml` — added `plugins:` section

## Next steps (for deploy agent)

- Set real GSC + Baidu verification tokens in `head-custom.html` (currently commented placeholders)
- `assets/img/og-default.png` — DONE (see OG Image section below)
- Run `bundle install` in the worktree to lock `jekyll-sitemap` into `Gemfile.lock`

---

# Agent Report — OG Image (og-default.png)

**Branch:** ship2/MOog  
**Date:** 2026-05-31  
**Agent:** ship-hardening (MOog)

## Task completed

Created a branded 1200×630 OG image at `assets/img/og-default.png`.

### Design
- **Palette:** deep dark brown (#3E200A) gradient background, amber (#C2701C / #E09B3C), gold (#D4AF37), cream (#FFF8DC)
- **CJK font:** PingFang TC Medium (system font from `/System/Library/AssetsV2/.../PingFang.ttc`) — full CJK rendered without tofu
- **Content:**
  - Main title: 藥油大全 (160 pt, cream)
  - Tagline: 香港藥油文化知識庫 (42 pt, gold)
  - URL: yaoyoudaquan.cn (36 pt, amber)
  - Disclaimer label: 文化資料 · 非醫療建議 (24 pt, cream-dim)
- **Decoration:** double-border frame, corner diamond ornaments, flanking vertical bars, horizontal divider with centre diamond
- **Generation method:** Python Pillow (PIL) script — fully reproducible, no health claims

### Verification
```
python3 -c "from PIL import Image; im=Image.open('assets/img/og-default.png'); print(im.size, im.format)"
# → (1200, 630) PNG  ✓
```

## Files changed

- `assets/img/og-default.png` — new file, 1200×630 PNG

## Commit

`735d6d7 feat(og): branded 1200x630 og-default.png`
