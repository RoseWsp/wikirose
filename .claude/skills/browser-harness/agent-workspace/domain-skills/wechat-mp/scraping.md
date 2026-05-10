# WeChat Official Account (微信公众号) — Search, Browse & Scrape

Field-tested against mp.weixin.qq.com and weixin.sogou.com on 2026-05-03.
Requires login (via WeChat QR scan) for full Sogou search and article access; public article pages are accessible without auth via direct link.

---

## URL Patterns

| Page | URL | Notes |
|------|-----|-------|
| Article page | `https://mp.weixin.qq.com/s/{SN}` | `SN` is the article signature string; public access |
| Article page (short) | `https://mp.weixin.qq.com/s?__biz={BIZ}&mid={MID}&idx={IDX}&sn={SN}` | Full param form |
| Official account profile | `https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz={BIZ}` | Requires WeChat login |
| Sogou WeChat search | `https://weixin.sogou.com/weixin?type={TYPE}&query={QUERY}` | Type: 1=公众号, 2=文章 |
| WeChat Search (搜一搜) | `https://www.weixin.qq.com/` or via WeChat app | Desktop web access limited |

---

## Search Flow

### Sogou WeChat Search (recommended for automation)

Sogou hosts a web-accessible index of WeChat articles and accounts.

- **Search for accounts**: `https://weixin.sogou.com/weixin?type=1&query={ACCOUNT_NAME}`
- **Search for articles**: `https://weixin.sogou.com/weixin?type=2&query={KEYWORD}`

```python
# Search for a public account
new_tab("https://weixin.sogou.com/weixin?type=1&query=人民日报")
wait_for_load()

# Search for articles by keyword
new_tab("https://weixin.sogou.com/weixin?type=2&query=AI+大模型")
wait_for_load()
```

### Sogou search gotchas

- Sogou may show an anti-bot CAPTCHA page if requests are too frequent. If a CAPTCHA appears, wait and retry or solve it interactively.
- Search results paginate via `page={N}` query param: `https://weixin.sogou.com/weixin?type=2&query={KEYWORD}&page=2`
- Article search results show: title (clickable), account name, publish date, snippet.
- Account search results show: avatar, account name (clickable), WeChat ID (微信号), description, QR code.
- Clicking an account name in Sogou results opens the account's Sogou profile page, not the native WeChat profile. From there, recent articles are listed.

### WeChat native search (搜一搜)

- Native WeChat search (`搜一搜`) is primarily accessible within the WeChat app or desktop client.
- The web interface at `weixin.qq.com` has very limited search functionality; most queries redirect to the app.
- For automation, **prefer Sogou WeChat search** as the primary search method.

---

## Official Account Profile (公众号主页)

### Accessing via __biz parameter

Each public account has a unique `__biz` identifier (Base64-encoded). The profile page URL is:

```
https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz={BIZ}#wechat_redirect
```

- This URL **requires WeChat login** in the browser. Opening it in a regular Chrome session will show a login prompt.
- If the user has an active WeChat web session, the profile page shows the account's recent articles in an infinite-scroll list.

### Accessing via Sogou

- Sogou account pages (`https://weixin.sogou.com/link?q={...}`) list recent articles from a public account without requiring WeChat login.
- These pages are more automation-friendly than the native profile pages.

---

## Article Extraction

### Public article pages

Article pages at `mp.weixin.qq.com/s/{SN}` are publicly accessible. Key extraction points:

| Content | Selector / Method | Notes |
|---------|-------------------|-------|
| Title | `#activity-name` or `h1.rich_media_title` | Text content, may include whitespace |
| Author / Account name | `a.rich_media_meta_nickname` or `#profileBt .rich_media_meta_nickname` | The public account name |
| Publish time | `#publish_time` | Format: `YYYY-MM-DD HH:MM` |
| Body text | `#js_content` | The main article content div |
| Body as plain text | `js("document.getElementById('js_content')?.innerText")` | Clean text extraction |
| Body as HTML | `js("document.getElementById('js_content')?.innerHTML")` | Preserves formatting and images |
| Images | `#js_content img` | `data-src` attribute holds the real URL (not `src`) |
| Original flag | `.rich_media_meta_original_tag` or text "原创" | Indicates original content |
| Read count | `#read_area .read_num` | May require JS execution to populate |

### Image handling

