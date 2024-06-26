# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

* `Config::custom_comments`
* `Revisioned::custom`
* `Flag` trait for custom `//@` flags
* `Build` trait for custom aux/dep build
    * `BuildManager` for deduplicating these builds on a per-`Config` basis

### Fixed

### Changed

* removed `Revisioned::no_rustfix` in favor of turning that into a rustc-specific custom flag
* removed `Revisioned::edition` in favor of turning that into a rustc-specific custom flag
* removed `Revisioned::needs_asm_support` in favor of turning that into a rustc-specific custom flag
* replaced `Mode::Run` with a rustc-specific run flag
* replaced rustfix with a rustc-specific rustfix flag
* replaced `rustfix` fields of `Mode::Fail` and `Mode::Yolo` by instead overwriting the rustc-specific custom flag
* aux builds and dependencies are now built *per* `Config` instead of being built just for the first `Config` and the result shared by the others
    * the configs could be different enough that aux builds built with a different config are incompatible (e.g. different targets).
* replaced `Revisioned::aux_builds` with a rustc-specific custom flag
* replaced `dependency_builder` and `dependency_manifest_path` with `DependencyBuilder` `Flag` that you an add to the default comments.

### Removed

## [0.22.3] - 2024-04-05

### Added

* Reexporting `eyre::Result` at the root level

### Fixed

* Passing `--target` to build command when cross-compiling.

### Changed

### Removed

## [0.22.2] - 2024-02-27

### Added

### Fixed

### Changed

* `spanned` dependency bump to lower `bstr` to `1.6.0` to resolve windows linker issues with `1.7`

### Removed

## [0.22.1] - 2024-02-16

### Added

* Add `//~v` comments to put an error matcher above the error site.

### Fixed

* Give aux builds the default comment config, too

### Changed

### Removed

## [0.22.0] - 2024-01-24

### Added

* Started maintaining a changelog
* `Config::comment_defaults` allows setting `//@` comments for all tests
* `//~` comments can now specify just an error code or lint name, without any message. ERROR level is implied
* `Revisioned::diagnostic_code_prefix` allows stripping a prefix of diagnostic codes to avoid having to repeat `clippy::` in all messages

### Fixed

* report an error instead of panicking when encountering a suggestion that does not belong to the main file.
* number of filtered tests is now > 0 when things actually got filtered.

### Changed

* crate-private span handling was passed off to the `spanned` crate, improving some diagnostics along the way.
* `Config::output_conflict_handling` does not contain the bless command message anymore, it is instead available separately as `Config::bless_command`
* Updating `cargo_metadata` to `0.18`
* Updated `spanned` to `0.1.5`, giving more precise spans for more iterator operations
* `Config::cfgs` is now `Config::program::cfg_flag`
* Bumped `annotate-snippets` to `0.10`

### Removed

* `$DIR` and `RUSTLIB` replacements
* `Config::edition` (replaced by `config.comment_defaults.base().edition`)
* `Config::filter_stdout` (replaced by `config.comment_defaults.base().normalize_stdout`)
* `Config::filter_stderr` (replaced by `config.comment_defaults.base().normalize_stderr`)
* `Config::mode` (replaced by `config.comment_defaults.base().mode`)

## [0.21.2] - 2023-09-27
