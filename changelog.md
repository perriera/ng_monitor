# Changelog

> All notable changes to this project will be documented in this file.</br>
> The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), </br>
> and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).</br>
> To add a tag to the git repository do:
>
> > git tag -a v0.5.0 -m " Using extras_mon v0.3.0"</br>
> > git push origin v0.5.0

IMPORTANT:

- Manually keep the changelog version number in sync with CMakeLists.txt project version.<br>
- Keep the changelog.md up to date, neat and tidy, (as it is a convenient tool for code maintenance).<br>
- Use [Semantic Versioning](https://semver.org/spec/v2.0.0.html) such that<br>
- Given a version number MAJOR.MINOR.PATCH, increment the:<br>
- MAJOR version when you make incompatible API changes,<br>
- MINOR version when you add functionality in a backwards compatible manner, and<br>
- PATCH version when you make backwards compatible bug fixes. <br>
- But there is no need to change the version number for correcting spelling errors, (etc).<br>
- MAKE SURE to tag and update the tag compare list below, (for quick code comparison purposes).<br>

## [Unreleased]

Detailed test cases</br>
Detailed class descriptions in README.md</br>
Correct URL for github, (for source compare)</br>

## [Next Steps]

#### 0.5.0 (2021-12-21)

### Changed

- Using extras_mon v0.3.0

#### 0.4.0 (2021-12-21)

### Changed

- Using extras_rsi v4.16.0

#### 0.3.0 (2021-12-21)

### Changed

- Using extras_rsi v4.15.0

#### 0.2.0 (2021-12-21)

### Changed

- Project name

#### 0.1.0 (2021-08-26)

### Added

- Fetch_Content support
- changelog.md
- Project VERSION inside CMakeLists.txt & changelog.md
- Adopted new changelog format.
- sudo make install parameters
- shared library support
- sudo checkinstall support
- GoF: Abstract design pattern support
- Debian package support
- extra/interfaces.hpp support
- Unit test casses support, (Catch2)
- Mock framework support, (FakeIt)

### Changed

- CMakeLists.txt revamped & streamlined
- README.md revamped & streamlined
- Added documentation on code
- cxx_std_17 on all targets
- std::filesystem on all targets

### Maintained

- @brief style formatting
- Doxygen support

[unreleased]: https://github.com/perriera/ng_monitor/compare/v0.5.0...HEAD
[0.5.0]: https://github.com/perriera/ng_monitor/compare/v0.4.0...v0.5.0
[0.4.0]: https://github.com/perriera/ng_monitor/compare/v0.3.0...v0.4.0
[0.3.0]: https://github.com/perriera/ng_monitor/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/perriera/ng_monitor/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/perriera/ng_monitor/releases/tag/v0.1.0
