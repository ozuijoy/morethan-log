# morethan-log

<img width="1715" alt="image" src="https://user-images.githubusercontent.com/72514247/209824600-ca9c8acc-6d2d-4041-9931-43e34b8a9a5f.png">

Next.js static blog using Notion as a Content Management System (CMS). Supports both Blog format Post as well as Page format for Resume. Deployed using Vercel, Cloudflare Pages, or Netlify.

[Demo Blog](https://morethan-log.vercel.app) | [Demo Resume](https://morethan-log.vercel.app/resume)

## Features

**📒 Writing posts using notion**

- No need of commiting to Github for posting anything to your website.
- Posts made on Notion are automaticaly updated on your site.

**📄 Use as a page as resume**

- Useful for generating full page sites using Notion.
- Can be used for Resume, Portfolios etc.

**👀 SEO friendly**

- Dynamically generates OG IMAGEs (thumbnails!) for posts. ([og-image-korean](https://github.com/morethanmin/og-image-korean)).
- Dynamically creates sitemap for posts.

**🤖 Customisable and Supports various plugin through CONFIG**

- Your profile information can be updated through Config. (`site.config.js`)
- Plugins support includes, Google Analytics, Search Console and also Commenting using Github Issues(Utterances) or Cusdis.

## Getting Started

1. Star this repo.
2. [Fork](https://github.com/ozuijoy/morethan-log/fork) the repo to your profile.
3. Duplicate [this Notion template](https://morethanmin.notion.site/12c38b5f459d4eb9a759f92fba6cea36?v=2e7962408e3842b2a1a801bf3546edda), and share to web.
4. Copy the web link and keep note of the Notion Page ID from the link, which will be in this format: `username.notion.site/NOTION_PAGE_ID?v=VERSION_ID`.
5. Clone your forked repo and customize `site.config.js` based on your preference.
6. Deploy on your preferred platform (see below).

### Required Environment Variables

All platforms require the following environment variable:

- **`NOTION_PAGE_ID`** (Required): The Notion page ID from the Share to Web URL. Only the ID portion, not the entire URL.

Optional environment variables (for plugins in `site.config.js`):

- `NEXT_PUBLIC_GOOGLE_MEASUREMENT_ID` — Google Analytics
- `NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION` — Google Search Console
- `NEXT_PUBLIC_NAVER_SITE_VERIFICATION` — Naver Search Advisor
- `NEXT_PUBLIC_UTTERANCES_REPO` — Utterances comments
- `TOKEN_FOR_REVALIDATE` — On-demand revalidation webhook (Netlify only)

---

### Deploy to Vercel

The `main` branch is configured for Vercel (static export).

1. Go to [vercel.com](https://vercel.com) → **Add New** → **Project**
2. Import `ozuijoy/morethan-log` (or your fork)
3. Select branch: `main`
4. Set environment variables (`NOTION_PAGE_ID` + optional ones)
5. Click **Deploy**

**Notes:**
- `output: 'export'` is set in `next.config.js` — Vercel auto-detects the `out/` directory
- No ISR, API routes, or Next.js image optimization (static site)
- Content updates require a redeploy (push a commit to trigger a rebuild)

---

### Deploy to Cloudflare Pages

The `main` branch is configured for Cloudflare Pages (static export).

1. Go to Cloudflare Dashboard → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
2. Select your fork of `morethan-log`
3. Configure build settings:
   - **Framework preset:** Next.js (or None)
   - **Build command:** `yarn build`
   - **Build output directory:** `out`
4. Set environment variables (`NOTION_PAGE_ID` + optional ones)
5. Click **Save and Deploy**

**Notes:**
- `output: 'export'` is set in `next.config.js` — static output goes to `out/`
- No ISR, API routes, or Next.js image optimization (static site)
- Content updates require a redeploy (push a commit to trigger a rebuild)

---

### Deploy to Netlify

The `netlify` branch is configured for Netlify (server runtime with full features).

1. Go to [app.netlify.com](https://app.netlify.com) → **Add new site** → **Import an existing project**
2. Import from Git: `ozuijoy/morethan-log` (or your fork)
3. **Select branch: `netlify`** (not `main`)
4. `netlify.toml` is already configured — no manual build settings needed
5. Set environment variables:
   - `NOTION_PAGE_ID` (Required)
   - `TOKEN_FOR_REVALIDATE` (Optional — enables `/api/revalidate` webhook)
   - Optional plugin variables (GA, Utterances, etc.)
6. Click **Deploy site**

**Notes:**
- `output: 'standalone'` is set in `next.config.js` — server runtime supports full Next.js features
- ✅ ISR: Posts revalidate every 7 days automatically (configurable via `revalidateTime` in `site.config.js`)
- ✅ API routes: `/api/revalidate` webhook available for on-demand updates
- ✅ Next.js image optimization enabled
- Uses `@netlify/plugin-nextjs` (configured in `netlify.toml`)

---

### Platform Comparison

| Feature | Vercel (`main`) | Cloudflare Pages (`main`) | Netlify (`netlify`) |
|---|---|---|---|
| Build mode | Static export | Static export | Standalone (server) |
| ISR auto-refresh | ❌ | ❌ | ✅ (7 days) |
| `/api/revalidate` webhook | ❌ | ❌ | ✅ |
| Next.js image optimization | ❌ | ❌ | ✅ |
| SSR sitemap | ❌ | ❌ | ✅ |
| Git trigger deploy | ✅ | ✅ | ✅ |

**Recommendation:** Use the `netlify` branch if you want automatic post updates without redeploying. Use `main` for Vercel or Cloudflare Pages if you prefer those platforms and don't mind redeploying to update content.

## FAQ

<details>
   <summary> Click to see FAQ </summary>
   Q1: If you finish making avatar.svg, How to make favicon.ico and apple-touch-icon.png?
   
   A1: check out https://www.favicon-generator.org/
   
   Q2: Is it necessary to set up a sitemap file?   
   A2: The system will dynamically create a sitemap.xml, so there is no need for manual setup.

   Q3: Why don’t Notion posts update automatically?   
   A3: Please set the revalidateTime in site.config.js and observe how long it takes to update.
   
   Q4: What should be entered for NEXT_PUBLIC_GOOGLE_MEASUREMENT_ID and NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION in site.config.js?
   A4: You can check https://github.com/morethanmin/morethan-log/issues/203. Please note that updates may take some time to take effect after setting.

If you encounter any other issues, please feel free to add them to the GitHub README to assist future users. We look forward to your contributions!

</details>

## Contributing

Check out the [Contributing Guide](.github/CONTRIBUTING.md).

### Contributors

<!--
Contributors template:
<a href="https://github.com/{username}"><img src="{src}" width="50px" alt="{username}" /></a>&nbsp;&nbsp;
-->

<a href="https://github.com/morethanmin/morethan-log/graphs/contributors">
<img src="https://contrib.rocks/image?repo=morethanmin/morethan-log" />
</a>

## Support

morethan-log is an MIT-licensed open source project. It can grow thanks to the sponsors and support from the amazing backers.

### Sponsors

<!--
Sponsors template:
<a href="https://github.com/{uesrname}"><img src="{src}" width="50px" alt="{username}" /></a>&nbsp;&nbsp;
-->

<p>
<a href="https://github.com/siyeons"><img src="https://avatars.githubusercontent.com/u/35549653?v=4" width="50px" alt="siyeons" /></a>&nbsp;&nbsp;
</p>

## License

The [MIT License](LICENSE).
