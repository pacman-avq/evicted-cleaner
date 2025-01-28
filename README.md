# evicted-cleaner

This setup will create a CronJob named evicted-cleaner in the k8s-admin-jobs namespace that runs every 30 minutes. The job uses the sa_cleaner service account, which has the necessary permissions to delete evicted pods across all namespaces. The command inside the container lists all evicted pods and deletes them using kubectl

* How to install:
```bash
kubectl apply -f service-account.yaml
```
and after apply the cronjob manifest
```bash
kubectl apply -f cronjob.yaml
```
The result is (I've set the job evry 2 minutes in this example):

```bash
NAME              SCHEDULE      TIMEZONE   SUSPEND   ACTIVE   LAST SCHEDULE   AGE
evicted-cleaner   */2 * * * *   <none>     False     0        27s             18m
NAME                       STATUS     COMPLETIONS   DURATION   AGE
evicted-cleaner-28968422   Complete   1/1           4s         4m27s
evicted-cleaner-28968424   Complete   1/1           4s         2m27s
evicted-cleaner-28968426   Complete   1/1           3s         27s
NAME                             READY   STATUS      RESTARTS   AGE
evicted-cleaner-28968422-v8xjc   0/1     Completed   0          4m27s
evicted-cleaner-28968424-dcltn   0/1     Completed   0          2m27s
evicted-cleaner-28968426-6dthj   0/1     Completed   0          27s
```


