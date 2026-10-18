# MageLift community alpha acceptance fixture

Public snapshot of Magento Open Source **2.4.9** with CE isolated security patches
documented in [ACCEPTANCE_SECURITY_PATCHES.md](ACCEPTANCE_SECURITY_PATCHES.md). Upstream
baseline: [magento/magento2 tag 2.4.9](https://github.com/magento/magento2/tree/2.4.9)
(commit `755e34dd689021c5165db9d35ecff74f7dc51527` on that line).

## Acceptance status

| Check | Status |
| --- | --- |
| Signed CLI/provider installation without host Go/PHP/Node | PASS |
| GCP bootstrap and reviewed CI IAM application | PASS |
| Cloud deploy (GCP) | PASS on the retained campaign, runs 39153317832 and 39156876510 |
| Cloud destroy (GCP) | campaign teardown follows those runs; this table is not a cleanup certificate |
| Composer `install` in CI | expected in fixture pipelines |
| Magento functional tests | **NOT_RUN** in this tree |

This directory is a **reference fixture** for MageLift community alpha acceptance.
It is not a production topology or sizing recommendation.

## Images and registry

Acceptance CI builds container images in **your** registry from this source. MageLift
does not publish a central Magento image catalog for this alpha.

## Configuration in CI

`magelift.yaml` here uses placeholder GCP project `example-gcp-project` and domain
`shop.example.com`. Project name `magelift-org249-ec2a332` is kept only to label this
acceptance scenario.

The YAML that actually targets your cloud account is **not** interpolated from product
defaults. Maintainers supply it through the repository variable
`MAGELIFT_ACCEPTANCE_CONFIG`; fixture-only CI customization materializes that content
for runs (workflows are added separately).

## Provenance

Upstream copyrights, `LICENSE*`, and `COPYING.txt` are unchanged. See also
[.magelift-acceptance.md](.magelift-acceptance.md).

The workflow starts from the CLI-generated single-test recipe. Fixture-only
customization materializes target YAML into ignored magelift.acceptance.yaml after checkout and compares the configured
GCP project with its repository variable. Its build condition also corrects an
undefined dispatch input in this canary's test-only generator; the source fix is
committed separately. Pull requests validate placeholder configuration and cannot
run the build or deploy jobs. Push to `main` no longer deploys. Restore
`push: branches: [main]` in `.github/workflows/magelift.yml`, or run
`workflow_dispatch`, to deploy again. A dispatch recreates cloud resources.
Cloud trust accepts only this repository's main
workflow and its build/test environments.

Build results are written under RUNNER_TEMP, keeping the committed source clean. The tracked placeholder YAML is never rewritten during CI.
