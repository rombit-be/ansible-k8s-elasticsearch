# Kubernetes Elasticsearch

A role that deploys a statuful set containing elasticsearch on a kubernetes cluster running on AWS.


Requirements
------------

This role depends on you having a kubernetes cluster. It uses a [headless service](https://kubernetes.io/docs/concepts/services-networking/service/) for discovery of elasticsearch nodes.


Role Variables
--------------

The following variables should be set before using this role:     

* k8s_cluster: The name of the cluster you want to deploy to
* k8s_namespace: The namespace to deploy elasticsearch in. Default is `elasticsearch`
* elasticsearch_image: Find a list of elasticsearch docker images [here](https://www.docker.elastic.co/#)     
* elasticsearch_image_version: defaults to `5.2.1`

For more variables you can override, look into [defaults/main.yml](defaults/main.yml)

Upgrades
--------

For rolling upgrade the upgrade strategy is set to on delete. Follow the instruction on elasticsearch site to make the rolling upgrade fast:

https://www.elastic.co/guide/en/elasticsearch/reference/current/rolling-upgrades.html

Don't forget to update the currently elected master last. As a master reelection has a bit of downtime. When deleting the master first a new node gets elected that will later be shut down again. Making this downtime happen twice.
