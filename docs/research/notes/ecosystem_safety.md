# Claude Agent Skills Ecosystem: Directories, Format, Security, Licensing, Precedence (as of 5 Nov 2026)

Research date: 2026-11-05. Star counts are snapshots from the date each page was fetched (this session unless noted). Third-party trackers often lag GitHub by months, so their figures are marked as older.

## (a) Which directories, marketplaces and curated lists are the most used and best curated, and how trustworthy is each?

### Takeaway
By stars, anthropics/skills is far ahead (about 187k). It is the only first-party source of example skills, but it is a demo repo, and its four document skills are not open source. The curated "awesome" lists (ComposioHQ about 79k, VoltAgent about 37k, travisvn about 16k) are link directories with little or no security vetting. skillsmp.com is an automated GitHub scraper whose only inclusion bar is 2 stars. The safest place to install from is Anthropic's plugin marketplaces (claude-plugins-official, claude-community), which have name-impersonation protection and SHA pinning. Even there, Anthropic says it does not verify plugin behaviour.

### Cited Findings
**anthropics/skills (first-party examples)**
- About 187.4k stars, 22.1k forks, 1.1k watchers and 61 commits (fetched Nov 2026). It holds Anthropic's example skills in four categories (Creative & Design, Development & Technical, Enterprise & Communication, Document Skills), plus `./spec` and `./template` folders. — [anthropics/skills](https://github.com/anthropics/skills)
- The README says the skills are "provided for demonstration and educational purposes only" and should be tested before you rely on them for critical tasks. — [anthropics/skills](https://github.com/anthropics/skills)
- You install it as a plugin marketplace: `/plugin marketplace add anthropics/skills`, then `/plugin install document-skills@anthropic-agent-skills` or `example-skills@anthropic-agent-skills`. — [anthropics/skills](https://github.com/anthropics/skills)
- `anthropic-agent-skills` and `agent-skills` are on Claude Code's list of official-tier marketplace names. — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md)

**Anthropic plugin marketplaces**
- Anthropic runs two general-purpose marketplaces:
  - `claude-plugins-official` (repo anthropics/claude-plugins-official) holds "Plugins Anthropic maintains, plus plugins from partners and other authors". Claude Code adds it automatically on the first interactive session.
  - `claude-community` (repo anthropics/claude-plugins-community) holds "Third-party plugins that their authors submitted to Anthropic". You have to add it yourself.
  — [Anthropic's marketplaces](https://code.claude.com/docs/en/plugins/anthropic-marketplaces.md)
- "Most of what it lists comes from partners and other authors rather than from Anthropic." The web catalog at claude.com/marketplace shows install counts and marks some plugins "Anthropic verified". — [Anthropic's marketplaces](https://code.claude.com/docs/en/plugins/anthropic-marketplaces.md)
- Claude Code accepts official and community marketplace names only from `github.com/anthropics/` repositories, so "a third-party marketplace can't present itself as an Anthropic one". Where the community catalog pins a plugin to a commit SHA, which it does for nearly every entry, Claude Code refuses to install a different commit. — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md)
- Anthropic still warns: "Anthropic does not control what MCP servers, files, or other software are included in plugins and cannot verify that they will work as intended or that they won't change." — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md)
- "Anthropic doesn't review third-party marketplaces." — [Anthropic's marketplaces](https://code.claude.com/docs/en/plugins/anthropic-marketplaces.md)
- Auto-update defaults: on for `claude-plugins-official` and most other official-tier marketplaces; off for the community marketplace and all third-party marketplaces. — [Install and manage plugins](https://code.claude.com/docs/en/discover-plugins)
- The old `claude-code-plugins` marketplace in anthropics/claude-code is deprecated. — [Anthropic's marketplaces](https://code.claude.com/docs/en/plugins/anthropic-marketplaces.md)

**ComposioHQ/awesome-claude-skills**
- About 78.7k stars, 9.5k forks, 201 open issues and 1.7k PRs (fetched Nov 2026). Older tracker snapshots showed 58.4k ([gittrend](https://gittrend.io/repo/ComposioHQ/awesome-claude-skills), last push May 2026) and about 64k ([SourcePulse](https://www.sourcepulse.org/projects/27928492)). — [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- The README claims "1000+" skills, but the visible list has about 150 entries, about 78 of them Composio app-automation skills. The page is heavily promotional: a Composio API key quickstart, UTM-tagged links, MCP Gateway pitches. — [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- It has no security policy or third-party vetting process. Some entries are dual-use (FFUF fuzzing, forensics or file deletion) or need access to sensitive sessions (Chrome Relay drives your logged-in Chrome). The repo is Apache-2.0, but individual skills may carry other licenses. — [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)

**VoltAgent/awesome-agent-skills**
- About 36.8k stars, 4.1k forks, 971 commits and an MIT license. The badge says "1497+" skills. It claims to be "Hand-picked, not AI-slop generated". Skills are grouped by the vendor or company that publishes them, plus a separate Community section. No security disclaimer is shown. — [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)

**travisvn/awesome-claude-skills**
- About 15.7k stars, 2.1k forks and only 42 commits. The "Last Updated" badge reads February 2026, and the newest dated "Recent Updates" entry is 13 Nov 2025. No license is stated. A tracker showed 12.2k stars with a last push on 28 Apr 2026 ([gittrend](https://gittrend.io/repo/travisvn/awesome-claude-skills)). — [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
- It is the only major list with a security section: "Skills can execute arbitrary code in Claude's environment". It advises installing only from trusted sources and reviewing SKILL.md and all scripts first. — [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)

**Other lists**
- BehiSecc/awesome-claude-skills had about 8.4k stars as of 13 Apr 2026 (older snapshot). — [Star History](https://www.star-history.com/behisecc/awesome-claude-skills)
- Chat2AnyLLM/awesome-claude-skills claims 7,225 skills (aggregator). — [ecosyste.ms](https://awesome.ecosyste.ms/projects/github.com%2FChat2AnyLLM%2Fawesome-claude-skills)

**skillsmp.com**
- Its own FAQ says a scraper regularly syncs with GitHub. Repos need at least 2 GitHub stars to appear. Search ranks by stars, not relevance. — [skillsmp.com](https://www.skillsmp.com); [PyPI skillsmp CLI](https://pypi.org/project/skillsmp/)
- Reported catalog sizes vary widely: 35,530 on the site page, and anywhere from 61k to 570k+ on third-party listings. — [EveryDev](https://www.everydev.ai/tools/skills-marketplace-skillsmp); [GTM Directory](https://thegtmdirectory.com/tools/skillsmp)

**Open registries (cautionary examples, not Claude-specific)**
- ClawHub (the OpenClaw registry) and skills.sh are where most documented malware was found (see section c). ClawHub let anyone upload; the only barrier was a GitHub account at least a week old. — [Koi Security](https://koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting); [eSecurity Planet](https://esecurityplanet.com/threats/hundreds-of-malicious-skills-found-in-openclaws-clawhub)

### Inferences
- Trust ranking for a marketing repo, from most to least trusted:
  1. anthropics/skills, Apache-2.0 skills only
  2. Anthropic-maintained plugins in claude-plugins-official
  3. Partner or vendor plugins in claude-plugins-official, and SHA-pinned claude-community entries
  4. Vendor-authored skills linked from VoltAgent
  5. Community entries on the awesome lists
  6. skillsmp.com and open registries
- Stars measure popularity, not safety. Orca showed a registry popularity metric could be "trivially spoofed" (see c). The awesome lists are discovery tools. Vet anything found through them as untrusted code.
- ComposioHQ's list has the most stars but works partly as a marketing funnel for Composio. Its "1000+" figure is not supported by the visible list.

### Gaps
- I could not see last-commit dates for anthropics/skills, VoltAgent or ComposioHQ on the fetched pages, so their update frequency in Nov 2026 is unverified.
- The size of the claude-plugins-official catalog is not published ("The catalog changes often").
- I found no source describing Anthropic's review process for claude-community submissions beyond SHA pinning.

## (b) What are the SKILL.md format rules per Anthropic's docs and the Agent Skills spec?

### Takeaway
A skill is a folder containing `SKILL.md` (YAML frontmatter plus a Markdown body), with optional `scripts/`, `references/` and `assets/` folders. The two key fields have hard limits:
- `name`: at most 64 characters; lowercase letters, digits and hyphens; must match the folder name; must not contain "anthropic" or "claude"
- `description`: 1 to 1,024 characters; no XML tags

Keep the body under 500 lines (about 5k tokens or fewer) and keep file references one level deep. Claude Code supports many extra fields. claude.ai uploads accept only the spec fields.

### Cited Findings
- **Spec frontmatter:**
  - `name` (required): 1–64 characters, lowercase a–z, 0–9 and hyphens only. It cannot start or end with a hyphen, cannot contain `--`, and "Must match the parent directory name".
  - `description` (required): 1–1,024 characters.
  - Optional: `license`, `compatibility` (at most 500 characters), `metadata` (a string-to-string map) and `allowed-tools` (experimental, space-separated).
  — [Agent Skills specification](https://agentskills.io/specification)
- **Anthropic platform rules:** `name` "Cannot contain XML tags" and "Cannot contain reserved words: `anthropic`, `claude`". `description` must be non-empty, at most 1,024 characters, with no XML tags. Write descriptions in third person ("Processes Excel files…"), stating both what the skill does and when to use it. Gerund names such as `processing-pdfs` are recommended. — [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- **Optional folders:** `scripts/` for executable code, `references/` for docs loaded on demand (e.g. REFERENCE.md, FORMS.md) and `assets/` for templates, images and data. Reference files use relative paths from the skill root. — [Agent Skills specification](https://agentskills.io/specification)
- **Progressive disclosure has three levels:**
  1. Metadata (about 100 tokens) is loaded at startup for every skill.
  2. The SKILL.md body (under 5,000 tokens recommended) is loaded when the skill activates.
  3. Resources are loaded only when needed.
  "Keep your main SKILL.md under 500 lines." — [Agent Skills specification](https://agentskills.io/specification)
- "Keep references one level deep from SKILL.md". Nested references may be read only partially (e.g. `head -100`). Reference files over 100 lines should start with a table of contents. Scripts are "run, not loaded"; only their output costs tokens. — [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- **Package availability:** claude.ai can install npm and PyPI packages; the Claude API "has no network access and no runtime package installation". — [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- **Validation tool:** `skills-ref validate ./my-skill` checks frontmatter and naming. — [Agent Skills specification](https://agentskills.io/specification)
- **Claude Code extra fields:** `when_to_use`, `argument-hint`, `arguments`, `disable-model-invocation`, `user-invocable`, `allowed-tools`, `disallowed-tools`, `model`, `effort`, `context: fork`, `agent`, `background`, `hooks`, `paths`, `shell`, plus `metadata`, `license` and `compatibility`, which are "accepted but not acted on".
  - In Claude Code, all fields are optional and only `description` is recommended; `name` defaults to the directory name.
  - Unrecognised fields are ignored without an error, so a misspelled field silently does nothing.
  — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- **Claude Code limits and loading:**
  - The combined `description` + `when_to_use` text is truncated at 1,536 characters in the skill listing.
  - Frontmatter is read only if the opening `---` is the file's first line.
  - After compaction, each recently invoked skill is re-attached with its first 5,000 tokens, within a 25,000-token shared budget.
  — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- claude.ai uploads accept only `name`, `description`, `license`, `compatibility`, `metadata` and `allowed-tools`. Any other field causes a hard error at upload. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)

### Inferences
- For portability across Claude Code, claude.ai and the API, vendored skills should use only the spec fields. Run `skills-ref validate` in CI.
- Rename any vendored skill whose name contains "claude" or "anthropic"; the platform docs forbid those words.

### Gaps
- I did not re-fetch Anthropic's engineering blog post "Equipping agents for the real world with Agent Skills" (Oct 2025, older info) this session. The format details above come from the current docs and spec instead.

## (c) What security issues are known with third-party skills, and what vetting checklist do security researchers recommend?

### Takeaway
2026 studies consistently find a large minority of public skills vulnerable (roughly 26–37%) and a few percent outright malicious. There have been real malware campaigns, notably ClawHavoc on ClawHub, which delivered Atomic Stealer through fake "prerequisite" install steps. Most malicious skills combine code with prompt injection. Skills that bundle scripts are about twice as likely to be vulnerable. The consensus advice: treat skills like npm or PyPI dependencies. Read every file, distrust install prerequisites and runtime-fetched instructions, pin to a hash, scan, sandbox, and minimise permissions.

### Cited Findings
**Research and audits**
- **Liu et al., "Agent Skills in the Wild" (arXiv:2601.10338, 15 Jan 2026):**
  - Collected 42,447 skills from two marketplaces and analysed 31,132.
  - 26.1% have at least one vulnerability across 14 patterns.
  - Data exfiltration appears in 13.3% and privilege escalation in 11.8%; 5.2% show high-severity patterns suggesting malicious intent.
  - Script-bundling skills are 2.12× more likely to be vulnerable (p<0.001).
  - Their SkillScan tool reports 86.7% precision and 82.5% recall.
  - The authors call for capability-based permissions and mandatory vetting.
  — [arXiv 2601.10338](https://arxiv.org/abs/2601.10338)
- **Snyk "ToxicSkills" (5 Feb 2026):**
  - Scanned 3,984 skills from ClawHub and skills.sh.
  - 36.82% (1,467) have some security flaw; 13.4% (534) have at least one critical issue; 76 malicious payloads were confirmed.
  - Of confirmed malicious skills, 100% contain malicious code patterns and 91% also use prompt injection.
  - Secrets were exposed in 10.9% of ClawHub skills.
  - Named threat actors: zaycv (40+ auto-generated skills), Aslaep123 (crypto typosquats) and pepe276 (Unicode-smuggling injection).
  - The 0% false-positive figure is vendor-reported.
  — [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)
- Snyk found a common attack pattern:
  - Prerequisites that download binaries, often in password-protected ZIPs to evade scanners.
  - Base64- or Unicode-obfuscated exfiltration commands.
  - Instructions that disable security controls.
  - Remote instructions fetched at runtime, so a skill can turn malicious after review.
  — [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)
- **Koi Security "ClawHavoc" (Feb 2026):**
  - 341 of 2,857 ClawHub skills (11.9%) were malicious; 335 carried the Atomic Stealer macOS infostealer.
  - Delivery was a fake prerequisite: a password-protected ZIP on Windows, or a shell command pasted from glot.io on macOS.
  - Lures included solana-wallet-tracker and youtube-summarize-pro, plus typosquats such as "clawhubb".
  - Koi later reported 824 malicious skills once the registry passed 10,700 skills.
  — [Koi Security](https://koi.ai/blog/clawhavoc-341-malicious-clawedbot-skills-found-by-the-bot-they-were-targeting); [The Hacker News](https://thehackernews.com/2026/02/researchers-find-341-malicious-clawhub.html)
- Antiy CERT counts at least 1,184 malicious skills historically on ClawHub. The figure differs from Koi's, probably because of different scope and dates. — [Antiy](https://www.antiy.net/p/clawhavoc-analysis-of-large-scale-poisoning-campaign-targeting-the-openclaw-skill-market-for-ai-agents/)
- Unit 42 found persistent, evasive malicious skills on ClawHub from February to May 2026. — [Unit 42](https://unit42.paloaltonetworks.com/openclaw-ai-supply-chain-risk/) (search snippet only; full page not fetched)
- Orca Security reports that the registry's popularity metric can be trivially spoofed. It also found that scanning happens at creation and only again later, leaving a window for malicious updates. — [Orca Security](https://orca.security/resources/blog/ai-agent-skill-supply-chain-security/) (search snippet only)
- A USENIX Security 2026 measurement study is reported to cover 98,380 skills and confirm 157 malicious ones. A May 2026 study reported a 0.00% detection rate for the scanners it evaluated. Both come from search-result summaries; I did not verify the primary papers. Related work: [arXiv 2605.28588](https://arxiv.org/html/2605.28588v1), [arXiv 2607.13987](https://arxiv.org/pdf/2607.13987). — [CSA research note](https://labs.cloudsecurityalliance.org/research/csa-research-note-ai-skill-supply-chain-attacks-20260624-csa/)
- **OWASP Agentic Skills Top 10 (page updated March 2026):**
  - Entries shown: AST01 Malicious Skills, AST02 Supply Chain Compromise, AST03 Over-Privileged Skills, AST04 Insecure Metadata, AST05 Untrusted External Instructions, AST08 Poor Scanning, AST10 Cross-Platform Reuse.
  - Skills "execute with the full permissions of the host agent".
  — [OWASP AST01](https://owasp.github.io/www-project-agentic-skills-top-10/ast01)

**Claude-specific risks (Anthropic docs)**
- A project skill's `allowed-tools` applies "even in a `-p` run in a folder you've never trusted". Anthropic says to review `allowed-tools` in checked-in skills. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Skills can embed `` !`cmd` `` shell injection, which runs before Claude sees the skill. Setting `"disableSkillShellExecution": true` blocks this for user, project, plugin and added-directory skills. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Plugins can run hooks, monitors, MCP and LSP servers, and `bin/` executables with full user privileges and outside the sandbox. Auto-update means "the files you reviewed can change on disk". — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md)

**Recommended vetting steps (compiled)**
1. **Check provenance.** Prefer verified publishers; be wary of new accounts or authors with many near-identical skills. — [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/); [OWASP](https://owasp.github.io/www-project-agentic-skills-top-10/ast01)
2. **Read every file.** That means SKILL.md, all `scripts/`, and, for plugins, `hooks/hooks.json`, `.mcp.json` and `bin/`. Run `claude --plugin-dir <dir> plugin details <name>` for a component inventory. — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md); [travisvn list](https://github.com/travisvn/awesome-claude-skills)
3. **Reject red flags:**
   - "Prerequisites" that download binaries or pipe curl into a shell
   - Password-protected archives
   - Base64 or Unicode-obfuscated strings
   - Instructions fetched from remote URLs at runtime
   - Requests to read credentials, `.env`, SSH keys or memory files
   - Instructions to disable safeguards
   Never auto-run Prerequisites sections. — [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/); [OWASP](https://owasp.github.io/www-project-agentic-skills-top-10/ast01)
4. **Review `allowed-tools`, `hooks` and `` !`cmd` `` usage.** Add `disable-model-invocation: true` for skills with side effects. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
5. **Scan.** For example, `uvx mcp-scan@latest --skills` (Snyk) or SkillScan (Liu et al.). Scanners miss things, so scanning does not replace manual review. — [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/); [arXiv 2601.10338](https://arxiv.org/abs/2601.10338)
6. **Pin and verify.** Hash-pin or commit-pin installed skills and alert on changes; turn off auto-update for marketplaces you don't control. — [OWASP](https://owasp.github.io/www-project-agentic-skills-top-10/ast01); [Install and manage plugins](https://code.claude.com/docs/en/discover-plugins)
7. **Contain.** Use a sandbox or container, least privilege, and audit logs. Rotate credentials if a bad skill ran. — [OWASP](https://owasp.github.io/www-project-agentic-skills-top-10/ast01); [Snyk](https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/)
8. **Enforce org-wide.** Use managed settings to allowlist marketplaces and restrict hooks. — [Plugin security and trust](https://code.claude.com/docs/en/plugins/security.md)

### Inferences
- Vendoring (copying a reviewed snapshot into git) is safer than installing a live plugin. The code is frozen at the reviewed commit, changes show up in diffs, and there is no background auto-update.
- Instruction-only marketing skills (copywriting, SEO checklists) are much lower risk than skills that bundle scripts. Even so, prompt injection in Markdown (hidden Unicode, "ignore previous instructions", fetch-this-URL steps) still needs a manual read.
- Most documented incidents were on open registries (ClawHub, skills.sh), not in Anthropic's marketplaces. I found no reported malware incident in anthropics/claude-plugins-official.

### Gaps
- I did not fetch and verify the primary papers for the USENIX 2026 study (98,380 skills, 157 malicious) or the "0.00% detection" claim.
- I found no public incident report specific to Claude skills from Anthropic's marketplaces or anthropics/skills.

## (d) What licensing rules apply when vendoring skills, and what must be included when copying an MIT or Apache-2.0 skill?

### Takeaway
Apache-2.0 skills, which includes most of anthropics/skills, can be vendored if you:
- ship a copy of the license
- keep all copyright and attribution notices
- reproduce the attribution notices from any NOTICE file
- mark the files you modified

MIT skills need the copyright notice and the license text kept. Anthropic's document skills (docx, pdf, pptx, xlsx) are source-available under terms that forbid copying, redistribution and derivative works outside Anthropic's services, so they must not be vendored into a repo.

### Cited Findings
- **Apache-2.0 §4 redistribution conditions:**
  1. Give recipients a copy of the License.
  2. "cause any modified files to carry prominent notices stating that You changed the files".
  3. Keep "all copyright, patent, trademark, and attribution notices from the Source form".
  4. If the Work includes a "NOTICE" file, derivative works must include "a readable copy of the attribution notices contained within such NOTICE file" in a NOTICE file, in the source or documentation, or in a display.
  — [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
- In anthropics/skills, "Many skills are open source under Apache 2.0". The document skills (`skills/docx`, `skills/pdf`, `skills/pptx`, `skills/xlsx`) are source-available, not open source. — [anthropics/skills](https://github.com/anthropics/skills)
- The document skills' LICENSE.txt prohibits these, among others:
  - reproducing or copying "except for temporary copies created automatically during authorized use of the Services"
  - "Distribute, sublicense, or transfer these materials to any third party"
  - "Create derivative works"
  - "Extract these materials from the Services or retain copies of these materials outside the Services"
  — [anthropics/skills docx LICENSE.txt](https://raw.githubusercontent.com/anthropics/skills/main/skills/docx/LICENSE.txt)
- The ComposioHQ list's repo license is Apache-2.0, "but individual skills may carry different licenses". Check each skill's folder. — [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- The VoltAgent list is MIT-licensed. That covers the list itself, not the linked skills. — [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)
- The travisvn list states no license. — [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
- The spec's optional `license` frontmatter field can name a license or a bundled file, e.g. `license: Proprietary. LICENSE.txt has complete terms`. Claude Code accepts it "but not acted on". — [Agent Skills specification](https://agentskills.io/specification); [Claude Code skills docs](https://code.claude.com/docs/en/skills)

### Inferences
- **Practical vendoring checklist for Apache-2.0 skills:**
  1. Copy the upstream LICENSE (or LICENSE.txt) into the skill folder, or into a top-level `third_party/licenses/`.
  2. Keep any copyright headers.
  3. If upstream has a NOTICE file, copy its attribution text into your repo's NOTICE.
  4. Add a "Modified by <you>, <date>: <summary>" note in each changed file, or in a CHANGES section of SKILL.md.
  5. Set `license: Apache-2.0` and `metadata: {source: <repo@commit>}` in frontmatter.
- **For MIT skills:** keep the copyright line and the full MIT text, e.g. a LICENSE file in the skill folder. Marking modifications is good practice but not required.
- **Skills with no license:** treat them as all rights reserved. Do not vendor them; link to them, or ask the author.
- **Repo-level tracking:** a `THIRD_PARTY_NOTICES.md` or `vendor.lock` listing each vendored skill's upstream URL, commit SHA, license and local changes covers both attribution and supply-chain pinning.
- For DOCX, PDF, PPTX or XLSX work, use Anthropic's built-in document skills or plugin (`document-skills@anthropic-agent-skills`) instead of copying them.

### Gaps
- I did not confirm whether anthropics/skills ships a top-level NOTICE file. The repo's root LICENSE file was not fetched; check them before vendoring.
- I did not fetch the MIT license text this session. Its keep-the-notice requirement is standard, but it is not cited here.

## (e) How do project-level skills in .claude/skills interact with plugin skills (name collisions, precedence)?

### Takeaway
Plugin skills are namespaced as `/plugin-name:skill-name`, so they never collide with project, personal or enterprise skills; both load side by side. Among the non-plugin locations, precedence is enterprise, then personal (`~/.claude/skills`), then project (`.claude/skills`). A skill beats a same-named `.claude/commands/` file.

### Cited Findings
- Skill locations:
  - Enterprise: the managed settings directory
  - Personal: `~/.claude/skills/`
  - Project: `.claude/skills/<skill-name>/SKILL.md` ("Commit it so your team gets it too")
  - Nested: `<subdir>/.claude/skills/`
  - `--add-dir` directories
  - Plugin: `<plugin>/skills/`, loaded as `/plugin-name:skill-name`
  - claude.ai account skills
  — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Precedence: "Enterprise over personal, and personal over project. With `deploy` in both `~/.claude/skills/` and the project's `.claude/skills/`, `/deploy` runs the personal one." — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Plugin vs local: "Both load, because plugin skills are namespaced as `/plugin-name:skill-name`." The frontmatter `name` sets the last segment: `my-plugin/skills/review/SKILL.md` with `name: fancy` becomes `/my-plugin:fancy`. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Other collision rules:
  - A skill and a `.claude/commands/` file with the same name: the skill wins.
  - A project skill named like a bundled skill replaces the bundled command, "but not its aliases".
  - With added directories, the first directory added wins and the other skill runs under a prefixed name (e.g. `/cli:verify`).
  — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- The `anthropic-skills` namespace is reserved for skills synced from claude.ai. Synced skills can't be edited locally, since "a later sync can overwrite or remove it". — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Plugin enablement scope: local (`.claude/settings.local.json`) overrides project (`.claude/settings.json`), which overrides user (`~/.claude/settings.json`). Committing a project-scope enable "doesn't download it to their machines"; each collaborator still has to install it. — [Install and manage plugins](https://code.claude.com/docs/en/discover-plugins)
- You can block skills with permission deny rules such as `Skill(deploy *)`, or disable them all with `Skill`. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)
- Only descriptions are loaded into context in a normal session; full content loads on invocation. — [Claude Code skills docs](https://code.claude.com/docs/en/skills)

### Inferences
- If this repo vendors a skill (e.g. `copywriting`) into `.claude/skills/` while the `marketing-skills` plugin is also enabled, both `/copywriting` and `/marketing-skills:copywriting` will exist. They won't shadow each other, but two near-identical descriptions in the listing could make automatic selection unpredictable and add context cost. Recommendation: either disable the plugin for this project (`false` in `.claude/settings.local.json` or `.claude/settings.json`), or give vendored copies distinct names and descriptions.
- A teammate's personal `~/.claude/skills/<same-name>` silently overrides the repo's project skill for them. Prefixed or distinctive names (e.g. `wsx-copywriting`) avoid that surprise.
- Because a project skill's `allowed-tools` applies even in untrusted `-p` runs, committed skills deserve code-review-level scrutiny in PRs.

### Gaps
- The docs don't say how Claude chooses between two auto-invocable skills with overlapping descriptions. The selection behaviour described above is inferred, not documented.
