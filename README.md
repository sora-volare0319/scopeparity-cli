# ScopeParity GitHub Action and CLI

ScopeParity compares literal Google OAuth scopes in Git-tracked source with a secret-free launch manifest and the evidence planned for each scope. The scan runs in the checked-out repository, requires no Google credentials, and returns a failing check for objective blockers or invalid inputs.

Google's Workspace IDE extension provides OAuth scope linting while you write code. ScopeParity complements it by checking parity across source, intended submission values, and demo-video evidence: https://developers.google.com/workspace/guides/developer-tools

## Guard pull requests

Commit an `oauth-evidence.yaml` manifest, then add this workflow:

```yaml
name: OAuth scope parity

on:
  pull_request:

permissions:
  contents: read

jobs:
  scopeparity:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@9c091bb21b7c1c1d1991bb908d89e4e9dddfe3e0 # v7.0.0
      - uses: sora-volare0319/scopeparity-cli@v1.0.0
        with:
          manifest: oauth-evidence.yaml
          report: scopeparity-report.html
```

The action uses the bundled CLI in this repository. It installs no project dependencies, sends no source or manifest data to ScopeParity, and does not opt into public URL checks. When objective blockers are found, the HTML report is written before the check returns its non-zero exit code.

For a monorepo, set `root` to the repository-relative project directory. `manifest` remains relative to that scan root; `report` is relative to the GitHub workspace.

## Keep the report (opt in)

Files created during a GitHub Actions job are not retained automatically. To keep the report in GitHub Actions storage, add this step after ScopeParity:

```yaml
      - name: Upload ScopeParity report
        if: always()
        uses: actions/upload-artifact@043fb46d1a93c77aae656e7c1c64a875d1fc6a0a # v7.0.1
        with:
          name: scopeparity-report
          path: scopeparity-report.html
          if-no-files-found: warn
```

This upload is optional and goes to the repository's GitHub Actions storage, not to ScopeParity.

## From parity check to launch evidence

The Action and every diagnostic finding stay free. When a project needs a versioned scope-evidence matrix, recording plan, provenance record, and repeatable evidence workflow, [preview the Launch Evidence Workspace](https://scopeparity.vercel.app/?utm_source=github&utm_medium=action-readme&utm_campaign=action-v1#pricing).

## Run locally

Create the secret-free manifest once:

```bash
npx -y github:sora-volare0319/scopeparity-cli#v0.1.4 init .
```

Review `oauth-evidence.yaml`, replace the example values with the launch values you intend to submit, then scan:

```bash
npx -y github:sora-volare0319/scopeparity-cli#v0.1.4 scan . --manifest oauth-evidence.yaml
```

Source, tests, fixtures, and security documentation live at https://github.com/sora-volare0319/scopeparity. The interactive report and exact-error guides are at https://scopeparity.vercel.app/.

ScopeParity finds deterministic technical inconsistencies. It does not provide legal or policy advice, inspect Google Cloud Console, assess restricted scopes, or guarantee Google approval.
