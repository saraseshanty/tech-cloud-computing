Laporan Praktikum Teknologi Cloud Computing - Minggu 13
Saras Eshanty
225611025
Learn Kubertentes Basics
Materi
Di lab ini, kita akan bermain-main dengan container orchestration pada Docker. Kita akan menerapkan aplikasi sederhana ke satu host dan mempelajari cara kerjanya. Kemudian, kita mengonfigurasi Docker Swarm, dan belajar menerapkan aplikasi sederhana yang sama di beberapa host. Kemudian kita akan melihat cara menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.
Tujuan
Mahasiswa mampu menerapkan dan memahami aplikasi sederhana ke satu host dan mempelajari cara kerjanya.
Mahasiswa mampu mengkonfigurasikan Docker Swarm dan menerapkan beberapa aplikasi yang sama dalam beberapa host.
Mahasiswa mampu menskalakan aplikasi dan memindahkan beban kerja ke berbagai host dengan mudah.
Pembahasan
Langkah - langkah Praktikum

MODUL 1
$ minikube version
1.jpg

$ minikube start
2.jpg

$ kubectl version
3.jpg

$ kubectl cluster-info
4.jpg

$ kubectl get nodes
5.jpg

MODUL 2
$ kubectl version $ kubectl get nodes

1.jpg

$ kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1

3.jpg

$ kubectl get deployments

4.jpg

$ echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy $ curl http://localhost:8001/version

5.jpg

$ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME $ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/

6.jpg

MODUL 3
$ kubectl get pods $ kubectl describe pods

1.jpg 2.jpg

$ echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n"; kubectl proxy $ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME

3.jpg

$ curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

4.jpg

$ kubectl logs $POD_NAME

5.jpg

$ kubectl exec -ti $POD_NAME -- bash $ cat server.js $ curl localhost:8080

6.jpg 7.jpg

$ exit

MODUL 4
$ kubectl get pods $ kubectl get services $ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080

1.jpg

$ kubectl get services $ kubectl describe services/kubernetes-bootcamp

2.jpg

$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT $ curl $(minikube ip):$NODE_PORT

3.jpg

$ kubectl describe deployment

4.jpg

$ kubectl get pods -l app=kubernetes-bootcamp $ kubectl get services -l app=kubernetes-bootcamp $ export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}') echo Name of the Pod: $POD_NAME $ kubectl label pods $POD_NAME version=v1

5.jpg

$ kubectl describe pods $POD_NAME

6.jpg

$ kubectl get pods -l version=v1

7.jpg

8.jpg

$ kubectl delete service -l app=kubernetes-bootcamp $ kubectl get services $ curl $(minikube ip):$NODE_PORT

9.jpg

$ kubectl exec -ti $POD_NAME -- curl localhost:8080

10.jpg

MODUL 5
$ kubectl get deployments

1.jpg

$ kubectl get deployments $ kubectl scale deployments/kubernetes-bootcamp --replicas=4 $ kubectl get deployments $ kubectl get pods -o wide $ kubectl describe deployments/kubernetes-bootcamp $ kubectl describe services/kubernetes-bootcamp

2.jpg

$ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT

3.jpg

$ curl $(minikube ip):$NODE_PORT $ kubectl scale deployments/kubernetes-bootcamp --replicas=2 $ kubectl get deployments $ kubectl get pods -o wide

3.jpg

MODUL 6
$ kubectl get deployments $ kubectl get pods $ kubectl describe pods $ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=jocatalin/kubernetes-bootcamp:v2 $ kubectl get pods

1.jpg

$ kubectl describe services/kubernetes-bootcamp $ export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}') echo NODE_PORT=$NODE_PORT $ curl $(minikube ip):$NODE_PORT

2.jpg

$ kubectl rollout status deployments/kubernetes-bootcamp $ kubectl describe pods

3.jpg

$ kubectl set image deployments/kubernetes-bootcamp kubernetes-bootcamp=gcr.io/google-samples/kubernetes-bootcamp:v10 $ kubectl get deployments $ kubectl get pods

4.jpg

$ kubectl describe pods $ kubectl rollout undo deployments/kubernetes-bootcamp

5.jpg

$ kubectl get pods $ kubectl describe pods

6.jpg

7.jpg

Software yang Diperlukan
Linux, Kubernetes


