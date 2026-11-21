<img src="assets/logo.png" width="112" height="112" alt="CivilOffset logo">

# CivilOffset

Convert a local tick to a candidate UTC tick for a supplied offset. This Blyx library is part of the calendar, scheduling and local time collection.

One wall time can occur twice during a fall-back transition and disappear entirely during a forward jump. Expose the number of valid UTC candidates. [PEP 495, local time disambiguation](https://peps.python.org/pep-0495/)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-civiloffset.git
cd blyx-civiloffset
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-civiloffset) · [Package page](https://www.blyx-lang.space/packages/civiloffset) · [Handbook](https://doc.blyx-lang.space/guide/blackbird)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-civiloffset.git vendor/civiloffset
```

```blyx
use vendor::civiloffset::civiloffset;

fn main() {
    let local = 7200.0;
    let offset = 3600.0;
    let result = civiloffset_candidate(local, offset);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
3600
3600
```

## API

`civiloffset_candidate(local, offset)`

Returns [candidate UTC, offset]. Offsets use seconds and must lie strictly within ±24 hours. Local ticks use the same epoch and unit. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| local | A exact signed integer |
| offset | A exact signed integer |

## In use

[Blackbird](https://github.com/Rahulchaube1/blyx-blackbird) uses this module to resolve a wall-clock timestamp at a known gap or fold without guessing its offset.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-civiloffset/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
