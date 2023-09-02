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

## OTHER STEPS
#### CREATE SECRET FOR NEXUS
```
k create secret docker-registry dockercred -n peakyblinders \
    --docker-server=http://grace-registry.nurigundogan.net \
    --docker-username=admin \
    --docker-password=<password>
```
#### LOGIN TEST FOR NEXUS
```
docker login -u admin -p <password> grace-registry.nurigundogan.net
```

## RELATED URLS
```
http://thomas.nurigundogan.net           / Jenkins
http://grace.nurigundogan.net            / Nexus Admin UI
https://grace-registry.nurigundogan.net  / Nexus Registry
http://shelby.nurigundogan.net           / EFK Stack
http://arthur.nurigundogan.net           / App Endpoint

```