- Article images use lazy loading: the `src` attribute is typically a placeholder, while `data-src` holds the actual image URL.
- To get all image URLs:
```python
images = js("""
Array.from(document.querySelectorAll('#js_content img'))
  .map(img => img.dataset.src || img.src)
  .filter(url => url && !url.startsWith('data:'))
""")
```
- Some image URLs may have referer restrictions. They can only be loaded from `mp.weixin.qq.com` context.

### Article metadata extraction helper

```python
def extract_article():
    """Extract key fields from a WeChat article page."""
    return js("""
    ({
        title: document.getElementById('activity-name')?.innerText?.trim(),
        author: document.querySelector('.rich_media_meta_nickname')?.innerText?.trim(),
        publish_time: document.getElementById('publish_time')?.innerText?.trim(),
        body_text: document.getElementById('js_content')?.innerText?.trim(),
        is_original: !!document.querySelector('.rich_media_meta_original_tag'),
        images: Array.from(document.querySelectorAll('#js_content img'))
            .map(img => img.dataset.src || img.src)
            .filter(url => url && !url.startsWith('data:'))
    })
    """)
```

---

## Sogou Search Results Extraction

### Article search results

```python
def extract_sogou_article_results():
    """Extract article results from Sogou WeChat search page."""
    return js("""
    Array.from(document.querySelectorAll('.news-list li')).map(item => ({
        title: item.querySelector('.txt-box h3 a')?.innerText?.trim(),
        url: item.querySelector('.txt-box h3 a')?.href,
        account: item.querySelector('.account')?.innerText?.trim(),
        date: item.querySelector('.s2')?.innerText?.trim(),
        snippet: item.querySelector('.txt-info')?.innerText?.trim()
    })).filter(r => r.title)
    """)
```

### Account search results

```python
def extract_sogou_account_results():
    """Extract account results from Sogou WeChat search page."""
    return js("""
    Array.from(document.querySelectorAll('.news-box .txt-box')).map(item => ({
        name: item.querySelector('h3 a')?.innerText?.trim(),
        wechat_id: item.querySelector('.info label')?.nextSibling?.textContent?.trim()?.replace(/^：/, ''),
        description: item.querySelector('.txt-gray')?.innerText?.trim(),
        url: item.querySelector('h3 a')?.href
    })).filter(r => r.name)
    """)
```

---

## Stable Cues

- Article page title element: `#activity-name`
- Article body container: `#js_content`
- Sogou article result list: `.news-list li`
- Sogou account result box: `.news-box .txt-box`
- Account profile recent articles: `.weui_media_box` or `.article_list`
- Publish date: `#publish_time`

---

## Interaction Notes

- **wait_for_load() is not enough** on article pages — rich media content (images, embedded videos) loads asynchronously. Add `wait(2)` after `wait_for_load()` before extracting.
- **Scroll to load more**: Sogou search results and account profile pages use infinite scroll. Scroll down to trigger loading more items.
- **Image loading**: Article images may not render until scrolled into view. Scroll through the article before extracting image URLs.
- **Anti-bot**: Sogou may show CAPTCHA if it detects automated access. Rate-limit requests and avoid rapid page loads.
- **WeChat login**: The native WeChat web login uses QR code scanning. There is no username/password flow. If login is required, the user must scan the QR code with their phone.

---

## Gotchas

- **`data-src` vs `src`** — article images use `data-src` for the real URL; `src` is often a placeholder or empty. Always prefer `data-src`.
- **Sogou CAPTCHA** — aggressive automation triggers anti-bot pages. If you see a CAPTCHA or redirect to `antispider` URL, pause and solve it or reduce request frequency.
- **Article URLs are session-bound** — some article links from Sogou search results are redirect URLs (`weixin.sogou.com/link?...`) that expire. If you need stable URLs, extract the `sn` parameter from the final `mp.weixin.qq.com` URL after following the redirect.
- **`__biz` is stable** — the `__biz` parameter uniquely identifies a public account and does not change. Cache it for future use.
- **No official web search** — WeChat does not provide a full-featured web search for articles. Sogou is the best available option for programmatic search.
- **Read count loads late** — the read count (阅读数) populates via an async JS call after page load. Wait at least 3-5 seconds or check for its presence before extracting.
- **Article body may be empty without proper load** — if `#js_content` has no content, the page may not have fully hydrated. Wait and re-check.
- **External links in articles** — WeChat articles may contain external links, but they are wrapped in a WeChat redirect URL (`mp.weixin.qq.com/mp/...`). The actual URL is in a query parameter.
