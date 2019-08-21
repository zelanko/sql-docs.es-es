---
title: Empleo de curl para cargar datos en HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use rizo para cargar datos en HDFS en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 729c3af97f98bafced482f7ead8ce85f93b55af3
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652217"
---
# <a name="use-curl-to-load-data-into-hdfs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Usar rizo para cargar datos en HDFS en[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo usar **rizo** para cargar datos en HDFS [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] en (versión preliminar).

## <a name="obtain-the-service-external-ip"></a>Obtener la dirección IP externa del servicio

WebHDFS se inicia cuando se completa la implementación; su acceso se realiza a través de Knox. El punto de conexión de Knox se expone a través de un servicio de Kubernetes denominado **gateway-svc-external**.  Para crear la dirección URL de WebHDFS necesaria para cargar o descargar archivos, necesita la dirección IP externa del servicio **gateway-svc-external** y el nombre del clúster de macrodatos. Para obtener la dirección IP externa del servicio **gateway-svc-external**, ejecute el siguiente comando:

```bash
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

Para mostrar el archivo de **hdfs:///airlinedata**, use el siguiente comando de curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Colocación de un archivo local en HDFS

Para colocar un nuevo archivo **test. csv** desde el directorio local en el directorio airlinedata, use el siguiente comando de curl (se requiere el parámetro **Content-Type**):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Creación de un directorio

Para crear un directorio **test** en `hdfs:///`, use el siguiente comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server, vea [¿Qué son los clústeres de macrodatos de SQL Server?](big-data-cluster-overview.md)
