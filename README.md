# SBOM and SLSA supply chain demo
Sample Flask app with deliberately outdated dependencies, plus a GitHub Actions pipeline:
Syft (SBOM) -> Grype (scan) -> Cosign keyless (sign + verify).

## Run locally
    syft dir:. -o cyclonedx-json=sbom.cdx.json
    grype sbom:sbom.cdx.json
    cosign generate-key-pair
    cosign sign-blob --key cosign.key --output-signature sbom.sig sbom.cdx.json
    cosign verify-blob --key cosign.pub --signature sbom.sig sbom.cdx.json
Change one character in sbom.cdx.json and verify again: it fails.

## Evidence (real runs)
See evidence/: Syft SBOM (6 Python packages + 5 GitHub Actions), scan summary, Cosign tamper test and run-output.txt.

## CI
Push to GitHub; the workflow runs automatically. Note: the workflow has not been run on GitHub yet; check the Actions tab on first push.
