<https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/>

The problem is that, during scale down by auto scaling, we need to make sure that the node should wait until all the pods are finished, instead of just evict them to another node.

(Especially in airflow worker pods, we must wait until all the pods were finished.)