# Security Policy

## Overview

This security policy applies to the **MON CS DOCS** content repository. We take security seriously and encourage responsible disclosure of any security-related concerns affecting the integrity, availability, or confidentiality of this project.

This repository contains documentation content, templates, configuration files, and project metadata. While it does not host production application code, we maintain security standards to protect contributors and users.

## Supported Versions

Security updates are applied to the current `main` branch. We do not maintain backports for older documentation versions. When security-relevant corrections are required (such as incorrect security guidance or outdated configurations), they are published immediately on the main branch and referenced in release notes where appropriate.

| Version | Supported          |
| ------- | ------------------ |
| main    | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

If you discover a security vulnerability in this repository, please report it through one of the following channels:

### Primary Channels

1. **Private Vulnerability Reporting** (Recommended)
   - Use GitHub's private vulnerability reporting feature
   - Navigate to the "Security" tab → "Report a vulnerability"
   - This creates a private security advisory visible only to repository maintainers

2. **Email**
   - Primary: [security.mon@moebiusorder.com](mailto:security.mon@moebiusorder.com)
   - Alternate: [mcdocs@moebiusorder.com](mailto:mcdocs@moebiusorder.com)

3. **Web Form**
   - Submit via: [mcdocs.moebiusorder.com/report](https://mcdocs.moebiusorder.com/report)

4. **GitHub Issue** (For non-sensitive security improvements only)
   - Use for security enhancements or policy clarifications
   - Do NOT use for active vulnerabilities or sensitive disclosures

### What to Include

When reporting a vulnerability, please provide:

- **Description**: Clear explanation of the issue and potential impact
- **Location**: Affected files, paths, or configuration elements
- **Reproduction Steps**: Detailed steps to verify the vulnerability
- **Proof of Concept**: Code, commands, or screenshots demonstrating the issue
- **Impact Assessment**: Your evaluation of severity and potential exploitation
- **Suggested Fix**: If you have recommendations for remediation

### What NOT to Report

The following are generally out of scope:

- Vulnerabilities in third-party services (hosting providers, CDN, GitHub infrastructure)
- Issues in the proprietary MON CS DOCS platform application (not present in this repository)
- Typographical errors or editorial content issues without security implications
- Social engineering or phishing attempts unrelated to repository security
- Denial of service against GitHub infrastructure

## Response Process

### Timeline

- **Acknowledgment**: We will acknowledge receipt of your report within **48 hours**
- **Initial Assessment**: Triage and severity assessment within **5 business days**
- **Status Updates**: Regular updates every **7 days** until resolution
- **Resolution**: Critical issues will be addressed within **30 days** when feasible

### Severity Classification

We use the following severity levels:

- **Critical**: Immediate threat to user safety, data integrity, or widespread exploitation
- **High**: Significant impact with clear exploitation path
- **Medium**: Moderate impact requiring specific conditions
- **Low**: Limited impact or theoretical vulnerability
- **Informational**: Security improvements or best practice recommendations

### Coordinated Disclosure

- We practice **responsible disclosure** and will work with you to coordinate public release
- Security fixes will be deployed before public disclosure whenever possible
- We request a **90-day disclosure window** for critical vulnerabilities to allow adequate remediation time
- Credit will be given to researchers who report valid vulnerabilities (unless anonymity is requested)

## Security Measures

This repository implements the following security controls:

### GitHub Security Features

- **Private Vulnerability Reporting**: Enabled for confidential security disclosures
- **Dependabot Alerts**: Automated scanning for vulnerable dependencies
- **Dependabot Security Updates**: Automatic pull requests for dependency patches
- **Secret Scanning**: Detection of accidentally committed credentials or tokens
- **Push Protection**: Prevents commits containing detected secrets
- **Dependency Graph**: Visibility into all project dependencies

### Access Controls

- **Branch Protection**: Main branch requires pull request reviews
- **Code Owners**: Designated maintainers review all changes
- **Two-Factor Authentication**: Required for all maintainers with write access
- **Audit Logging**: All repository activities are logged

### Contribution Security

- All contributions are reviewed before merging
- CI/CD workflows use minimal permissions
- External contributions are reviewed for malicious content
- No executable code is accepted in documentation contributions

## Security Best Practices for Contributors

If you contribute to this repository:

- **Never commit secrets**: No API keys, passwords, tokens, or credentials
- **Review dependencies**: Ensure any tooling dependencies are from trusted sources
- **Sign commits**: Use GPG signing for commit verification (recommended)
- **Follow style guide**: Adhere to security guidelines in CONTRIBUTING.md
- **Report concerns**: If you notice something suspicious, report it immediately

## Vulnerability Disclosure Policy

When a vulnerability is confirmed:

1. **Private Fix**: A patch is developed privately in a security advisory
2. **Testing**: The fix is validated against the reported vulnerability
3. **Release**: A new version is released with the security fix
4. **Notification**: Security advisory is published with details and attribution
5. **Communication**: Relevant parties are notified (sponsors, major users, security lists)

### Public Disclosure

Security advisories are published at:
- GitHub Security Advisories: [https://github.com/Moebius-Order/moncsdocs/security/advisories](https://github.com/Moebius-Order/moncsdocs/security/advisories)
- Release Notes: Referenced in relevant version release notes
- Website: [https://mcdocs.moebiusorder.com/security](https://mcdocs.moebiusorder.com/security)

## Hall of Fame

We recognize security researchers who responsibly disclose vulnerabilities:

- This section will list contributors who have helped improve MON CS DOCS security
- Recognition is provided unless anonymity is requested
- Acknowledgment is included in security advisories and release notes

## Contact

For security-related questions or concerns:

- **Security Team**: [security.mon@moebiusorder.com](mailto:security.mon@moebiusorder.com)
- **General Inquiries**: [mcdocs@moebiusorder.com](mailto:mcdocs@moebiusorder.com)
- **Report Form**: [mcdocs.moebiusorder.com/report](https://mcdocs.moebiusorder.com/report)
- **Community**: [https://t.me/moncsdocs](https://t.me/moncsdocs) (for non-sensitive discussions only)

## Additional Resources

- **Contributing Guidelines**: [CONTRIBUTING.md](CONTRIBUTING.md)
- **Code of Conduct**: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
- **License**: [LICENSE](LICENSE)
- **Platform Security**: Infrastructure security managed separately by Moebius Order

---

**Last Updated**: February 28, 2026

© 2026 Moebius Order. This security policy is licensed under CC BY-SA 4.0.
