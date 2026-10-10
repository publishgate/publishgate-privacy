# PublishGate Privacy Policy

**Effective date:** 10 October 2026
**Developer:** PublishGate
**Contact:** publishgate.support@gmail.com

This policy describes version 0.1.0 of the PublishGate Chrome extension and how it handles information. It is written to match what the extension's code does.

## 1. The short version

- PublishGate checks the web page you choose to scan for common publishing mistakes, such as a missing title, missing image descriptions, placeholder text and weak links. The page is analysed **inside your browser**.
- **Nothing from the page is sent to the PublishGate developer.** PublishGate has no developer-operated server, no user accounts and no analytics.
- Before it looks at any page, PublishGate shows a disclosure inside the extension and asks for your consent. Until you agree it does not read your current tab or make any requests.
- The **only** network activity is an **optional link check**. It is **off by default**. If you turn it on, your browser sends requests to links on the **same website you are scanning**. Those requests can carry **that site's normal cookies** and **the full address of the page you scanned**, and the site's operator may log them. See section 7.

## 2. When consent is required, and when it is asked for again

- **First use.** The first time you open PublishGate, it shows a disclosure with two choices: **Agree and continue** and **Not now**. Opening the popup is not consent.
- **Before you agree,** PublishGate does not read your current tab's address or title, does not add its script to any page, shows nothing from any page, and makes no requests. **Not now** closes the popup and records nothing.
- **Disclosure versions.** The disclosure has a version number (currently 1). When a release changes what PublishGate reads, shows, stores or sends in a way the disclosure must describe, the version number is increased. Consent given to an earlier version is not valid for the new one: PublishGate treats it as no consent, deletes the saved consent and your saved link-check choice, shows the updated disclosure, and does not read your tab or make requests until you agree again.
- **If storage is unavailable.** If your browser blocks or cannot read PublishGate's local storage, or the saved consent is damaged, PublishGate behaves as if you had not consented and asks again.
- **Link checks are a separate choice.** Agreeing to the disclosure does not turn on link checks. The checkbox on the first-use screen starts unticked, and you can change it later with the checkbox beside the Scan button.

## 3. What PublishGate reads

PublishGate reads information only from the tab you opened it on (the active tab of your current window), and only after you have consented.

**Each time you open PublishGate on a page:** it reads the web address (URL) of the tab, adds its own script to the tab if it is not already there, and checks the page for signs that it was built with Webflow: attributes on the page's `<html>` element, the page's "generator" meta tag, the addresses of its scripts, linked files (such as stylesheets) and images, its host name, and some Webflow-specific class names.

**When you press Scan this page,** it reads from the page:

- the page's address and title;
- the meta description, robots and generator tags;
- every image: its address, `alt` text, role, class names, displayed size, whether it sits inside a link, button or captioned figure, short text in the container around it (up to 200 characters), and whether a nearby video is muted or has controls;
- every link: its address, visible text, accessible label, title, role, accessibility attributes, the *names* of event-handler and `data-` attributes, and class names;
- the page's text, including text that is currently hidden, searched for placeholder phrases such as "Lorem ipsum", "TODO", "TBD" and "replace this text". Text inside script, style, `<textarea>`, code and similar elements is skipped;
- on Webflow pages, the text of Webflow's built-in form-message and empty-collection elements.

It inspects the main page only. Content inside embedded frames (iframes) and shadow DOM is not scanned. Reading is not editing: PublishGate does not change your page, except that when you click "Show on page" it briefly (about four seconds) draws an outline around the affected element.

## 4. What PublishGate shows

Results appear **only in the PublishGate popup on your screen.** They include finding titles and explanations; short excerpts from the page (the HTML of an affected image, link or tag, up to about 180 characters; text around a placeholder phrase, up to about 120 characters; nearby text quoted up to about 60 characters); link addresses; a short path to the affected element; the site's host name (the full address appears when you hover over it); and counts.

Because these come from the page, they can contain whatever the page contains, including personal information or tokens that appear in a link address or page text. They are not sent anywhere by PublishGate, but anyone who can see your screen, or a screenshot of the results, can see them. Do not share results from private pages.

## 5. What PublishGate does not access

