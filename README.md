# GitHub Composite Action for Terraform Validation and Formatting

![Release](https://github.com/subhamay-bhattacharyya-gha/tf-validate-action/actions/workflows/release.yaml/badge.svg)&nbsp;![Commit Activity](https://img.shields.io/github/commit-activity/t/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Last Commit](https://img.shields.io/github/last-commit/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Release Date](https://img.shields.io/github/release-date/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Repo Size](https://img.shields.io/github/repo-size/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![File Count](https://img.shields.io/github/directory-file-count/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Issues](https://img.shields.io/github/issues/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Top Language](https://img.shields.io/github/languages/top/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Custom Endpoint](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/bsubhamay/bc727a7bfdc54056933718e073c39753/raw/tf-validate-action.json?)

Validate and format Terraform configuration in your CI pipeline using this GitHub Composite Action. This action ensures that your Terraform code is properly formatted and structurally valid without requiring backend state management. Perfect for pre-commit checks, pull request validation, and CI/CD pipelines.

---

## 📘 Description

This composite GitHub Action performs the following tasks for Terraform code quality:
- Checks out the repository at a specific release tag or current branch
- Initializes Terraform without backend configuration (downloads providers only)
- Checks code formatting (`terraform fmt`)
- Validates configuration syntax (`terraform validate`)
- Supports soft-fail behavior to continue even on validation errors
- Outputs a `valid` result for use in conditional downstream steps

---

## 🔧 Inputs

| Name             | Description                                                                 | Required | Default   |
|------------------|-----------------------------------------------------------------------------|----------|-----------|
| `terraform-dir`  | Relative path to the directory containing Terraform configuration files     | No       | `tf`      |
| `release-tag`    | Git release tag to check out. If omitted, the current branch is used        | No       | `''`      |
| `soft-fail`      | Set to `'true'` to continue the workflow even if formatting or validation fails | No   | `true`    |

---

## 📤 Outputs

| Name    | Description                                      |
|---------|--------------------------------------------------|
| `valid` | `true` if validation passed, `false` if it failed |

---

## ✅ Behavior

- Performs a `terraform init -backend=false` to download providers without configuring state backend
- Checks if Terraform code is properly formatted using `terraform fmt -check`
- Validates configuration syntax using `terraform validate`
- Prints results to both console output and the GitHub Actions Summary
- Supports `soft-fail` for non-blocking failures during development workflows
- Outputs a `valid` result for downstream conditional steps

---

## 🚀 Usage

### Basic Usage

```yaml
jobs:
  tf-validate:
    runs-on: ubuntu-latest
    steps:
      - name: Run Terraform Validate Action
        id: tf-validate
        uses: subhamay-bhattacharyya-gha/tf-validate-action@main
        with:
          terraform-dir: tf
          soft-fail: "false"

      - name: Display Status
        run: |
          echo "Validation Passed: ${{ steps.tf-validate.outputs.valid }}"
```

### With Release Tag

```yaml
jobs:
  tf-validate:
    runs-on: ubuntu-latest
    steps:
      - name: Run Terraform Validate Action
        uses: subhamay-bhattacharyya-gha/tf-validate-action@main
        with:
          terraform-dir: tf
          release-tag: v1.0.0
          soft-fail: "true"
```

## License

MIT
