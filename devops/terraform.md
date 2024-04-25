* Change to file in json format to inspect even sensitive values
```
terraform plan -out tfplan
terraform show -json tfplan > tfplan.json
```