- **Form field values.** PublishGate's code never reads what is typed or selected in form fields (the values of inputs, textareas or selects), and it skips the contents of `<textarea>` elements. It does read ordinary text that a page displays, which can include the visible text of labels, buttons and options.
- **Cookies, read directly.** PublishGate never reads cookies. It does not use the browser's cookie interface or `document.cookie`. (When link checks are on, your browser itself attaches cookies to requests; see section 7.)
- **Other tabs.** It does not read or message tabs other than the one you opened it on.
- **Browsing history.** It does not use the browser's history, bookmarks or downloads features, and it keeps no history of the pages you scan.
- **Other stored data.** It does not read a page's local storage, session storage or databases.

Its permissions are limited to `activeTab` (temporary access to the tab you opened it on) and `scripting` (to add its own packaged script to that tab). It requests no permission to access websites in general.

## 6. What is stored, and for how long

**Saved on your device.** PublishGate saves two entries in the extension's own `localStorage` in your browser profile:

| Key | Contents |
| --- | --- |
| `publishgate.consent` | The disclosure version you agreed to and the time you agreed. |
| `publishgate.linkChecks` | `true` or `false`: whether link checks are on. Anything other than `true` means off. |

An older setting called `publishgate.verifyLinks` from earlier development builds is ignored and deleted. PublishGate does not use `chrome.storage`, cookies or a database, and it writes no scan results to disk. PublishGate does not encrypt these two entries. Removing the extension or clearing its data may erase them, in which case you are asked again; whether and when your browser does this is outside PublishGate's control.

**Scan results.** Results are held in the memory of the scanned tab, in PublishGate's script, so that reopening the popup can show the last result. They are discarded when you reload or close the tab, when you scan again (the new result replaces the old one), or when you withdraw consent. On a single-page site that changes address without reloading, an old result can stay in the tab's memory until the tab is reloaded or closed, but the popup only shows a result for the exact address that was scanned. The popup keeps results only while it is open.

## 7. Optional link checks

Link checks are the only thing PublishGate does that sends data over the network. They are **disabled by default** and run only if you tick the link-check checkbox, either on the first-use screen or beside the Scan button, and then press Scan. Unticking the checkbox stops link checks in later scans. Withdrawing consent also asks any link check already in progress to stop (section 10).

**Which links are requested.**
- Only links to the **same origin** as the scanned page: the same scheme (http or https), host and port. External links, other subdomains and a `www` or non-`www` variant of the host are not requested. Link checks run only on http and https pages.
- Each distinct address (ignoring any `#fragment`) is checked at most once per scan, and at most **40** distinct addresses are checked per scan. Any further links are not checked. "Checked once" can mean two requests: a `HEAD` and, in the cases described below, one confirming `GET`.

**Links that are skipped.** PublishGate does not request:
- addresses containing a username or password;
- links with an attribute that marks them as actions: `download`, `onclick`, `data-method`, `data-confirm`, `data-remote`, `data-turbo-method`, `data-turbo-confirm`, `data-action`, `hx-post`, `hx-delete`, `hx-put` or `hx-patch`;
- addresses whose path or query contains words such as `logout`, `signout`, `sign-off`, `delete`, `destroy`, `remove`, `unsubscribe`, `opt-out`, `cancel`, `reset`, `confirm`, `verify`, `activate`, `approve`, `revoke`, `disable`, `unlink`, `invite`, `add-to`, `cart/add`, `checkout`, `purchase`, `/api/`, `/admin` or `/wp-admin`. Matching is by text, so some ordinary pages are skipped too;
- addresses with a query parameter named `token`, `access_token`, `key`, `api_key`, `code`, `auth`, `otp`, `sig`, `signature`, `session`, `sid`, `nonce`, `secret`, `password`, `pwd`, `hash`, `invite` or `magic`.

If any link to an address is of one of these kinds, that address is not requested at all. The number of skipped links is shown in the results.

**How they are requested.**
- PublishGate sends a **`HEAD`** request. Only if the answer is 404, 405, 410 or 501 (and is not a redirect) does it send **one `GET`** request to the same address to confirm. It reads only the status code and asks the browser to discard the response body.
- **Redirects are not followed.** A redirect is treated as "the link responds", and the address it points to is not requested. This is so that a link on the scanned site can never cause a request to a different site.
- Each request times out after **6 seconds**. Up to **6** requests run at the same time. After **30 seconds** in total, no new request is started; links not reached are reported as not checked.
- Requests are made with the browser's **"no-store" cache mode**, which tells the browser not to answer from its HTTP cache and not to save the response, so they reach the website.

