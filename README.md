Внутри кластера выполняются команды:      
1. ```helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx```     
2. ```helm repo add prometheus-community https://prometheus-community.github.io/helm-charts```     
3. ```helm repo update```     

Сначала необходимо установить сущности kubernetes, для которых будет использоваться ingress-nginx-controller:     
4. ```helm install prometheus prometheus-community/kube-prometheus-stack --namespace=monitoring --create-namespace```   

Перед тем, как выполнить следущую команду, нужно убедиться, что образ приложения был загружен в репозиторий Dockerhub, на который будет ссылаться app-deploy.yaml:       
5. ```kubectl apply -f app-deploy.yaml```     

Лишь затем устанавливаем сам ingress-nginx-controller:    
6. ```helm install ingress-nginx ingress-nginx/ingress-nginx --namespace=nginx-ingress --create-namespace```     

После того, как мы убедились, что ingress-nginx-controller работает (получил EXTERNAL-IP), приступаем к ingress-ресурсам:    
7. ```kubectl apply -f app-ingress.yaml```       
8. ```kubectl apply -f grafana-ingress.yaml```       
