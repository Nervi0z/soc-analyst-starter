# Contributing

Contributions are welcome: new resources, corrections, broken links, outdated content, and additional sections.

---

## Ways to contribute

- **New resource:** Open an [issue](https://github.com/Nervi0z/soc-analyst-starter/issues/new?template=add-resource.md) with the resource name, URL, and a note on why it belongs here
- **Fix existing content:** Broken link, outdated info, incorrect command — submit a pull request directly
- **New section:** Open an issue first to discuss scope before writing
- **Typos and formatting:** Small fixes are fine as pull requests without an issue

---

## Submitting a pull request

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR_USERNAME/soc-analyst-starter.git
   ```
3. Create a descriptive branch:
   ```bash
   git checkout -b add-cyberdefenders-section
   git checkout -b fix-wireshark-filter-example
   ```
4. Make your changes in `README.md`
5. Commit with [Conventional Commits](https://www.conventionalcommits.org/) prefixes:
   ```bash
   git commit -m "feat: add CyberDefenders to practice platforms"
   git commit -m "fix: correct broken TryHackMe SOC path link"
   git commit -m "docs: expand Sysmon event ID table"
   ```
6. Push your branch:
   ```bash
   git push origin your-branch-name
   ```
7. Open a pull request against `main`. Reference any related issue with `Closes #NUMBER`

---

## Content standards

- No emojis
- Commands must be real and executable — not descriptions of what a command does
- Resources must be verifiably active and directly relevant to SOC L1 work
- Descriptions should be specific — if a sentence could appear in any security guide unchanged, rewrite it
- Free or freemium resources preferred; paid resources are fine when genuinely valuable and noted as such
