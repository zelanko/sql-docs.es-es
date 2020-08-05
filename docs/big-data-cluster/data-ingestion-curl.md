---
title: Empleo de curl para cargar datos en HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use curl para cargar datos en HDFS en un clúster de macrodatos de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e4d030b54944b8fe25d930f7f0b4fc540f7aff67
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784333"
---
# <a name="use-curl-to-load-data-into-hdfs-on-big-data-clusters-2019"></a>Empleo de curl para cargar datos en HDFS en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

En este artículo se explica cómo usar **curl** para cargar datos en HDFS en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

## <a name="prerequisites"></a><a id="prereqs"></a> Requisitos previos

- [Cargar datos de ejemplo en un clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>Obtener la dirección IP externa del servicio

WebHDFS se inicia cuando se completa la implementación; su acceso se realiza a través de Knox. El punto de conexión de Knox se expone a través de un servicio de Kubernetes denominado **gateway-svc-external**.  Para crear la dirección URL de WebHDFS necesaria para cargar o descargar archivos, necesita la dirección IP externa del servicio **gateway-svc-external** y el nombre del clúster de macrodatos. Para obtener la dirección IP externa del servicio **gateway-svc-external**, ejecute el siguiente comando:

```terminal
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<big data cluster name>` es el nombre del clúster que ha especificado en el archivo de configuración de implementación. El nombre predeterminado es `mssql-cluster`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construcción de la dirección URL para acceder a WebHDFS

Ahora, puede construir la dirección URL para acceder a WebHDFS como se indica a continuación:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

Por ejemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Enumeración de un archivo

Para mostrar el archivo de **hdfs:///product_review_data**, use el siguiente comando de curl:

```terminal
curl -i -k -u root:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

En el caso de los puntos de conexión que no usan la raíz, use el siguiente comando de curl:

```terminal
curl -i -k -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocación de un archivo local en HDFS

Para colocar un nuevo archivo **test. csv** desde el directorio local en el directorio product_review_data, use el siguiente comando de curl (se requiere el parámetro **Content-Type**):

```terminal
curl -i -L -k -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]

En el caso de los puntos de conexión que no usan la raíz, use el siguiente comando de curl:

```terminal
curl -i -L -k -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Creación de un directorio

Para crear un directorio **test** en `hdfs:///`, use el siguiente comando:

```terminal
curl -i -L -k -u root:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

[!INCLUDE [big-data-cluster-root-user](../includes/big-data-cluster-root-user.md)]
En el caso de los puntos de conexión que no usan la raíz, use el siguiente comando de curl:

```terminal
curl -i -L -k -u <AZDATA_USERNAME>:<AZDATA_PASSWORD> -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server, vea [¿Qué son los clústeres de macrodatos de SQL Server?](big-data-cluster-overview.md)
