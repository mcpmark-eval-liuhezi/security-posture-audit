# Security Posture Audit — HeziLiu GitHub Account

Quarterly security review snapshot, compiled from live GitHub API queries on 2026-10-22.

## 1. Account profile (exactly as the API reported)

- **Login:** `HeziLiu`
- **Public repository count (`public_repos`):** 4
- Profile: https://github.com/HeziLiu

## 2. Repository inventory (4 repositories)

| # | Repository | Kind | Default branch | Description |
|---|---|---|---|---|
| 1 | HeziLiu/Little-rookie | Source | master | "Undergraduate coursework" (Java) |
| 2 | HeziLiu/Big-Buzzard | Source | master | "For future...." |
| 3 | HeziLiu/CodingInterviewChinese2 | Fork | master | 《剑指Offer》第二版源代码 (C++) |
| 4 | HeziLiu/awesome-chatgpt-prompts-zh | Fork | main | ChatGPT 中文调教指南 |

Note: the default repository search returns only non-fork repositories (2 results); the remaining 2 were recovered with a fork-inclusive search, bringing the inventory to 4 — matching the profile's `public_repos` count of 4.

## 3. Per-repository scanning findings

Each repository was checked for open code scanning alerts and open secret scanning alerts (8 checks total). **Every check was refused by the GitHub API with `403 Resource not accessible by personal access token`** — the audit token does not carry the security-events scope needed to read these endpoints. No alert data (not even an empty list) could be returned for any repository. These are access failures, not clean results: **no repository may be treated as verified-clean on this evidence.**

| Repository | Open code scanning alerts | Open secret scanning alerts |
|---|---|---|
| HeziLiu/Little-rookie | Not retrievable — API returned 403 "Resource not accessible by personal access token" | Not retrievable — API returned 403 "Resource not accessible by personal access token" |
| HeziLiu/Big-Buzzard | Not retrievable — same 403 | Not retrievable — same 403 |
| HeziLiu/CodingInterviewChinese2 | Not retrievable — same 403 | Not retrievable — same 403 |
| HeziLiu/awesome-chatgpt-prompts-zh | Not retrievable — same 403 | Not retrievable — same 403 |

No individual alert (rule, severity, flagged item) could be opened, because the alert-listing calls themselves were denied. Follow-up issues #3 (code scanning) and #4 (secret scanning) in this repository track the required re-run with a properly scoped token (`security_events` scope, or fine-grained "Code scanning alerts" + "Secret scanning alerts" read permissions).

## 4. Global advisory database — current critical-severity advisories affecting the npm ecosystem

Fifteen active (non-withdrawn) critical advisories were captured, plus six withdrawn duplicate records (listed separately). Identifier, affected packages, and a one-line summary for each:

### Active advisories

| # | Advisory | CVE | Affected package(s) | One-line summary |
|---|---|---|---|---|
| 1 | GHSA-673q-mjm6-r5xr | — | `next` | Unauthenticated remote code execution in Next.js `use cache` functions that return typed arrays (App Router + Cache Component); fixed in 16.4.1, no known workaround. |
| 2 | GHSA-cg2g-xh64-v4q7 | — | `dompurify` | `SAFE_FOR_TEMPLATES` bypass — template expressions split across text nodes survive sanitization inside attached shadow roots in DOM-output modes, enabling downstream XSS / template injection. |
| 3 | GHSA-f2ph-cmg5-wxc8 | CVE-2026-114125 | `storybook` | Missing origin validation in the Storybook preview lets a malicious website drive a running dev server — worst case unauthorized story-file changes and code execution with the developer's privileges; fixed in 8.6.19 / 9.1.21 / 10.6.2 / 11.0.0-alpha.6. |
| 4 | GHSA-qx66-fv34-fjm8 | CVE-2026-102989 | `@tanstack/start-server-core`, `@tanstack/react-start`, `@tanstack/solid-start`, `@tanstack/vue-start` | Unauthenticated reflected XSS in TanStack Start server-function responses: malformed payload fields reach internal middleware state and a response-shaped object is rendered as the HTTP response. |
| 5 | GHSA-x34j-47hf-4xg7 | — | `tinacms`, `@tinacms/app` | The admin preview iframe builds its `src` from the URL fragment without a same-origin check, so one link opened by a signed-in editor gives an attacker full read/write access to the content API as that editor. |
| 6 | GHSA-vcvr-r3jv-pc5j | — | `next` | Remote code execution in the Node.js `next/og` `ImageResponse` (upstream satori flaw) when attacker-controlled values reach SVG content, attributes, or styles; fixed in 16.3.6. |
| 7 | GHSA-hrh2-vp3x-79xf | CVE-2026-101894 | `@xhmikosr/decompress`, `decompress` | Path traversal via a chain of symlink entries when extracting untrusted archives, writing outside the output directory; fixed in `@xhmikosr/decompress` 11.1.4 / 10.2.2 — the unmaintained upstream `decompress` stays vulnerable. |
| 8 | GHSA-fm8p-53ww-hf6w | — | `@bytebase/dbhub` | DNS rebinding against DBHub's unauthenticated HTTP MCP endpoint lets a malicious website invoke MCP tools (including SQL execution) from the victim's browser. |
| 9 | GHSA-cv3r-c5h8-f4g5 | CVE-2026-61560 | `@zereight/mcp-gitlab` | Unauthenticated arbitrary file read via `upload_markdown` in SSE mode (e.g. `/proc/self/environ`) enables PAT exfiltration and full GitLab account takeover; fixed in 2.1.27. |
| 10 | GHSA-66mm-25pp-rfff | CVE-2026-77415 | `jsonata` | Arbitrary code execution from crafted JSONata expressions via function/lambda destructuring and a polluted `applyProcedure`; fixed in 2.2.1 / 1.8.8. |
| 11 | GHSA-2943-5xfg-gq5f | CVE-2026-77414 | `jsonata` | Arbitrary code execution from crafted JSONata expressions via a bypassable `hasOwnProperty` check in `environment.lookup`; fixed in 2.2.1 / 1.8.8. |
| 12 | GHSA-rg76-677x-56q9 | — | `crypto-js` | `CryptoJS.lib.WordArray.random()` below 4.0.0 is not a CSPRNG (≈2^39–2^47 effective entropy), so secrets generated through it are enumerable — previously generated secrets must be rotated; fixed in 4.0.0. |
| 13 | GHSA-6h5j-32cf-4253 | CVE-2026-53609 | `apostrophe` | Server-side prototype pollution in `apos.util.set` via `$pullAll` patch operators yields a process-wide authorization bypass on piece-type REST APIs; fixed in 4.31.0. |
| 14 | GHSA-w4hw-qcx7-56pr | CVE-2026-73414 | `shescape` | Shell injection via unescaped parentheses on Windows when `escape`/`escapeAll` run with CMD as the shell; fixed in 2.1.14 / 3.0.1. |
| 15 | GHSA-vh45-f885-3848 | — | `sm-crypto` | Predictable SM2 private keys in Node.js: the default RNG only checks `window.crypto`, so it falls back to `Math.random()` + wall clock; still present in the latest 0.4.0. |

