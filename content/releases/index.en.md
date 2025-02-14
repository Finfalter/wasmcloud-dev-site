---
title: "Release History / Changelog"
description: "This is a high-level overview of the additions, removals, and changes for releases of wasmcloud and related tooling. This is not a complete list. For all of the specific details, check out the release notes for each release in the appropriate repository."
layout: "changelog"
draft: false
---

### Release 0.50 

{{< changelog "added" >}}
- The wasmcloud host has been ported to Elixir (OTP) to provide greater flexibility, scalability and reliability. Actor and Capability providers won't see any elixir code, but this change is expected to make it easier to develop several features on the roadmap.
- A new dashboard, built with Phoenix, shows the status of the lattice, and enables starting and stopping actors and capability providers.
- A new host implementation in JavaScript that runs in the browser or on nodejs. A WebAssembly actor can be deployed without changes to any host - on linux, macos, windows, or in a browser.
{{</ changelog >}}

{{< changelog "changed" >}}

- Capability providers communicate with the wasmcloud host over a secure protocol via NATS, rather than being loaded as a library (as they were with host versions <= 0.18). This change allows us to support capability providers written in languages other than Rust, and is more flexible
- The Interface Definition Language (IDL) has changed from WIDL to Smithy, and a new code generator generates code from smithy libraries.

{{</ changelog >}}




### Release 0.18.0
{{< changelog "added" >}}
* Actor and Provider name and revision are now included with the control interface `HostInventory` query ([PR #154](https://github.com/wasmCloud/wasmCloud/pull/154)). Names and revisions are not displayed yet with `wash`'s `ctl get inventory` command.
* Released `wash` `v0.4.0`, the integrated REPL environment no longer requires NATS to run which dramatically simplifies the onboarding experience ([`wash` PR #107](https://github.com/wasmCloud/wash/pull/107))
* `get_actor_identity` and `get_provider_identity` functions on the Host API for retrieving the name, image reference, and revision number of an actor or provider respectively ([PR #163](https://github.com/wasmCloud/wasmCloud/pull/163))
* `--nsprefix` option on the `wasmcloud` binary which allows you to set a namespace other than "default" with the stock `wasmcloud` binary ([PR #161](https://github.com/wasmCloud/wasmCloud/pull/161))
* Configured a Gitpod environment for a complete pre-configured in-browser development environment for `wasmcloud`. ([PR #162](https://github.com/wasmCloud/wasmCloud/pull/162))
{{</ changelog >}}

{{< changelog "changed" >}}
* Control interface and lattice WIDL files are now stored in the `wasmcloud` repository instead of `capability-providers` ([PR #154](https://github.com/wasmCloud/wasmCloud/pull/154))
* Host API `providers()` function now returns a Vec of 3-tuples (public_key, contract_id, link_name) - was previously just public key
{{</ changelog >}}

{{< changelog "Fixed" >}}
* Fixed a bug where the control interface and host API could incorrectly report the OCI image reference of an actor or provider. ([PR #159](https://github.com/wasmCloud/wasmCloud/pull/159) and [PR #163](https://github.com/wasmCloud/wasmCloud/pull/163))
* Fixed a bug where live updating an actor would not update the stored OCI image references ([PR #160](https://github.com/wasmCloud/wasmCloud/pull/160))
{{</ changelog >}}


### Release 0.17.0
{{< changelog "added" >}}
* Added additional logging and error messages to common operations ([PR #143](https://github.com/wasmCloud/wasmCloud/pull/143) and [PR #148](https://github.com/wasmCloud/wasmCloud/pull/148))
* Added the ability to remove a link on the Host API and control interface ([PR #147](https://github.com/wasmCloud/wasmCloud/pull/147))
* Added extensive Rust documentation on the `wasmcloud_host` crate ([PR #151](https://github.com/wasmCloud/wasmCloud/pull/151))
* Added additional queries to the Host API to query the lattice cache. This allows users directly invoking the Host API to retrieve the same information available via the control interface ([PR #153](https://github.com/wasmCloud/wasmCloud/pull/153))
{{</ changelog >}}

{{< changelog "Fixed" >}}
* Fixed an issue where operations could be called on a host that had not started ([PR #142](https://github.com/wasmCloud/wasmCloud/pull/142))
{{</ changelog >}}

### Release 0.16.0
The **0.16.0** release includes multiple bug fixes, documentation improvements, and additional features.

{{< changelog "added" >}}
* Added `bencher` sample for determining wasmcloud performance ([PR #100](https://github.com/wasmCloud/wasmCloud/pull/100))
{{</ changelog >}}

{{< changelog "changed" >}}
* Renamed `wascc-codec` to `wasmcloud-provider-core` ([PR #102](https://github.com/wasmCloud/wasmCloud/pull/102))
* Updated embedded Extras provider to use `wasmcloud:extras` capability contract ([PR #109](https://github.com/wasmCloud/wasmCloud/pull/109))
* Updated `actix-rt` to `2.1.0` which is based on `tokio 1.X`. This is a breaking change for users that embed a `wasmcloud-host` in their Rust program. ([PR #114](https://github.com/wasmCloud/wasmCloud/pull/114) and [PR #135](https://github.com/wasmCloud/wasmCloud/pull/135))
* Changed fields on the `Host` struct to allow it to be sent between threads ([PR #132](https://github.com/wasmCloud/wasmCloud/pull/132))
{{</ changelog >}}

{{< changelog "Fixed" >}}
* Fixed a bug where loading a capability provider caused a SIGSEGV on Linux ([PR #99](https://github.com/wasmCloud/wasmCloud/pull/99))
* Fixed a bug where the live update operation didn't allow for differing OCI references ([PR #128](https://github.com/wasmCloud/wasmCloud/pull/128))
{{</ changelog >}}

### Release 0.15.0

The **0.15.0** release is the single biggest release we've had since the project began. It is essentially a bottom-up rewrite of the entire wasmcloud host runtime. In addition to this internal rewrite, we've incorporated lessons learned from the past year of development and applied those to the way we build capability providers, define actor interfaces, and support the developer experience. The core theme of this release is the ruthless focus on developer experience.

{{< changelog "added" >}}

* Consolidated multiple CLI tools (`nk`, `wascap`, etc) into the new wasmcloud shell [wash](https://github.com/wasmcloud/wash)
* Added a fully functioning REPL to the `wash` CLI
* Provider archives - allows for the bundling of multiple OS/CPU native libraries into a single archive
* **OCI** support - You can now deploy actors and capability providers into a host/lattice from an OCI registry
* First-party capability providers and sample actors are all available in our OCI registry `wasmcloud.azurecr.io`
* `wasmcloud` and `wash` are now installable via package cloud, homebrew, and other convenient methods

{{</ changelog >}}

{{< changelog "changed" >}}

* Completely rewrote the `wasmcloud-host` crate to allow for easier maintenance and adding features
* The [wasmcloud-host](https://crates.io/crates/wasmcloud-host) crate is now entirely `async` and based on the `actix` framework
* Too many others to list here...

{{</ changelog >}}

<hr/>
<!-- Below are all of the changelog markdown formats that we use -->
<!-- {{< changelog "added" >}}
{{</ changelog >}} -->

<!-- {{< changelog "changed" >}}
{{</ changelog >}} -->

<!-- {{< changelog "Removed" >}}
{{</ changelog >}} -->

<!-- {{< changelog "Fixed" >}}
{{</ changelog >}} -->

<!-- {{< changelog "Security" >}}
{{</ changelog >}} -->

<!-- {{< changelog "Unreleased" >}}
{{</ changelog >}} -->