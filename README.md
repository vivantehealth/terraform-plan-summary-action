# terraform-plan-summary-action

Suggested use:

```yaml
jobs:
  run:
    name: Run
    runs-on: ubuntu-latest
    steps:
      - name: Terraform plan
        run: |
          terraform plan -out=tf.planfile
      - name: Write JSON plan file
        id: json-plan
        # from https://github.com/hashicorp/setup-terraform/issues/20
        # terraform_wrapper adds GH-related text to stdout (debug, outputs, etc.)
        # use the non-wrapped binary instead
        run: |
          terraform-bin show -json planfile > tf-plan.json
          echo "::set-output name=JSON_PLAN_PATH::$(realpath tf-plan.json)"
      - name: Summarize plan
        id: plan-summary
        uses: vivantehealth/terraform-plan-summary-action@v0
        with:
          json-tf-plan: "${{ steps.json-plan.outputs.JSON_PLAN_PATH }}"
          environment: "dev"
```
