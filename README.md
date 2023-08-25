## CREATE AKS WITH TERRAFORM
```
cd setups/aks
az login
az account set --subscription <subs-id>
az ad sp create-for-rbac -n <name> --role Contributor --scopes /subscriptions/<subs-id>

terraform init
terraform plan
terraform apply
terraform output -raw kube_config > aks_kubeconfig
export KUBECONFIG=./aks_kubeconfig
k get nodes
```
## DEPLOY NEXUS & JENKINS
```
cd setups/jenkins
ansible-playbook -i inventory.ini jenkins.yml
```
```
cd setups/nexus
ansible-playbook -i inventory.ini nexus.yml
```

## BONUS! DEPLOY EFK
```
cd setups/efk
k apply -f .
```

## RELATED URLS
```
http://thomas.nurigundogan.net           / Jenkins
http://grace.nurigundogan.net            / Nexus Admin UI
https://grace-registry.nurigundogan.net  / Nexus Registry
http://shelby.nurigundogan.net           / EFK Stack
http://arthur.nurigundogan.net           / App Endpoint

```

