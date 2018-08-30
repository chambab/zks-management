# zks-management
Apply Only ICP CE/CNE Environment & GPA(Grafana, Prometheus, Alertmanager) Stack

Test with ICP Verision  <= 2.1.0.3
## zks-monitoring
* Prometheus Alert Rule
```
$ kubenetes apply -f monitoring/prometheus/prometheus-rules.yaml
```
* Alertmanager Notification Config
```
$ kubenetes apply -f monitoring/alertmanager/alertmanager-config-cm.yaml

$ kubenetes apply -f monitoring/alertmanager/alertmanager-template-cm.yaml
$ kubectl edit deployment monitoring-prometheus-alertmanager

...
volumes:
      - configMap:
          defaultMode: 420
          name: monitoring-prometheus-alertmanager
        name: config-volume
      - configMap:                                    //Template ConfigMap Add
          defaultMode: 420
          name: alertmanager-templates
        name: alertmanager-templates-volume

image: ibmcom/alertmanager:v0.13.0
        imagePullPolicy: IfNotPresent
        name: alertmanager
        ...
        ...
        volumeMounts:
        - mountPath: /etc/config
          name: config-volume
        - mountPath: /var/lib/alertmanager/data
          name: storage-volume
        - mountPath: /etc/alertmanager-templates	//Template ConfigMap Add
          name: alertmanager-templates-volume
```
* Grafana Dashboard

## zks-logging
## zks-hpa
* Custom-Metric-Adaptor(Prometheus)
