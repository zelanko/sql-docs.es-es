---
title: Use curl para cargar datos en HDFS | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: Use curl para cargar datos en HDFS en clústeres de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 56bee3241427b9de9768e7bdd9e49646b51521d1
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860151"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>Use curl para cargar datos en HDFS en clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo usar **curl** para cargar datos en HDFS en clústeres de macrodatos de 2019 de SQL Server (versión preliminar).

## <a name="obtain-the-service-external-ip"></a>Obtener la dirección IP externa de servicio

WebHDFS se inicia cuando se completa la implementación, y su acceso se pasa a través de Knox. El punto de conexión de Knox se expone a través de un servicio de Kubernetes denominado **endpoint security**.  Para crear la dirección URL de WebHDFS necesaria para cargar/descargar archivos, necesitará la **endpoint security** dirección IP externa y el nombre del clúster del servicio. Puede obtener el **endpoint security** dirección IP externa del servicio, ejecute el comando siguiente:

```bash
kubectl get service endpoint-security -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> El `<cluster name>` aquí es el nombre del clúster que proporcionó cuando ejecutó `mssqlctl cluster create --name <cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir la dirección URL para tener acceso a WebHDFS

Ahora, puede construir la dirección URL para tener acceso a la WebHDFS como sigue:

`https://<endpoint-security service external IP address>:30443/gateway/default/webhdfs/v1/`

Por ejemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Un archivo de lista

Archivo de lista en **hdfs: / / / airlinedata**, use el siguiente comando curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Coloque un archivo local en HDFS

Para colocar un nuevo archivo **test.csv** desde airlinedata Active directory local, use el siguiente comando curl (el **Content-Type** el parámetro es obligatorio):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Cree un directorio

Para crear un directorio **probar** en `hdfs:///`, use el siguiente comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<endpoint-security IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el clúster de macrodatos de SQL Server, vea [¿qué es el clúster de macrodatos de SQL Server?](big-data-cluster-overview.md).
