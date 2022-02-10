# kubernetes-operator

https://sdk.operatorframework.io/docs/building-operators/golang/tutorial/

cd to memcached-operator folder first.

- Generate code for resource type
  
        make generate

- Generating CRD manifests
    
        make manifests

- Build operator
  
        make docker-build docker-push

- Run operator

        make deploy

- Create CR
  
        kubectl apply -f config/samples/cache_v1alpha1_memcached.yaml

- Results:
    
        $ kubectl get deployment -n memcached-operator-system
        NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
        memcached-operator-controller-manager   1/1     1            1           29m


        $ kubectl get pods
        NAME                                READY   STATUS    RESTARTS   AGE
        memcached-sample-75bf65b88f-jwq5s   1/1     Running   0          24m
        memcached-sample-75bf65b88f-rlhdz   1/1     Running   0          28m
        memcached-sample-75bf65b88f-w7kzt   1/1     Running   0          28m

- Clean
  
        $ kubectl delete -f config/samples/cache_v1alpha1_memcached.yaml

        memcached.cache.weiwongfaye "memcached-sample" deleted

        $ make undeploy

        ./kubernetes-operator/memcached-operator/bin/kustomize build config/default | kubectl delete --ignore-not-found=false -f -
        namespace "memcached-operator-system" deleted
        customresourcedefinition.apiextensions.k8s.io "memcacheds.cache.weiwongfaye" deleted
        serviceaccount "memcached-operator-controller-manager" deleted
        role.rbac.authorization.k8s.io "memcached-operator-leader-election-role" deleted
        clusterrole.rbac.authorization.k8s.io "memcached-operator-manager-role" deleted
        clusterrole.rbac.authorization.k8s.io "memcached-operator-metrics-reader" deleted
        clusterrole.rbac.authorization.k8s.io "memcached-operator-proxy-role" deleted
        rolebinding.rbac.authorization.k8s.io "memcached-operator-leader-election-rolebinding" deleted
        clusterrolebinding.rbac.authorization.k8s.io "memcached-operator-manager-rolebinding" deleted
        clusterrolebinding.rbac.authorization.k8s.io "memcached-operator-proxy-rolebinding" deleted
        configmap "memcached-operator-manager-config" deleted
        service "memcached-operator-controller-manager-metrics-service" deleted
        deployment.apps "memcached-operator-controller-manager" deleted