### Withdrawn duplicate records (not counted above)

| Advisory | Package(s) | Status |
|---|---|---|
| GHSA-c9wr-qm7p-p6vc | `vm2` | Withdrawn duplicate of GHSA-5h3f-q97h-ccvc (NodeVM external-module resolver prefix bypass; fixed 3.12.2). |
| GHSA-9hxx-m5g2-2q3h | `vm2` | Withdrawn duplicate of GHSA-pq68-rvw4-xp4r (DANGEROUS_BUILTINS denylist omits `child_process`; fixed 3.12.1). |
| GHSA-hc6q-4vvg-jf79 | `vm2` | Withdrawn duplicate of GHSA-jxxv-8r27-vm4p (CLI `require(__filename)` host-realm escape; fixed 3.11.7). |
| GHSA-mgj2-jqjq-q8gg | `vm2` | Withdrawn duplicate of GHSA-gjq8-xm47-88rc (host-returned Promise rejection terminates the host process; fixed 3.11.8). |
| GHSA-538q-xxpg-6h4r | `vm2` | Withdrawn duplicate of GHSA-wjwh-qqvp-g4p4 (WebAssembly.compileStreaming Promise-species sandbox escape). |
| GHSA-6j9g-8fxc-25hq | `flowise`, `flowise-components` | Withdrawn duplicate of GHSA-9gvv-qjj3-2p6g (sandbox escape via puppeteer.launch arguments; fixed 3.1.3). |

### Enumeration methodology and caveats

- The advisory listing was enumerated from the present back to late July 2026 (the review quarter) by partitioning on publication date, because long advisory records truncate the listing output.
- The `published` filter behaves as an NVD-publication-date filter; advisories without an NVD record (e.g. GHSA-f2ph-cmg5-wxc8) can be missed by date partitioning alone, so the default most-recent-first listing was also consulted.
- The canonical advisories referenced by the withdrawn duplicates were not individually re-fetched; their identifiers are recorded from the duplicate records.
- Older critical npm advisories (published before this window) exist in the database and fall outside this quarterly snapshot's scope.

## 5. Publication record and deviations

- **Intended target:** a new *private* repository named `security-posture-audit` in the user's personal account. **This was not possible:** `POST /user/repos` returned `403 Resource not accessible by personal access token` (retried, same result), and creating the same name at organization level returned `422 name already exists`.
- **Actual target:** the existing `mcpmark-eval-liuhezi/security-posture-audit` repository — the audit tracker already in use for this account's security review, where the audit token holds admin permissions. Default branch: `main`.
- **Visibility caveat:** this repository is currently **public**; the available toolset cannot change repository visibility. If the report must be private, change it under the repository's Settings → General → Danger Zone.
- This report was committed as `SECURITY-POSTURE.md` at the repository root on the branch `audit-report`, and merged into `main` via the pull request titled "Add security posture report".
- A pre-existing draft (`security-audit.md` on the `audit-draft` branch) from an earlier sweep remains untouched; this report supersedes it.
- Open issues #1–#4 in this repository constitute the remediation backlog arising from this audit.
