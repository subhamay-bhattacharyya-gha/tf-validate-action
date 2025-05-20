# GitHub Composite Action for Terraform Validate

![Release](https://github.com/subhamay-bhattacharyya-gha/tf-validate-action/actions/workflows/release.yaml/badge.svg)&nbsp;![Commit Activity](https://img.shields.io/github/commit-activity/t/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Last Commit](https://img.shields.io/github/last-commit/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Release Date](https://img.shields.io/github/release-date/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Repo Size](https://img.shields.io/github/repo-size/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![File Count](https://img.shields.io/github/directory-file-count/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Issues](https://img.shields.io/github/issues/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Top Language](https://img.shields.io/github/languages/top/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Custom Endpoint](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/bsubhamay/bc727a7bfdc54056933718e073c39753/raw/tf-validate-action.json?)

Validate Terraform configuration in your CI pipeline using this GitHub Composite Action. It checks for formatting and structural issues in Terraform files and provides a pass/fail output for workflow automation.

---

## 📘 Description

This composite GitHub Action performs the following Terraform validation tasks:
- Initializes Terraform (`terraform init`)
- Checks code formatting (`terraform fmt`)
- Validates configuration structure (`terraform validate`)
- Provides visual feedback in the GitHub Actions summary
- Can optionally continue even if validation fails (`soft-fail`)

---

## 🔧 Inputs

| Name                 | Description                                       | Required | Default |
|----------------------|---------------------------------------------------|----------|---------|
| `working-directory`  | Directory containing Terraform configuration files| No       | `.`     |
| `soft-fail`          | Continue workflow even if validation fails        | No       | `false` |

---

## 📤 Outputs

| Name    | Description                                 |
|---------|---------------------------------------------|
| `valid` | `true` if validation passed, `false` if not |

---

## ✅ Behavior

- Fails the job if the Terraform code is not formatted or contains structural errors.
- Sets a `valid` output variable for downstream steps.
- Prints pass/fail messages in both console output and GitHub Actions summary.
- Optionally continues on failure when `soft-fail: true`.

---

## 🚀 Usage

```yaml
jobs:
  tf-validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Terraform Validate
        uses: subhamay-bhattacharyya-gha/tf-validate-action@main
        with:
          working-directory: tf
          soft-fail: false

      - name: Display Status
        run: |
          echo "Validation Passed: ${{ steps.validate.outputs.valid }}"
```

## License

MIT
