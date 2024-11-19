
## Accessing variable from one job in another job within a GitHub Actions workflow

Variables set in `GITHUB_ENV` apply only to the current job. To carry the value over to another job, you need a job output. Mind that you need to define the job output based on the step output.

Example : https://github.com/adam-cowley/aura-cli-integration-tests/blob/main/.github/workflows/aura.yml

    jobs:
      check-pr:
        runs-on: ubuntu-latest
        outputs:
          pr-number: ${{ steps.check-prs.outputs.PR_NUMBER }}
        steps:
          - name: Check PRs
            id: check-prs
            run: |
              # ...
              echo "PR_NUMBER=$pr_number" >> $GITHUB_OUTPUT
    
      publish:
        needs: [check-pr]
        runs-on: ubuntu-latest
        env:
          PR_NUMBER: ${{ needs.check-pr.outputs.pr-number }}
