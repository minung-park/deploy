# Kubernetes 설치

## macOS 에서 minikube 설치 (+kubeflow)

* https://kubernetes.io/ko/docs/tasks/tools/install-minikube/

$ minikube start --kubernetes-version v1.14.1 --cpus 4 --memory 8096 --disk-size=40g --insecure-registry handson-registry:15000 --driver=virtualbox


=============

대시보드

minikube dashboard

=============

kfctl 설치

wget https://github.com/kubeflow/kfctl/releases/download/v1.0-rc.4/kfctl_v1.0-rc.3-1-g24b60e8_darwin.tar.gz

tar xzvf kfctl_v1.0-rc.3-1-g24b60e8_darwin.tar.gz

# Add kfctl to PATH, to make the kfctl binary easier to use.
# Use only alphanumeric characters or - in the directory name.
$ export PATH=$PATH:"<path-to-kfctl>"
예) 
KFCTL="/Users/moosung/work/study/deploy/kubeflow/install"
export PATH=$PATH:${KFCTL}

==============

쿠베플로우 설치 

https://www.kubeflow.org/docs/started/k8s/kfctl-k8s-istio/

Kubeflow Deployment with kfctl_k8s_istio


export KF_NAME=study-kubeflow
export BASE_DIR=/Users/moosung/work/kubeflow_dir
export KF_DIR=${BASE_DIR}/${KF_NAME}
export CONFIG_URI=https://raw.githubusercontent.com/kubeflow/manifests/v0.7-branch/kfdef/kfctl_k8s_istio.0.7.0.yaml

mkdir -p ${KF_DIR}
cd ${KF_DIR}
kfctl build -V -f ${CONFIG_URI}

export CONFIG_FILE=${KF_DIR}/kfctl_k8s_istio.0.7.0.yaml
kfctl apply -V -f ${CONFIG_FILE}

=====================

https://istio.io/docs/tasks/traffic-management/ingress/ingress-control/

Determining the ingress IP and ports

80 포트에 연결된 포트 알아내기 (보통 31380)
kubectl get svc istio-ingressgateway -n istio-system
> 이런 부분이 있다 - 80:31380/TCP


대시보드 url 

(포트 바꿔서 외부와 연결)
kubectl port-forward -n istio-system svc/istio-ingressgateway [원하는 포트]:80 --address=0.0.0.0


