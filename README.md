I am creating the user with the daniyal name and below are the steps to create the user
openssl genrsa -out daniyal.key 2048 (create a private key)
openssl req -new -key daniyal.key -out daniyal.csr -subj "/CN=daniyal" (create a csr)
openssl x509 -req -in daniyal.csr \
  -CA ~/.minikube/ca.crt \
  -CAkey ~/.minikube/ca.key \
  -CAcreateserial \
  -out daniyal.crt -days 365 (creaet a certs with validity of 1 year)

 Now you have created the keys, csr and certs so now you have to push these in config file

 kubectl config set-credentials daniyal \
  --client-certificate=daniyal.crt \
  --client-key=daniyal.key

kubectl config set-context daniyal-context \
  --cluster=minikube \
  --user=daniyal

  kubectl config use-context daniyal-context (using this command you can switch context)

  After you have created the user and set the context in ~/.kube/config file so now you will give permision I am giving to view the pods in all ns so I am using cluster role
