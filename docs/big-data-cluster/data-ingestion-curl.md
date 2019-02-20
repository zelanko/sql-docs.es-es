---
title: Use curl para cargar datos en HDFS en clústeres de SQL Server 2019 macrodatos | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c2172b9dda1f6f15b90e0f9a65f0abc179256918
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425770"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-big-data-clusters"></a>Use curl para cargar datos en HDFS en clústeres de macrodatos de SQL Server 2019

En este artículo se explica cómo usar **curl** para cargar datos en HDFS en clústeres de macrodatos de 2019 de SQL Server (versión preliminar).

## <a name="obtain-the-service-external-ip"></a>Obtener la dirección IP externa de servicio

WebHDFS se inicia cuando se completa la implementación, y su acceso se pasa a través de Knox. El punto de conexión de Knox se expone a través de un servicio de Kubernetes llamado (por ahora) **service-seguridad-lb**.  Para crear la dirección URL de WebHDFS que necesite utilizar CURL para cargar o descargar archivos que necesitará el **service-seguridad-lb** dirección IP externa y el nombre del clúster del servicio. Puede obtener la dirección IP de servicio de seguridad de servicio de equilibrador de carga externa, ejecute este comando:

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> El `<cluster name>` aquí es el nombre del clúster que especificó cuando ejecutó mssqlctl crear clúster `<cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Construir la dirección URL para tener acceso a WebHDFS

Ahora, puede construir la dirección URL para tener acceso a la WebHDFS como sigue:

`https://<service-security-lb service external IP address>:30443/gateway/default/webhdfs/v1/`

Por ejemplo:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Un archivo de lista

Archivo de lista en **hdfs: / / / airlinedata** use el siguiente comando curl:

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Coloque un archivo local en HDFS

Para colocar un nuevo archivo **test.csv** desde un directorio local al directorio airlinedata (**Content-Type** el parámetro es obligatorio) use el siguiente comando curl:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Cree un directorio

Para crear un directorio **probar** en `hdfs:///` use el siguiente comando:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el clúster de macrodatos de SQL Server, vea [¿qué es el clúster de macrodatos de SQL Server?](big-data-cluster-overview.md).
