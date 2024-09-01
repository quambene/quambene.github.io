# Eric Release: Rust bindings for the German tax library

_First published on [Reddit](https://www.reddit.com/r/rust/comments/1eurk6n/rust_bindings_for_the_german_tax_library) (2024-08-17)._

Is Rust used in the tax software industry? No. But will it become more important
in the future? Also no.

For everybody else (i.e. mainly cats and dolphins), I made the [Rust
bindings](ttps://crates.io/crates/eric-bindings) and
[SDK](https://crates.io/crates/eric-sdk) for the Elster Rich Client (Eric). Eric
is a shared C library provided by the German tax administration which is
integrated into a tax application.

The Eric bindings were generated using
[bindgen](https://crates.io/crates/bindgen) which was a very smooth experience.

The functionality of the Eric SDK is currently kept simple (see
<https://docs.rs/eric-sdk/latest/eric_sdk/struct.Eric.html>). It takes an XML
file in the XBRL standard for a specified taxonomy, like the company balance
sheet, income statement, or any other event in the context of tax declaration,
and checks the provided data for plausibility. The validated XML file can then
be sent to the tax authorities.

The `eric-bindings` and `eric-sdk` were released in v0.4.1 and v0.3.1. Check out the repo for more information: <https://github.com/quambene/eric-rs>.
