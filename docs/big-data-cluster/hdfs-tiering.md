---
title: Configuración de la organización en niveles de HDFS
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo configurar la organización en niveles de HDFS para montar un sistema de archivos de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]Azure Data Lake Storage externo en HDFS en un.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c7b24af0b0c6a22cbab1a9c280a0ba868ca2cd21
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652326"
---
# <a name="configure-hdfs-tiering-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Configuración de la organización en niveles de HDFS[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

La organización en niveles de HDFS ofrece la posibilidad de montar un sistema de archivos externo compatible con HDFS en HDFS. En este artículo se explica cómo configurar la organización en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] niveles de HDFS para (versión preliminar). En este momento, se admite la conexión con Azure Data Lake Storage Gen2 y Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Introducción a la organización en niveles de HDFS

Con la organización en niveles, las aplicaciones pueden acceder sin problemas a los datos de diversos almacenes externos como si los datos residieran en el HDFS local. El montaje es una operación de metadatos, donde los metadatos que describen el espacio de nombres en el sistema de archivos externo se copian en el HDFS local. Estos metadatos incluyen información sobre los directorios y archivos externos con sus permisos y listas de control de acceso (ACL). Los datos correspondientes solo se copian a petición, cuando se accede a los propios datos a través de, por ejemplo, una consulta. Ahora se puede acceder a los datos externos del sistema de archivos desde el clúster de macrodatos de SQL Server. Puede ejecutar trabajos de Spark y consultas SQL en estos datos de la misma manera que los ejecutaría en los datos locales almacenados en HDFS en el clúster.

### <a name="caching"></a>Almacenamiento en memoria caché
En la actualidad, de forma predeterminada, el 1 % del almacenamiento total de HDFS se reservará para el almacenamiento en caché de los datos montados. El almacenamiento en caché es una configuración global entre los montajes.

> [!NOTE]
> La organización en niveles de HDFS es una característica desarrollada por Microsoft y se ha publicado una versión anterior como parte de la distribución de Apache Hadoop 3.1. Para más información, consulte [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806).

En las secciones siguientes se ofrece un ejemplo de cómo configurar la organización en niveles de HDFS con un origen de datos de Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Actualizar

La organización en niveles de HDFS admite la actualización. Actualice un montaje existente para la instantánea más reciente de los datos remotos.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Instrucciones de montaje

Se admite la conexión con Azure Data Lake Storage Gen2 y Amazon S3. Puede encontrar instrucciones sobre cómo montar en estos tipos de almacenamiento en los siguientes artículos:

- [Cómo montar ADLS Gen2 en niveles de HDFS en un clúster de macrodatos](hdfs-tiering-mount-adlsgen2.md)
- [Cómo montar S3 en niveles de HDFS en un clúster de macrodatos](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> Limitaciones y problemas conocidos

En la lista siguiente se proporcionan los problemas conocidos y las limitaciones actuales cuando se [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]usa la organización en niveles de HDFS en:

- Si el montaje se queda en un estado `CREATING` durante mucho tiempo, lo más probable es que se haya producido un error. En esta situación, cancele el comando y, si es necesario, elimine el montaje. Compruebe que los parámetros y las credenciales sean correctos antes de volver a intentarlo.

- No se pueden crear montajes en directorios existentes.

- No se pueden crear montajes en montajes existentes.

- Si alguno de los antecesores del punto de montaje no existe, se creará con los permisos predeterminados para r-xr-xr-x (555).

- La creación de montajes puede tardar algún tiempo según el número y el tamaño de los archivos que se montan. Durante este proceso, los archivos del montaje no son visibles para los usuarios. Mientras se crea el montaje, todos los archivos se agregarán a una ruta de acceso temporal, cuyo valor predeterminado es `/_temporary/_mounts/<mount-location>`.

- El comando de creación de montaje es asincrónico. Después de ejecutar el comando, se puede comprobar el estado de montaje para conocerlo.

- Al crear el montaje, el argumento que se usa para **--mount-path** es esencialmente un identificador único del montaje. La misma cadena (incluida la "/" al final si está presente) debe usarse en los siguientes comandos.

- Los montajes son de solo lectura. No se pueden crear directorios ni archivos en un montaje.

- No se recomienda el montaje de directorios y archivos que puedan cambiar. Una vez creado el montaje, los cambios o las actualizaciones de la ubicación remota no se reflejarán en el montaje en HDFS. Si se producen cambios en la ubicación remota, puede optar por eliminar y volver a crear el montaje para que refleje el estado actualizado.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]acerca de, vea [¿Qué es [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
