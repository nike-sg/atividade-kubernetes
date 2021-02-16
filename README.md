# To deploy
Logar na azure
> az login

Criar um resource-group 
> az group create --name rg-aulainfra --location brazilsouth

Criar um ssh (somente se não já existir)
> ssh-keygen -f ssh-key-atividade-aks

Criar um cluster kubernetes
> az aks create --resource-group rg-aulainfra --name atividade-aks --node-count 1 --node-vm-size Standard_D2s_v3 --ssh-key-value ssh-key-atividade-aks.pub

Vincular 
> az aks get-credentials --name atividade-aks --resource-group rg-aulainfra --output table

Aplicar pod mysql
> kubectl apply -f mysql

Criar o nginx
> kubectl apply -f nginx


# Comandos

Deletar RG
> az group delete --name rg-aulainfra --yes --no-wait

Deletar pods
> kubectl delete -f mysql
> kubectl delete -f nginx

Entrar no sh do nginx
> kubectl exec -it pod/nginx-pod-declarativo -- sh