# Домашнее задание 3

1. Почему команда `sh -c ps aux | grep my_web_server_process` не самый лучший вариант указания liveliness probe?

Могут быть варианты когда команда `grep` найдет в команде `ps aux` другие процессы, не связанные с основной работой приложения, и тогда ошибочно посчитает что приложение до сих пор успешно функционирует. 

Однако данная проверка сможет защитить от ошибок на уровне OS, когда сама команда становится недоступной.

# Домашнее задание 2

1. Почему поды не обновились при обновлении манифеста ReplicaSet?

Исходя из [документации](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/), ReplicaSet отвечает только за контроль необходимого кол-ва подов, но не за их обновление. Напротив, Deployment предоставляет дополнительные возможности также и обновления подов.

Как запустить задание с 2 звездами (име кластер развернутый при помщи kind):

- Создать namespace monitoring: `kubectl create ns monitoring`

- Применить `node-exporter-deamonset.yaml`: `kubectl apply -f node-exporter-deamonset.yaml` 

- Проверить что поды создались на всех нодах, включая master-nodes/control-planes: `kubectl get ds -n monitoring`


# Домашнее задание 1

1. Почему все pod в namespace kube-system восстановились после удаления?

- Почему восстанавливается под `coredns`?

Под `coredns` контролируется объектом `deployment`, который всегда проверяет необходимое кол-во реплик и при необходимости воссоздает их.

- Почему восстанавливаются остальные под из `kube-system`?

Остальные поды принадлежат к категории Static Pods, которые управляются напрямую kubelet и [воссоздаются им при необходимости](https://kubernetes.io/docs/tasks/configure-pod-container/static-pod/). Для справки, данные поды могут быть удалены если их конфигурации также будут удалены из директории `/etc/kubernetes/manifests`.

2. Добавлен [web-pod.yml](/kubernetes-intro/web-pod.yaml) контейнер.

3. Добавлены файлы [frontend-pod.yaml](/kubernetes-intro/frontend-pod.yaml) и [frontend-pod-healthy.yaml](/kubernetes-intro/frontend-pod-healthy.yaml).

Проблема автосгенерированного `yaml` файла заключалась в отсутствии переменных окружения.

---