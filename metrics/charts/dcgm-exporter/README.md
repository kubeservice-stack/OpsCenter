
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
>>>>>>> 7664fe5 (add dcgm-exporter)
=======
>>>>>>> 952776d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
>>>>>>> f6e4bebac24d7bcba8dc64c2859a923e46635dcb
1， 配置使用nvidia runtime
=======

>>>>>>> c3ca160 (add dcgm-exporter)
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
1， 配置使用nvidia runtime
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======

>>>>>>> fdfe4e2 (add dcgm-exporter)
=======
1， 配置使用nvidia runtime
>>>>>>> b4ae0b9 (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
>>>>>>> 7664fe5 (add dcgm-exporter)
=======
=======
1， 配置使用nvidia runtime
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
>>>>>>> 952776d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
=======
1， 配置使用nvidia runtime
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
>>>>>>> f6e4bebac24d7bcba8dc64c2859a923e46635dcb
#use docker
/etc/docker/daemon.json


{
    "default-runtime": "nvidia",
    "runtimes": {
        "nvidia": {
            "path": "/usr/bin/nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}


#use  containerd
/etc/containerd/config.toml

########
version = 2
[plugins]
  [plugins."io.containerd.grpc.v1.cri"]
    [plugins."io.containerd.grpc.v1.cri".containerd]
      default_runtime_name = "nvidia"

      [plugins."io.containerd.grpc.v1.cri".containerd.runtimes]
        [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia]
          privileged_without_host_devices = false
          runtime_engine = ""
          runtime_root = ""
          runtime_type = "io.containerd.runc.v2"
          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.nvidia.options]
            BinaryName = "/usr/bin/nvidia-container-runtime"
#######

          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
            BinaryName = "/usr/bin/nvidia-container-runtime"
            CriuImagePath = ""
            CriuPath = ""
            CriuWorkPath = ""
            IoGid = 0
            IoUid = 0
            NoNewKeyring = false
            NoPivotRoot = false
            Root = ""
            ShimCgroup = ""
            SystemdCgroup = false

<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
>>>>>>> 7664fe5 (add dcgm-exporter)
=======
>>>>>>> 952776d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
>>>>>>> f6e4bebac24d7bcba8dc64c2859a923e46635dcb
2, 部署
=======

>>>>>>> c3ca160 (add dcgm-exporter)
<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
2, 部署
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======

>>>>>>> fdfe4e2 (add dcgm-exporter)
=======
2, 部署
>>>>>>> b4ae0b9 (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
>>>>>>> 7664fe5 (add dcgm-exporter)
=======
=======
2, 部署
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
>>>>>>> 952776d (Signed-off-by: yogiseven <seventhyou@126.com>)
=======
=======
2, 部署
>>>>>>> 2ff402d (Signed-off-by: yogiseven <seventhyou@126.com>)
>>>>>>> f6e4bebac24d7bcba8dc64c2859a923e46635dcb
cd  dcgm-exporter/deployment

kubectl create ns monitoing

helm template dcgm-exporter . --namespace monitoring > dcgm-exporter.yaml

kubectl apply -f  dcgm-exporter.yaml




