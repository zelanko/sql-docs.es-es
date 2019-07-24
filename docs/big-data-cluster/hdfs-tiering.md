---
title: Configuración de la organización en niveles de HDFS
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo configurar la organización en niveles de HDFS para montar un sistema de archivos de Azure Data Lake Storage externo en HDFS en un clúster de macrodatos de SQL Server 2019 (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 17eedf9f0797a0adb5eda6ca8ee090fc762e1491
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419378"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configuración de la organización en niveles de HDFS en clústeres de macrodatos SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La organización en niveles de HDFS proporciona la capacidad de montar el sistema de archivos externo compatible con HDFS en HDFS. En este artículo se explica cómo configurar la organización en niveles de HDFS para clústeres de macrodatos de SQL Server 2019 (versión preliminar). En este momento, se admite la conexión a Azure Data Lake Storage Gen2 y Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Información general sobre la organización en niveles de HDFS

Con los niveles, las aplicaciones pueden acceder sin problemas a los datos de una variedad de almacenes externos como si los datos residan en el HDFS local. El montaje es una operación de metadatos, donde los metadatos que describen el espacio de nombres en el sistema de archivos externo se copian en el HDFS local. Estos metadatos incluyen información acerca de los directorios y archivos externos junto con sus permisos y ACL. Los datos correspondientes solo se copian a petición, cuando se tiene acceso a los propios datos a través de, por ejemplo, una consulta. Ahora se puede acceder a los datos externos del sistema de archivos desde el SQL Server clúster de Big Data. Puede ejecutar trabajos de Spark y consultas SQL en estos datos de la misma manera en que se ejecutan en los datos locales almacenados en HDFS en el clúster.

### <a name="caching"></a>Almacenamiento en memoria caché
En la actualidad, de forma predeterminada, el 1% del almacenamiento HDFS total se reservará para el almacenamiento en caché de los datos montados. El almacenamiento en caché es una configuración global entre los montajes.

> [!NOTE]
> La organización en niveles de HDFS es una característica desarrollada por Microsoft y se ha publicado una versión anterior de, como parte de Apache Hadoop distribución 3,1. Para obtener más información, [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) vea para obtener más información.

En las secciones siguientes se proporciona un ejemplo de cómo configurar la organización en niveles de HDFS con un origen de datos de Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Actualizar

La organización en niveles de HDFS admite la actualización. Actualice un montaje existente para la instantánea más reciente de los datos remotos.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de Big Data implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Instrucciones de montaje

Se admite la conexión a Azure Data Lake Storage Gen2 y Amazon S3. Puede encontrar instrucciones sobre cómo montar en estos tipos de almacenamiento en los siguientes artículos:

- [Cómo montar ADLS Gen2 para la organización en niveles de HDFS en un clúster de Big Data](hdfs-tiering-mount-adlsgen2.md)
- [Cómo montar S3 para la organización en niveles de HDFS en un clúster de Big Data](hdfs-tiering-mount-s3.md)

## <a id="issues"></a>Problemas conocidos y limitaciones

En la lista siguiente se proporcionan los problemas conocidos y las limitaciones actuales al usar los niveles de HDFS en los clústeres de macrodatos de SQL Server:

- Si el montaje está atascado en `CREATING` un estado durante mucho tiempo, lo más probable es que se haya producido un error. En esta situación, cancele el comando y elimine el montaje si es necesario. Compruebe que los parámetros y las credenciales sean correctos antes de volver a intentarlo.

- No se pueden crear montajes en directorios existentes.

- Los montajes no se pueden crear en montajes existentes.

- Si alguno de los antecesores del punto de montaje no existe, se creará con los permisos predeterminados para r-XR-XR-x (555).

- La creación de montajes puede tardar algún tiempo según el número y el tamaño de los archivos que se montan. Durante este proceso, los archivos del montaje no son visibles para los usuarios. Mientras se crea el montaje, todos los archivos se agregarán a una ruta de acceso temporal, cuyo `/_temporary/_mounts/<mount-location>`valor predeterminado es.

- El comando de creación de montaje es asincrónico. Después de ejecutar el comando, se puede comprobar el estado de montaje para conocer el estado del montaje.

- Al crear el montaje, el argumento que se usa para **--Mount-path** es esencialmente un identificador único del montaje. La misma cadena (incluida la "/" al final si está presente) debe usarse en los siguientes comandos.

- Los montajes son de solo lectura. No puede crear directorios ni archivos en un montaje.

- No se recomienda el montaje de directorios y archivos que puedan cambiar. Una vez creado el montaje, los cambios o actualizaciones de la ubicación remota no se reflejarán en el montaje en HDFS. Si se producen cambios en la ubicación remota, puede optar por eliminar y volver a crear el montaje para reflejar el estado actualizado.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server 2019, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
