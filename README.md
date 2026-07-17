# ScopeParity CLI release

This repository is the dependency-free, bundled distribution of the open-source ScopeParity CLI. Source, tests, fixtures, and security documentation live at https://github.com/sora-volare0319/scopeparity. The interactive report and exact-error guides are at https://scopeparity.vercel.app/.

Create the secret-free manifest once:

```bash
npx -y github:sora-volare0319/scopeparity-cli#v0.1.2 init .
```

Review `oauth-evidence.yaml`, replace the example values with the launch values you intend to submit, then scan:

```bash
npx -y github:sora-volare0319/scopeparity-cli#v0.1.2 scan . --manifest oauth-evidence.yaml
```

The scan stays local by default and never requests Google credentials. Nothing is sent automatically. ScopeParity finds deterministic technical inconsistencies; it does not provide legal or policy advice, assess restricted scopes, or guarantee Google approval.
