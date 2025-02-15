
# Rust library lambda_sqs

[![Crates.io][crates-badge]][crates-url]
[![MIT licensed][mit-badge]][mit-url]
[![Build Status][actions-badge]][actions-url]
[![Rust 1.46+][version-badge]][version-url]
[![FOSSA Status][fossa-badge]][fossa-url]
[![Docs][docs-badge]][docs-url]
[![BuyMeaCoffee][bmac-badge]][bmac-url]
[![GitHubSponsors][ghub-badge]][ghub-url]

[crates-badge]: https://img.shields.io/crates/v/lambda_sqs.svg
[crates-url]: https://crates.io/crates/lambda_sqs
[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-url]: https://github.com/jerusdp/lambda_sqs/blob/main/LICENSE
[actions-badge]: https://github.com/jerusdp/lambda_sqs/actions/workflows/general.yml/badge.svg?branch=main
[actions-url]: https://github.com/jerusdp/lambda_sqs/actions/workflows/general.yml
[version-badge]: https://img.shields.io/badge/rust-1.46+-orange.svg
[version-url]: https://www.rust-lang.org
[fossa-badge]: https://app.fossa.com/api/projects/custom%2B22707%2Fgithub.com%2Fjerusdp%2Flambda_sqs.svg?type=shield
[fossa-url]: https://app.fossa.com/projects/custom%2B22707%2Fgithub.com%2Fjerusdp%2Flambda_sqs?ref=badge_shield
[docs-badge]:  https://docs.rs/lambda_sqs/badge.svg
[docs-url]:  https://docs.rs/lambda_sqs
[bmac-badge]: https://badgen.net/badge/icon/buymeacoffee?color=yellow&icon=buymeacoffee&label
[bmac-url]: https://buymeacoffee.com/jerusdp
[ghub-badge]: https://img.shields.io/badge/sponsor-30363D?logo=GitHub-Sponsors&logoColor=#white
[ghub-url]: https://github.com/sponsors/jerusdp

Specialised lambda_runtime to accept and process events from SQS.

## SQS Events

SQS dispatches events to the a lambda function in batches (often, it seems
to my surprise). This crate provides a lambda_runtime implementation which
expects to receive a batch of messages in the [SqsEvent] type and provides
a method to transform the batch of events to a vector of your Struct.

## Example

```rust
use your_module::YourStruct;
use lambda_sqs::{handler_fn, Context, Error};
use lambda_sqs::SqsEvent;
#[tokio::main]
async fn main() -> Result<(), Error> {
    lambda_sqs::run(handler_fn(my_handler)).await?;
    Ok(())
}
pub async fn my_handler(e: SqsEvent, c: Context) -> Result<(), Error> {
    let events: Vec<YourStruct> = e.into_t();
#   // Process events
#   Ok(())
 }
```

## License

Licensed under either of

* Apache License, Version 2.0
   ([LICENSE-APACHE](LICENSE-APACHE) or [apache-url])
* MIT license
   ([LICENSE-MIT](LICENSE-MIT) or [mit-url])

at your option.

[apache-url]: http://www.apache.org/licenses/LICENSE-2.0
[mit-url]: http://opensource.org/licenses/MIT

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