**What the website receives.** Your browser makes these requests from the scanned page's context, so they are sent the way requests from that page would be:
- **The site's normal cookies.** The browser attaches the cookies it holds for that site, including cookies that page scripts cannot read (HttpOnly cookies). PublishGate does not read these cookies; the browser adds them. In testing, link-check requests carried the site's cookies, including an HttpOnly one.
- **The `Referer` header.** Depending on the scanned page's referrer policy, this header may contain the full scanned page URL, including its path and query string but not its fragment; it may contain only the origin; or it may be omitted. In our Chrome test, a page that set a `no-referrer` policy omitted this header, while cookies were still sent.
- The browser's usual request headers, which in testing included `Sec-Fetch-Site: same-origin` and `Sec-Fetch-Mode: cors`.
- If the page is served over plain `http`, these requests are plain `http` too.

**The website's operator may log these requests.** The operator receives them as ordinary requests from your browser and can record them, together with the cookies and the `Referer` they carry, in server logs or other tools. That can include personal data or tokens in the scanned page's address or in cookies. No one at PublishGate receives them.

**They are not guaranteed to be harmless.** The requests are meant to be read-only, and PublishGate skips links that look like actions. But it cannot know how a particular website behaves. A site might react to a `HEAD` or `GET` request in unexpected ways, for example by changing something, counting a visit, raising an alert or applying a rate limit, and the skip rules are based on text patterns that can miss unusual sites. Leave link checks off for sites where that matters to you.

## 8. Developer servers, accounts, analytics and sharing

- PublishGate has no developer-operated server that receives data from the extension, no account or sign-in, and no analytics, advertising or error-reporting service.
- No scan result, page content, address, setting or identifier is sent to the developer or to any third party by PublishGate. The extension's only network requests are the same-origin link checks in section 7, which go to the site you are scanning.
- PublishGate does not sell user data, does not use it for advertising, and does not use it to assess creditworthiness or for lending. Information read from a page is used only to show you findings about the page you chose to scan (and, for link checks, to make the requests described above).
- All of PublishGate's code is included in the extension package. It does not download or run code from elsewhere.

## 9. Third-party libraries and licences

PublishGate bundles three open-source libraries, all under the MIT licence: **React 19.3.0**, **React DOM 19.3.0** and **Scheduler 0.28.0** (used by React DOM). Their licence texts are included in the file `THIRD_PARTY_NOTICES.txt` in the extension package. These libraries run inside the extension on your device; they are not services and do not send data anywhere.

## 10. Withdrawing consent

You can review the full disclosure at any time with the **Privacy** button in the popup. **Withdraw consent and reset** there:
- deletes both saved entries described in section 6 (so link checks are off again);
- clears the popup's state and returns it to the first-use screen;
- asks the PublishGate script in the tab you were using to discard the scan results it holds and to stop any link checks still running. This is best-effort: if the page has already been reloaded or closed, nothing is held. The script itself stays loaded in that tab until it is reloaded, but it holds no results and does nothing unless the extension messages it.

After withdrawing, PublishGate does not read your tab or make requests until you agree again. Withdrawing does not undo requests already sent to a website; those are in that site's own records.

## 11. Security limitations

- PublishGate has no servers of its own, so there is no developer-side copy of your data to secure.
- It does not add its own encryption. The two saved entries are stored unencrypted in your browser profile, and scan results exist in the tab's memory and on screen while you use PublishGate. Anyone or any software with access to your browser, profile or screen could see them.
- Link checks use the same scheme as the links on the page, so on an `http` site they are not encrypted.
- Protections such as the skipped-link rules are heuristics, not guarantees.
- How Chrome and Google handle data in your browser is governed by their own terms and policies, not this one.

## 12. Chrome Web Store user data policy

PublishGate is intended to comply with the Chrome Web Store User Data Policy, including its Limited Use requirements: it uses page information only for its single purpose of showing you findings about the page you scan, and does not transfer or sell it. This is a statement of how PublishGate is designed to behave and is not a guarantee of any decision by Google.

## 13. Changes to this policy

If this policy changes, the new version will be published at the same address with a new effective date. If a release changes what PublishGate reads, shows, stores or sends, the in-product disclosure is updated and its version number increased, so that earlier consent no longer applies and you are asked again before the changed handling takes place (section 2).

## 14. Contact

For privacy questions, contact **publishgate.support@gmail.com**.
