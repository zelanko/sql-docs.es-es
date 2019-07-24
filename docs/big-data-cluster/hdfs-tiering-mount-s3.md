---
title: Montaje de S3 para los niveles de HDFS
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo configurar la organización en niveles de HDFS para montar un sistema de archivos S3 externo en HDFS en un clúster de macrodatos SQL Server 2019 (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 28c80d6076f07c8a4f1605149f4b5c730c8349a1
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419339"
---
# <a name="how-to-mount-s3-for-hdfs-tiering-in-a-big-data-cluster"></a>Cómo montar S3 para la organización en niveles de HDFS en un clúster de Big Data

En las secciones siguientes se proporciona un ejemplo de cómo configurar la organización en niveles de HDFS con un origen de datos de almacenamiento S3.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de Big Data implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**
- Crear y cargar datos en un cubo S3 
  - Cargue los archivos CSV o parquet en el cubo S3. Estos son los datos de HDFS externos que se montarán en HDFS en el clúster de Big Data.

## <a name="access-keys"></a>Claves de acceso

### <a name="set-environment-variable-for-access-key-credentials"></a>Establecer la variable de entorno para las credenciales de clave de acceso

Abra un símbolo del sistema en un equipo cliente que pueda tener acceso al clúster de Big Data. Establezca una variable de entorno con el siguiente formato. Tenga en cuenta que las credenciales deben estar en una lista separada por comas. El comando "SET" se usa en Windows. Si usa Linux, use "Export" en su lugar.

   ```text
    set MOUNT_CREDENTIALS=fs.s3a.access.key=<Access Key ID of the key>,
    fs.s3a.secret.key=<Secret Access Key of the key>
   ```

   > [!TIP]
   > Para obtener más información sobre cómo crear teclas de acceso S3, consulte [S3 Access Keys](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html#access-keys-and-secret-access-keys).

## <a id="mount"></a>Montaje del almacenamiento de HDFS remoto

Ahora que ha preparado un archivo de credenciales con claves de acceso, puede iniciar el montaje. En los pasos siguientes se monta el almacenamiento de HDFS remoto en S3 en el almacenamiento de HDFS local del clúster de Big Data.

1. Use **kubectl** para buscar la dirección IP del **controlador de punto de conexión: servicio SVC-external** en el clúster de Big Data. Busque **external-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Inicie sesión con **azdata** mediante la dirección IP externa del punto de conexión del controlador con el nombre de usuario y la contraseña del clúster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
   
1. Establezca la variable de entorno MOUNT_CREDENTIALS según las instrucciones anteriores.

1. Monte el almacenamiento de HDFS remoto en Azure mediante el **almacenamiento de BDC de azdata creación del grupo de montaje**. Reemplace los valores de marcador de posición antes de ejecutar el siguiente comando:

   ```bash
   azdata bdc storage-pool mount create --remote-uri s3a://<S3 bucket name> --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > El comando mount Create es asincrónico. En este momento, no hay ningún mensaje que indique si el montaje tuvo éxito. Consulte la sección [Estado](#status) para comprobar el estado de los montajes.

Si se monta correctamente, debería poder consultar los datos de HDFS y ejecutar trabajos de Spark en él. Aparecerá en HDFS para el clúster de Big Data en la ubicación especificada por `--mount-path`.

## <a id="status"></a>Obtención del estado de montajes

Para mostrar el estado de todos los montajes en el clúster de Big Data, use el siguiente comando:

```bash
azdata bdc storage-pool mount status
```

Para mostrar el estado de un montaje en una ruta de acceso específica en HDFS, use el siguiente comando:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Actualización de un montaje

En el ejemplo siguiente se actualiza el montaje.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Eliminar el montaje

Para eliminar el montaje, use el comando **azdata BDC Storage-Pool Mount Delete** y especifique la ruta de acceso de montaje en HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server 2019, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
