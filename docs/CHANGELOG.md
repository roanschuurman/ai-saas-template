# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Initial project template structure
- Mobile stack configuration (Flutter/Dart)
- SaaS stack configuration (Next.js/TypeScript)
- 8-step unified workflow
- Quality gates documentation
- Development instruction files

## Template Structure

Each release should follow this format:

## [X.Y.Z] - YYYY-MM-DD

### Added
- New features, capabilities, or major enhancements
- New documentation or guides

### Changed
- Changes to existing functionality
- Updates to dependencies or configurations
- Process improvements

### Deprecated
- Features that will be removed in future versions
- Old patterns or approaches to avoid

### Removed
- Features or capabilities that were removed
- Cleanup of deprecated functionality

### Fixed
- Bug fixes and corrections
- Security vulnerability patches

### Security
- Security-related changes or improvements
- Vulnerability disclosures and fixes

## Iteration-Specific Entries

When using this template for actual projects, each iteration should add entries like:

### [1.2.3+auth-login.i05] - 2025-08-22

### Added
- Biometric authentication support for iOS/Android [i05]
- Fallback PIN entry when biometrics fail [i05]
- Login attempt rate limiting [i05]

### Changed
- Updated login flow to support multiple auth methods [i05]
- Improved error messaging for auth failures [i05]

### Fixed
- Fixed TouchID prompt appearing on unsupported devices [i05]

### Technical Notes
- Test coverage: 95% (auth module)
- Performance: Login time reduced by 40%
- Security: Added rate limiting and improved session management

---

## Conventions

### Version Format
- Template updates: `X.Y.Z` (semantic versioning)
- Feature iterations: `X.Y.Z+feature-slug.iNN` (where iNN is iteration number)

### Entry Categories
- **Added**: New functionality or features
- **Changed**: Modifications to existing functionality  
- **Deprecated**: Features marked for future removal
- **Removed**: Features that were deleted
- **Fixed**: Bug fixes and corrections
- **Security**: Security-related changes

### Commit Reference
Each entry should reference the acceptance test IDs and commit hashes where possible.

---

*This changelog is automatically updated during the Deploy step (07) of each iteration.*
