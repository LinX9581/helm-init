https://ithelp.ithome.com.tw/articles/10238998
https://ithelp.ithome.com.tw/articles/10239692


## 新增
kubectl create ns helm-init
helm create helm-init
cd helm-init/

* 根據 Chart.yaml 去生 k8s yaml
c

# 查詢
* 查看目前 helm的 release2 以及pod
helm list -n helm-init
helm list --all-namespaces
kubectl get all -n helm-init

* 查看生出來的實際 yaml 長怎樣
helm -n helm-init get manifest helm-release2

* 檢查
helm lint ./

## Editor
* 會去覆蓋 value.yaml 但實際上檔案不會被改
helm -n helm-init upgrade helm-release2 --set service.type=NodePort ./
helm upgrade -n helm-init helm-release2 ./ -f values.yaml

* 可以查看異動了甚麼
helm -n helm-init get values helm-release2


# 版本控管
* 看歷史紀錄
helm history helm-release2 -n helm-init
helm rollback helm-release2 -n helm-init 5

## 移除
kubectl delete all --all -n helm-init
helm delete -n helm-init helm-release2

## 確認結果
kdsn 查看node ip
ip:service port 即可看到 nginx



kubectl get all -n helm-init