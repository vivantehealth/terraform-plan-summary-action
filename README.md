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
          terraform plan -out=tf.plan
          terraform show -json tf.plan > tf-plan.json
      - name: Summarize plan
        uses: vivantehealth/terraform-plan-summary-action@v0
        with:
          plan-file: ./tf-plan.json
```
