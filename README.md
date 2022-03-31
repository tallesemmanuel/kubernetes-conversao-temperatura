## Deployment projeto conversão de temperatura em kubernetes

### Para entender toda criação do build da imagem em docker. Veja esse link abaixo.

```bash
git clone https://github.com/tallesemmanuel/conversao-temperatura.git
```

## Requisitos - Ter instalado os seguintes serviços.

- Kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
- K3d - https://k3d.io/v5.4.1/
- Docker - https://docs.docker.com/engine/install/ubuntu/

## Como iniciar com esse projeto

Download do projeto.

```bash
git clone https://github.com/tallesemmanuel/kubernetes-conversao-temperatura.git
```

- Iniciar um cluster.

No meu caso, estou subindo um cluster com 3 agents e 3 servers, analise se para você da certo o total de nós.
Também neste comando, estou especificando a porta da aplicação "8080", mapeando localmente uma porta "30000" para o loadbalancer, caso tenha muitos pods e seja escalável.

```bash
k3d cluster create cluster-temperatura --agents 3 --servers 3 -p "8080:30000@loadbalancer"
```

- Para realizar o deployment da aplicação, se da necessário rodar apenas um comando.

```bash
kubectl apply -f deployment.yml
```

- Você pode acompanhar os serviços com o comando.
Nele você consegue ver todos os "pods", "services", "replicateSets", "deployments" e etc.

```bash
kubectl get all
```

Saída do comando.

```bash
NAME                                         READY   STATUS    RESTARTS   AGE
pod/conversao-temperatura-54bb868989-wqk86   1/1     Running   0          8m17s

NAME                            TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
service/conversao-temperatura   NodePort    10.43.42.227   <none>        80:30000/TCP   8m17s
service/kubernetes              ClusterIP   10.43.0.1      <none>        443/TCP        9m25s

NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/conversao-temperatura   1/1     1            1           8m17s

NAME                                               DESIRED   CURRENT   READY   AGE
replicaset.apps/conversao-temperatura-54bb868989   1         1         1       8m17s
```
