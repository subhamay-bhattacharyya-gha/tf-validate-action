# GitHub Composite Action for Terraform Validation and Formatting

![Release](https://github.com/subhamay-bhattacharyya-gha/tf-validate-action/actions/workflows/release.yaml/badge.svg)&nbsp;![Commit Activity](https://img.shields.io/github/commit-activity/t/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Last Commit](https://img.shields.io/github/last-commit/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Release Date](https://img.shields.io/github/release-date/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Repo Size](https://img.shields.io/github/repo-size/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![File Count](https://img.shields.io/github/directory-file-count/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Issues](https://img.shields.io/github/issues/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Top Language](https://img.shields.io/github/languages/top/subhamay-bhattacharyya-gha/tf-validate-action)&nbsp;![Custom Endpoint](https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/bsubhamay/bc727a7bfdc54056933718e073c39753/raw/tf-validate-action.json?)

Validate and format Terraform configuration in your CI pipeline using this GitHub Composite Action. This action ensures that your Terraform code is properly initialized, formatted, and structurally valid. It supports CI-friendly state keying, custom release tag checkouts, and soft failure for flexibility in development workflows.

---

## 📘 Description

This composite GitHub Action performs the following tasks for Terraform code quality:
- Checks out the repository at a specific release tag or current branch
- Initializes Terraform with an S3 backend
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
| `ci-pipeline`    | Set to `'true'` to use commit SHA in the backend key (CI/CD use case)       | No       | `false`   |
| `s3-bucket`      | Name of the S3 bucket for storing the Terraform state file                  | Yes      | —         |
| `s3-region`      | AWS region where the S3 backend bucket is located (e.g., `us-east-1`)       | Yes      | —         |
| `soft-fail`      | Set to `'true'` to continue the workflow even if formatting or validation fails | No   | `true`    |

---

## 📤 Outputs

| Name    | Description                                      |
|---------|--------------------------------------------------|
| `valid` | `true` if validation passed, `false` if it failed |

---

## ✅ Behavior

- Performs a `terraform init` using a dynamic or static S3 backend key
- Fails the job if Terraform code is not properly formatted or is invalid
- Prints results to both console output and the GitHub Actions Summary
- Supports `soft-fail` for non-blocking failures during development workflows
- Outputs a `valid` result for downstream conditional steps

---

## 🚀 Usage

```yaml
jobs:
  tf-validate:
    runs-on: ubuntu-latest
    steps:
      - name: Run Terraform Validate Action
        uses: subhamay-bhattacharyya-gha/tf-validate-action@main
        with:
          terraform-dir: tf
          s3-bucket: your-terraform-backend-bucket
          s3-region: us-east-1
          ci-pipeline: "true"
          soft-fail: "false"

      - name: Display Status
        run: |
          echo "Validation Passed: ${{ steps.tf-validate.outputs.valid }}"
```

## License

MIT
