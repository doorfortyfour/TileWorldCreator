## Merging & Clusters :id=merging  

A build layer takes care of partitioning a map into smaller clusters. Each cluster contains multiple tile objects. When merging is enabled, all tiles inside of a cluster are being merged together.  When changing a map - by painting tiles for example - the build tiles layer checks for all changed tiles in each cluster and updates only the changed cluster.  
> When creating large maps it is highly recommended to enable merging. 
