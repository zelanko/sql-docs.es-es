---
title: Empleo de curl para cargar datos en HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use curl para cargar datos en HDFS en clústeres de macrodatos de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aae991c6dfdade4145f1e5578273e3b6aeb83299
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958632"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>Empleo de curl para cargar datos en HDFS en clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo usar **curl** para cargar datos en HDFS en clústeres de macrodatos de SQL Server 2019 (versión preliminar).

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
