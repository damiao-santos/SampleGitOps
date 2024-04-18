Instalar Sealed Secrets

Baixamos a CLI:

wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.26.2/kubeseal-0.26.2-linux-amd64.tar.gz

tar -xvf kubeseal-0.20.5-linux-amd64.tar.gz
sudo mv kubeseal /usr/local/bin
sudo chmod +x /usr/local/bin/kubeseal

Após baixamos o yaml do controlle:

wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.26.2/controller.yaml

kubectl apply -f controller.yaml

para criptografar de forma online basta executar o comando no padrão abaixo

kubeseal --format=yaml < secret.yaml > sealedsecret.yaml

Para criptografar de forma offline o cert deve ser baixado

kubeseal --fetch-cert > publickey.pem

e após isso do mesmo diretorio que esta o .pem

kubeseal --format=yaml --cert=publickey.pem < secret.yaml > sealedsecret.yaml

O sealed secret não permite descriptografar o arquivo, para visualizar a secret podemos acessar diretamente o pod e verificar as variaveis de ambiente:

exemplo:
kubectl exec -it busybox-deployment-576bf8d585-dz268 sh

/ # echo $APIKEY
api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxx

