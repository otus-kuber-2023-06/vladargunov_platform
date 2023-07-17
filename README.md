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