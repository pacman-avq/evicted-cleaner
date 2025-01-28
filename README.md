# evicted-cleaner

This setup will create a CronJob named evicted-cleaner in the k8s-admin-jobs namespace that runs every 30 minutes. The job uses the sa_cleaner service account, which has the necessary permissions to delete evicted pods across all namespaces. The command inside the container lists all evicted pods and deletes them using kubectl
