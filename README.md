# ScopeParity CLI release

This repository is the dependency-free, bundled distribution of the open-source ScopeParity CLI. Source, tests, fixtures, and security documentation live at https://github.com/sora-volare0319/scopeparity.

Run the current GitHub distribution:

```bash
npx -y github:sora-volare0319/scopeparity-cli scan . --manifest oauth-evidence.yaml
```

The scan stays local by default and never requests Google credentials. ScopeParity finds deterministic technical inconsistencies; it does not provide legal or policy advice, assess restricted scopes, or guarantee Google approval.
