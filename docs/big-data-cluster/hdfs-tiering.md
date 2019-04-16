---
title: Configurar los niveles de HDFS
titleSuffix: SQL Server big data clusters
description: Este artículo explica cómo configurar HDFS niveles para montar un sistema de archivos externo de Azure Data Lake Storage en HDFS en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32648829c64143b4f31a5d27479bbc3d28076fa2
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582428"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurar HDFS niveles en clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Los niveles de HDFS proporciona la capacidad de montar externo, sistema de archivos compatible con HDFS en HDFS. Este artículo explica cómo configurar los niveles para los clústeres de macrodatos de 2019 de SQL Server (versión preliminar) de HDFS. En este momento, CTP 2.4 solo admite la conexión a Azure Data Lake Storage Gen2, que es el enfoque de este artículo.

## <a name="hdfs-tiering-overview"></a>Información general sobre los niveles de HDFS

Con los niveles, las aplicaciones pueden acceder sin problemas a datos en una variedad de almacenes externos como si los datos residen en HDFS. Montaje de archivos es una operación de metadatos, donde se copiarán los metadatos que describen el espacio de nombres del sistema de archivos externos en HDFS. Estos metadatos incluyen información sobre los archivos junto con sus permisos y las ACL y directorios externos. Los datos correspondientes son solo copiado y a petición, cuando se tiene acceso a los datos en Sí. Ahora se pueden acceder a los datos del sistema de archivos externo desde el clúster de macrodatos de SQL Server. Puede ejecutar Spark trabajos y consultas SQL en estos datos de la misma manera que debiera ejecutar en todos los datos locales almacenados en HDFS en el clúster.

> [!NOTE]
> Los niveles de HDFS es una característica desarrollada por Microsoft, y se ha publicado una versión anterior del mismo como parte de la distribución de Apache Hadoop 3.1. Para obtener más información, consulte [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) para obtener más información.

Las secciones siguientes proporcionan un ejemplo de cómo configurar la organización en niveles con un origen de datos de Azure Data Lake Storage Gen2 HDFS.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos implementada](deployment-guidance.md)
- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a id="load"></a> Cargar datos en Azure Data Lake Storage

La siguiente sección describe cómo configurar Azure Data Lake almacenamiento Gen2 para probar los niveles de HDFS. Si ya tiene datos almacenados en Azure Data Lake Storage, puede omitir esta sección para usar sus propios datos.

1. [Crear una cuenta de almacenamiento con las funcionalidades de Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Crear un contenedor de blobs](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) en esta cuenta de almacenamiento para los datos externos.

1. Cargue un archivo CSV o Parquet en el contenedor. Se trata de los datos HDFS externos que se montará en HDFS en el clúster de macrodatos.

## <a id="mount"></a> Montar el almacenamiento HDFS remoto

Los pasos siguientes montar el almacenamiento HDFS remoto en Azure Data Lake en el almacenamiento HDFS local de su clúster de macrodatos.

1. Abra un símbolo en un equipo cliente que puede tener acceso al clúster de macrodatos.

1. Cree un archivo local denominado **files.creds** que contiene sus credenciales de cuenta de Azure Data Lake Storage Gen2 con el formato siguiente:

   ```text
   fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

   > [!TIP]
   > Para obtener más información sobre cómo buscar la clave de acceso (`<storage-account-access-key>`) para la cuenta de almacenamiento, consulte [ver y copiar las claves de acceso](https://docs.microsoft.com/azure/storage/common/storage-account-manage?#view-and-copy-access-keys).

1. Use **kubectl** para buscar la dirección IP para el **proxy de servicio de punto de conexión** servicio en el clúster de macrodatos. Busque el **External-IP**.

   ```bash
   kubectl get svc endpoint-service-proxy -n <your-cluster-name>
   ```

1. Inicie sesión con **mssqlctl** con el punto de conexión de proxy de servicio con el nombre de usuario del clúster y la contraseña:

   ```bash
   mssqlctl login -e https://<IP-of-endpoint-service-proxy>:30777/ -u <username> -p <password>
   ```

1. Montar el almacenamiento HDFS remoto en Azure mediante **crear montaje del almacenamiento mssqlctl**. Reemplace los valores de marcador de posición antes de ejecutar el comando siguiente:

   ```bash
   mssqlctl storage mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name> --credential-file <path-to-adls-credentials>/file.creds
   ```

   > [!NOTE]
   > El montaje crear comando es asincrónica. En este momento, no hay ningún mensaje que indica si el montaje se realizó correctamente. Consulte la [estado](#status) sección para comprobar el estado de sus montajes.

Si ha montado correctamente, podrá consultar los datos HDFS y ejecutar trabajos de Spark en él. Aparecerá en el HDFS del clúster de macrodatos en la ubicación especificada por `--local-path`.

## <a id="status"></a> Obtener el estado de montajes

Para mostrar el estado de todos los montajes en el clúster de macrodatos, utilice el siguiente comando:

```bash
mssqlctl storage mount status
```

Para mostrar el estado de un montaje en una ruta específica en HDFS, use el siguiente comando:

```bash
mssqlctl storage mount status --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminar el montaje

Para eliminar el montaje, use el **mssqlctl almacenamiento montaje delete** comando y especifique la ruta de acceso de montaje en HDFS:

```bash
mssqlctl storage mount delete --mount-path <mount-path-in-hdfs>
```

## <a id="issues"></a> Limitaciones y problemas conocidos

En la lista siguiente proporciona los problemas conocidos y limitaciones actuales cuando se usa HDFS en clústeres de macrodatos de SQL Server:

- Si el tamaño del directorio externo que se va a montar es mayor que la capacidad del clúster, se produce un error de montaje.

- Si el montaje está atascado en un `CREATING` estado durante mucho tiempo, lo más probable es que ha fallado. En esta situación, cancelar el comando y elimine el montaje si es necesario. Compruebe que los parámetros y las credenciales son correctas antes de Reintentar.

- No se puede crear montajes en directorios existentes.

- No se puede crear montajes dentro de montajes existentes.

- Si alguno de los antecesores del punto de montaje no existe, se crearán con los permisos r xr xr-x (555) de forma predeterminada.

- Creación de montaje puede tardar algún tiempo dependiendo del número y tamaño de los archivos que se va a montar. Durante este proceso, los archivos en el montaje no son visibles para los usuarios. Mientras se crea el montaje, todos los archivos se agregarán a una ruta de acceso temporal, cuyo valor predeterminado es `/_temporary/_mounts/<mount-location>`.

- El comando de creación de montaje es asincrónico. Después de ejecuta el comando, se puede comprobar el estado de montaje para comprender el estado del montaje.

- Al crear el montaje, se usa para el argumento **--local-path** es esencialmente un identificador único del montaje. Debe usarse la misma cadena (incluido "/" al final, si está presente) en los siguientes comandos.

- Los montajes son de solo lectura. No se puede crear todos los directorios o archivos de un montaje.

- No se recomienda directorios de montaje y los archivos que se pueden cambiar. Una vez creado el montaje, los cambios o actualizaciones a la ubicación remota no se reflejarán en el montaje en HDFS. Si se producen cambios en la ubicación remota, puede elegir eliminar y volver a crear el montaje para reflejar el estado actualizado.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
