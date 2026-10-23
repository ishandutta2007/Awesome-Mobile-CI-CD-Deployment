# Awesome-Mobile-CI-CD-Deployment

## Top Mobile CI/CD & Deployment Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Native iOS Signing, Managed macOS Runners & Self-Hosted Build Pipelines*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Mobile CI/CD & Deployment**. These tools automate the path from a git push to a tester's device or the App Store — running builds on macOS hardware, managing the iOS certificate and provisioning profile nightmare, and orchestrating release workflows without a dedicated release engineer.

**Examples** include Fastlane, Bitrise, Codemagic, GitHub Actions, Xcode Cloud, and GitLab CI/CD (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, transparent code signing, and CI-agnostic automation — especially critical because **iOS code signing is the most common reason mobile pipelines break**, and open-source Fastlane is the tool that solves it regardless of which CI you use.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[Bitrise](https://www.bitrise.io/)** — **The mobile-first CI/CD platform with 400+ pre-built steps.** **Hobby tier is free (300 credits/month)**, Pro at **$200/month** with M2 Pro Large machines . **Gartner Peer Insights reviewers** praise the mobile-specific focus, but **small teams may find Pro pricing high** for occasional releases . **Best for teams wanting dedicated mobile CI** with a visual workflow editor and mobile-specific build insights, without managing macOS runner infrastructure themselves.

- **[Codemagic](https://codemagic.io/)** — **The Flutter and cross-platform CI/CD specialist.** **Free tier: 500 minutes/month on Apple Silicon**, Pro at **$49/month** . **In a 2026 benchmark using the open-source Flutter app Medito**, Codemagic's Mac mini M4 completed an iOS release build in **6 min 58 sec** — roughly **1.8x faster than GitHub Actions' standard M1 runner** (12 min 18 sec) . **Hosted CodePush OTA service** claims roughly 1/4 the price of Expo for 100k MAU . **Best for Flutter teams** wanting native Apple Silicon builds without managing infrastructure, with competitive build speeds on their M4 machines .

- **[GitHub Actions](https://github.com/features/actions)** — **The general-purpose CI/CD runner with macOS support.** **Free for public repositories; private repos get 2,000 free minutes/month (macOS consumes at 10x rate, effectively 200 minutes)** . **The same 2026 benchmark** showed the standard M1 runner at **12 min 18 sec** for an iOS release build, while the **larger M2 Pro runner (Team/Enterprise only) cut that to 6 min 31 sec** — the fastest result in the benchmark . **The catch**: mobile-specific workflows require significant YAML configuration, and **code signing is DIY** . **Best for teams already on GitHub** wanting CI without a separate vendor, accepting that larger macOS runners require a paid GitHub plan .

- **[Xcode Cloud](https://developer.apple.com/xcode-cloud/)** — **Apple's first-party CI/CD, bundled with the Apple Developer Program ($99/year).** **Requires Xcode 15+, a remote Git repository, and automatic code signing enabled** . **Workflows support build, analyze, test, and archive actions** with automatic TestFlight distribution . **The hard limitation**: **Apple ecosystem only** — no Android, no cross-platform builds . **Best for small-to-medium iOS-only teams** wanting zero-configuration Apple-native CI without managing runners .

- **[GitLab CI/CD](https://about.gitlab.com/)** — **The DevOps platform with macOS runners (beta).** **Supports iOS builds via GitLab-hosted macOS runners** (`macos-14-xcode-15` images) with **fastlane integration for code signing** . **Best for teams already using GitLab** for source control and issue tracking, wanting CI in the same platform.

## Open-Source GitHub Projects

- **[Fastlane](https://github.com/fastlane/fastlane)** — **The de facto standard for mobile build automation and the open-source answer to iOS signing hell.** MIT licensed. **`match` stores certificates and provisioning profiles in an encrypted Git repository or cloud storage (Google Cloud, S3)** , giving every developer and CI machine identical signing assets . **The passphrase is stored as `MATCH_PASSWORD`** and each file is encrypted with openssl . **On CI, run match with `readonly: is_ci`** to prevent accidental certificate regeneration . **Beyond signing**: `gym` builds the IPA, `pilot` uploads to TestFlight, `deliver` manages App Store metadata, `snapshot` captures screenshots, and `supply` handles Android Play Store uploads . **Runs locally and on any CI** — GitHub Actions, GitLab CI, Bitrise, Jenkins — no vendor lock-in . **The security model**: even if your certificates leak, they can't be used without your App Store Connect credentials, which are stored in the local keychain, not git . **Best for any mobile team** that wants complete ownership of their build and signing process, regardless of which CI runs the lane.

- **[Oore CI](https://github.com/oore-ci/oore.build)** — **The self-hosted, Flutter-first mobile CI and internal distribution platform.** **Alpha status — APIs and CLI flags may change** . **Runs on macOS (arm64 or x86_64)** with a daemon (`oored`), operator CLI (`oore`), web UI, and OIDC authentication . **Five device roles** allow distributed setups: Complete (control plane + builds), Control plane, Runner, Web node, and CLI only — so builds can run across multiple Macs . **Best for Flutter teams** wanting self-hosted CI with distribution capabilities, accepting alpha-stage stability .

- **[Zealot](https://github.com/ai-aide/zealot)** — **The self-hosted beta distribution platform for iOS, Android, macOS, Linux, and Windows.** Open-source alternative to Pgyer/TestFlight . **Features**: multi-platform app hosting, **automatic iOS test device sync and one-click registration to the Apple Developer portal**, **REST API and iOS/Android SDKs**, **fastlane plugin** for automated uploads, **app metadata parsing**, and **third-party login** (Feishu, GitLab, GitHub, Google, LDAP, OIDC) . **Best for teams wanting a full-featured self-hosted TestFlight replacement** with device management and fastlane integration .

### Additional Strong Open-Source Options

- **Appium** — The free, code-first mobile automation foundation underneath most test clouds. **You own device procurement, USB hubs, battery health, and flaky host machines** — hardware upkeep is a real headcount cost. Best for teams with platform engineers wanting full control and zero license cost.
- **Zebrunner MCloud** — Self-hosted device farm for automated Appium tests and manual remote access to physical Android/iOS devices.

**Frameworks for building custom systems**: Combine **Fastlane** for build automation and code signing across any CI, **Zealot** for self-hosted beta distribution with device management, **Oore CI** for Flutter-first self-hosted CI, and **Bitrise** or **GitHub Actions** for the CI runner itself — to build a mobile deployment pipeline tailored to your platform (iOS vs Android vs cross-platform), signing complexity, and tolerance for vendor dependency.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- **iOS code signing is the most common reason mobile CI pipelines break** — certificates expire, provisioning profiles need renewal, and credentials must match across local machines and CI. **Fastlane match** stores signing assets in an encrypted Git repo so everyone uses identical credentials, and running `readonly: is_ci` on CI prevents accidental regeneration [citation:1][citation:8].
- **Build speed benchmarks are hardware-dependent** — a 2026 benchmark using a Flutter app showed GitHub Actions' larger M2 Pro runner (6 min 31 sec) beating Codemagic's M4 (6 min 58 sec) and Bitrise's M2 Pro Large (8 min 13 sec), while the standard GitHub M1 runner lagged at 12 min 18 sec [citation:4]. Validate against your specific project and machine tier.
- **Xcode Cloud is Apple-only** — Android and cross-platform teams need Bitrise, Codemagic, or GitHub Actions [citation:11].
- **Self-hosted distribution shifts responsibility to you** — storage durability, access control, and app binary retention become your operations, not a vendor's.
- Self-hosted open-source solutions require proper Docker deployment, TLS configuration for installation pages, and awareness that iOS ad-hoc distribution requires registered device UDIDs.

---

**Made for mobile engineers and release managers who want deployment pipelines they can debug and control.**
Let's make mobile CI/CD more open, signing-transparent, and self-hostable.
