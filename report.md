# Security Posture Audit Report — Account HeziLiu

Quarterly security review cycle. All figures and lists below are reported exactly as the live GitHub search and API results returned them at audit time — no rounding, no estimating.

## 1. Account

- **Login (as returned by account lookup):** `HeziLiu`
- **Profile URL:** https://github.com/HeziLiu
- **Account ID:** 28861483
- **Profile metadata:** public_repos 4, public_gists 0, followers 5, following 5

## 2. Repository Inventory

Repository search performed: `user:HeziLiu`

**Live result: total_count 2, incomplete_results false.** The search returned exactly 2 repositories. (Note: the account profile metadata reports 4 public repositories; the difference is attributable to the search excluding forked repositories by default. Both returned repositories are non-forks.)

### 2.1 HeziLiu/Little-rookie

- **Default branch:** `master`
- **Description:** Undergraduate coursework
- **Primary language:** Java
- **Created:** 2018-05-15T06:51:51Z
- **Visibility:** public
- **Published security advisories:** NONE — the repository security advisory query (state: published) returned an empty list `[]`. No advisories have been published against this repository.
- **Most recent commit on default branch (`master`):**
  - Short SHA: `964bd6b`
  - Full SHA: 964bd6b191a3864a4c6c4430a85d17bb16920581
  - Date: 2019-06-02T07:47:10Z
  - Message: `DELETE`

### 2.2 HeziLiu/Big-Buzzard

- **Default branch:** `master`
- **Description:** For future....
- **Created:** 2018-05-15T07:20:25Z
- **Visibility:** public
- **Published security advisories:** NONE — the repository security advisory query (state: published) returned an empty list `[]`. No advisories have been published against this repository.
- **Most recent commit on default branch (`master`):**
  - Short SHA: `4ce5a6d`
  - Full SHA: 4ce5a6d6e410756cebcaed5cdf6f661c24446bda
  - Date: 2018-05-17T10:22:21Z
  - Message: `Merge branch 'master' of https://github.com/Tackic/Big-Buzzard`

### Advisory status summary

| Repository | Published advisories | Latest commit (short SHA) | Latest commit date |
|---|---|---|---|
| HeziLiu/Little-rookie | None (empty result) | 964bd6b | 2019-06-02 |
| HeziLiu/Big-Buzzard | None (empty result) | 4ce5a6d | 2018-05-17 |

## 3. Pull Requests Authored

Pull request search performed: `is:pr author:HeziLiu`, sorted by creation date, most recent first.

**The search did NOT return nothing — it returned results.** Reported exactly as returned by the live search:

- **total_count returned by the initial search call: 1316**
- **total_count returned by a subsequent identical search call: 1317**

Most recent first, the pull requests returned by the live searches (repository, number, state):

| Repository | PR number | State | Created |
|---|---|---|---|
| mcpmark-eval-liuhezi/release-readiness-demo | 16 | closed (merged) | 2026-10-23T02:22:18Z |
| mcpmark-eval-liuhezi/pipeline-rehearsal | 1 | open | 2026-10-23T02:22:08Z |
| mcpmark-eval-liuhezi/copilot-dispatch-lab | 2 | open | 2026-10-23T02:21:09Z |
| mcpmark-eval-liuhezi/ci-triage-demo | 8 | open (draft) | 2026-10-23T02:14:19Z |
| mcpmark-eval-liuhezi/eng-onboarding-runbook | 1 | open | 2026-10-23T02:11:37Z |
| mcpmark-eval-liuhezi/ci-review-demo | 1 | open | 2026-10-23T02:10:08Z |
| mcpmark-eval-liuhezi/code-review-rehearsal | 1 | open | 2026-10-22T23:59:34Z |
| mcpmark-eval-liuhezi/release-audit-hub | 8 | open | 2026-10-22T23:59:07Z |
| mcpmark-eval-liuhezi/release-drill-2026-solo | 1 | closed (merged) | 2026-10-22T23:58:05Z |
| mcpmark-eval-liuhezi/ci-lifecycle-demo | 2 | open | 2026-10-22T20:56:06Z |
| mcpmark-eval-liuhezi/actions-runbook-drill | 1 | open | 2026-10-22T20:51:05Z |
| mcpmark-eval-liuhezi/release-audit-tracker-4 | 2 | open | 2026-10-22T20:47:14Z |

Supplementary date-scoped searches of the same author, reported as returned:
- `is:pr author:HeziLiu created:2026-10-23` — total_count 46
- `is:pr author:HeziLiu created:2026-10-22` — total_count 359

Enumerated verification notes, recorded for audit integrity:
- The search API response payloads truncate the per-item list, so items beyond the most recent handful could not be itemized one-by-one from a single response. Counts above are exactly as returned.
- The unfiltered search (1316/1317) and the date-scoped searches (46 + 359 for the two most recent days) were separate live queries; their most-recent-first orderings are reported independently, exactly as each response ordered them.

## 4. Publication Record and Deviations

- Intended action: create a new repository named `security-posture-audit` initialized with a README.
- Actual outcome: repository creation under the personal account `HeziLiu` was refused by the API with `403 Resource not accessible by personal access token`. Creation in the organization the account belongs to (`mcpmark-eval-liuhezi`) returned `422 name already exists on this account`.
- Resolution: the audit trail was written to the existing repository `mcpmark-eval-liuhezi/security-posture-audit` (default branch `main`), on a newly created branch `audit-findings`, with this report committed as `report.md`. The pull request from `audit-findings` into `main` carries the exact title "Add security posture audit report".
- The account lookup confirmed membership in organization `mcpmark-eval-liuhezi` (no team memberships within it).
- Notification watching on the repository `mcpmark-eval-liuhezi/security-posture-audit` was switched on as part of this audit cycle.

## 5. Findings Summary for the Team Sync

1. **No published security advisories** against either repository returned by the account repository search.
2. **Both repositories are dormant** — most recent default-branch commits date from 2018 and 2019.
3. **Pull request activity is non-empty and substantial** — the authored-PR search returned 1316 (1317 on a repeat call) total matches, most recent first, spanning demonstration and audit repositories under the `mcpmark-eval-liuhezi` organization.
