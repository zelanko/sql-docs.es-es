---
title: Montaje de S3 para los niveles de HDFS
titleSuffix: SQL Server big data clusters
description: Este artículo explica cómo configurar HDFS niveles para montar un sistema de archivos externo de S3 en HDFS en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1f126620c4da759a4c56abad05bf2e989d7d1bc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782069"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Cómo S3 de montaje para los niveles en un clúster de macrodatos HDFS

Las secciones siguientes proporcionan un ejemplo de cómo configurar la organización en niveles con un origen de datos de almacenamiento de S3 HDFS.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos implementada](deployment-guidance.md)
- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**
- Crear y cargar datos en un cubo de S3 
  - Cargar CSV o archivos en el cubo de S3 de Parquet. Se trata de los datos HDFS externos que se montará en HDFS en el clúster de macrodatos.

## <a name="access-keys"></a>Claves de acceso

1. Abra un símbolo en un equipo cliente que puede tener acceso al clúster de macrodatos.

1. Cree un archivo local denominado **filename.creds** que contiene sus credenciales de cuenta S3 con el formato siguiente:

   ```text
    fs.s3a.access.key=<Access Key ID of the key>
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Para obtener más información sobre cómo crear claves de acceso de S3, consulte [claves de acceso de S3](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a> Montar el almacenamiento HDFS remoto

Ahora que ha preparado un archivo de credenciales con las teclas de acceso, puede iniciar el montaje. Los pasos siguientes montar el almacenamiento remoto de HDFS en S3 en el almacenamiento HDFS local de su clúster de macrodatos.

1. Use **kubectl** para buscar la dirección IP para el punto de conexión **controlador-svc-external** servicio en el clúster de macrodatos. Busque el **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Inicie sesión con **mssqlctl** utilizando la dirección IP externa del punto de conexión de controlador con el nombre de usuario del clúster y la contraseña:

   ```bash
   mssqlctl login -e https://<IP-of-controller-svc-external>:30080/
   ```

1. Montar el almacenamiento HDFS remoto en Azure mediante **mssqlctl montaje del bloque de almacenamiento de clúster crear**. Reemplace los valores de marcador de posición antes de ejecutar el comando siguiente:

   ```bash
   mssqlctl cluster storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name> --credential-file <path-to-s3-credentials>/file.creds
   ```

   > [!NOTE]
   > El montaje crear comando es asincrónica. En este momento, no hay ningún mensaje que indica si el montaje se realizó correctamente. Consulte la [estado](#status) sección para comprobar el estado de sus montajes.

Si ha montado correctamente, podrá consultar los datos HDFS y ejecutar trabajos de Spark en él. Aparecerá en el HDFS del clúster de macrodatos en la ubicación especificada por `--mount-path`.

## <a id="status"></a> Obtener el estado de montajes

Para mostrar el estado de todos los montajes en el clúster de macrodatos, utilice el siguiente comando:

```bash
mssqlctl cluster storage-pool mount status
```

Para mostrar el estado de un montaje en una ruta específica en HDFS, use el siguiente comando:

```bash
mssqlctl cluster storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminar el montaje

Para eliminar el montaje, use el **mssqlctl clúster grupo de almacenamiento montaje delete** comando y especifique la ruta de acceso de montaje en HDFS:

```bash
mssqlctl cluster storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
