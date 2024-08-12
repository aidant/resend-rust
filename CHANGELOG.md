# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

<!-- ## [Unreleased] -->

## [0.9.0] - 2024-08-12

### Added

- `email.scheduled_at` field (and `emails::with_scheduled` method for setting it)
- `emails::update` method
- `emails::cancel_schedule` method

### Changed

- The following structs had all their fields made private in order to prevent future breaking
  changes when new fields are added. Simply use the relevant builder methods instead.
  [GitHub issue](https://github.com/resend/resend-rust/issues/15).

  - `CreateEmailBaseOptions`
  - `ContactData`
  - `ContactChanges`
  - `CreateDomainOptions`
  - `DomainChanges`
  - `UpdateEmailOptions`

## [0.8.1] - 2024-07-11

### Changed

- `Email.text` is now optional

### Fixed

- The `cc`, `bcc` and `text` fields of the `Email` struct are nullable which broke deserialization.
  It now works as expected.

## [0.8.0] - 2024-07-05

### Added

- `rate_limit` module
- `Error::RateLimit`

## [0.7.0] - 2024-07-01

### Added

- `Attachment::with_content_type` method and `content_type` field
- `Error::Parse` variant

### Changed

- HTML server responses instead of proper JSON errors (which should mostly happen in outages)
  now have better error messages


## [0.6.0] - 2024-06-16

### Changed

- `RATE_LIMIT` to `RESEND_RATE_LIMIT` to avoid potential collisions with other libs

### Removed

- Outdated doc comment from `Client::user_agent`

## [0.5.2] - 2024-06-10

### Added

- `DomainChanges::with_tls` method
- docs for `Domain.Tls` enum options

## [0.5.1] - 2024-06-08

### Changed

- Moved Github URLs from `resend-rs` to `resend-rust` (no code changes)

## [0.5.0] - 2024-06-08

### Added

- `DomainChanges.tls`
- Rate limiting (default 9/s), configurable with `RATE_LIMIT` env variable (async only)

### Changed

- renamed `SendEmail` to `CreateEmailBaseOptions`
- renamed `email.retrieve` to `email.get`
- renamed `SendEmailResponse` to `CreateEmailResponse`
- renamed `ApiKeyData` to `CreateApiKeyOptions`
- renamed `domains.DomainData` to `CreateDomainOptions`
- `email.send` now returns a `CreateEmailResponse` instead of an `EmailId`
- `batch.send` now returns a `Vec<CreateEmailResponse>` instead of a `Vec<EmailId>`
- `audiences.create` now returns `CreateAudienceResponse` instead of `AudienceId`
- `contacts.update` now returns `UpdateContactResponse`
- `domains.update` now returns `UpdateDomainResponse`
- moved batch related stuff to a new module
- `email.send_batch` is now `batch.send`
- moved error stuff from `config` to their own `error` module
- removed `[...]Id` types from function arguments
- implemented `Deref<str>` for all `[...]Id` types
- `DomainRecord` has been converted to an enum for better/more detailed type handling
- `Domain.records` is now optional
- `Email.to` is now a vec
- `contacts.delete_by_email` and `contacts.delete_by_contact_id` now return the `deleted` boolean
- Renamed `Client` to `Resend`
- `Domain` no longer has the `dns_provider` field.
- `Domain.delete` now returns a `DeleteDomainResponse` 
- `Email.Tag.value` is no longer an optional
- `Email.html` and `Email.reply_to` are now both optional

### Deleted

- removed ability to configure user agent via `RESEND_USER_AGENT` (this is no longer configuable)
- `email.with_value`, use the `new` constructor instead
- `impl<T: AsRef<str>> From<T> for Tag` is removed since Tag now also needs a value
- `ContactChanges.email` and `ContactChanges.with_email`

## [0.4.0] - 2024-05-01

`@martsokha` basically rewrote the entire repository 0_0
([pr](https://github.com/resend/resend-rust/pull/1))

The crate now supports the entire Resend API surface, check the
[docs](https://docs.rs/resend-rs/latest/resend_rs/) for examples.

## [0.3.0] - 2024-02-06

### Changed

- `Mail::new` now accepts a list of `to` addresses and thus supports sending an
  email to multiple recipients.

  ```rs
  // Before:
  let mail = Mail::new("from1", "to1", "subject1", "html1");

  // Now
  let mail = Mail::new("from1", &["to1"], "subject1", "html1");
  ```

## [0.2.0] - 2023-07-10

Disabled `reqwest`'s default features and enabled `rustls-tls`.

## [0.1.0] - 2023-07-10

Initial release.

[0.9.0]: https://crates.io/crates/resend-rs/0.9.0
[0.8.1]: https://crates.io/crates/resend-rs/0.8.1
[0.8.0]: https://crates.io/crates/resend-rs/0.8.0
[0.7.0]: https://crates.io/crates/resend-rs/0.7.0
[0.6.0]: https://crates.io/crates/resend-rs/0.6.0
[0.5.2]: https://crates.io/crates/resend-rs/0.5.2
[0.5.1]: https://crates.io/crates/resend-rs/0.5.1
[0.5.0]: https://crates.io/crates/resend-rs/0.5.0
[0.4.0]: https://crates.io/crates/resend-rs/0.4.0
[0.3.0]: https://crates.io/crates/resend-rs/0.3.0
[0.2.0]: https://crates.io/crates/resend-rs/0.2.0
[0.1.0]: https://crates.io/crates/resend-rs/0.1.0
