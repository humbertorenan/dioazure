az login
az group create --name MeuGrupo --location brazilsouth
az vm create --name MinhaVM --resource-group MeuGrupo --image UbuntuLTS

az vm create \
  --name MinhaVM \
  --resource-group MeuGrupo \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys

az vm list --output table
az vm start --name MinhaVM --resource-group MeuGrupo
az vm stop --name MinhaVM --resource-group MeuGrupo
az vm delete --name MinhaVM --resource-group MeuGrupo --yes


az network nsg create \
  --resource-group MeuGrupo \
  --name MeuNSG

az network nsg rule create \
  --resource-group MeuGrupo \
  --nsg-name MeuNSG \
  --name PermitirSSH \
  --protocol tcp \
  --priority 1000 \
  --destination-port-range 22 \
  --access allow \
  --direction inbound

