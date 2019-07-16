---
title: Configurar los niveles de HDFS
titleSuffix: SQL Server big data clusters
description: Este artículo explica cómo configurar HDFS niveles para montar un sistema de archivos externo de Azure Data Lake Storage en HDFS en un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0397b0a27b98bb43a7513e0552124bba0972dfdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958316"
---
# <a name="configure-hdfs-tiering-on-sql-server-big-data-clusters"></a>Configurar HDFS niveles en clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Los niveles de HDFS proporciona la capacidad de montar externo, sistema de archivos compatible con HDFS en HDFS. Este artículo explica cómo configurar los niveles para los clústeres de macrodatos de 2019 de SQL Server (versión preliminar) de HDFS. En este momento, se admite la conexión a Azure Data Lake Storage Gen2 y Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Información general sobre los niveles de HDFS

Con los niveles, las aplicaciones pueden acceder sin problemas a datos en una variedad de almacenes externos como si los datos residen en el HDFS local. Montaje de archivos es una operación de metadatos, donde se copiarán los metadatos que describen el espacio de nombres del sistema de archivos externos a su instancia de HDFS local. Estos metadatos incluyen información sobre los archivos junto con sus permisos y las ACL y directorios externos. Los datos correspondientes son solo copiado y a petición, cuando se tiene acceso a los propios datos a través de una consulta de ejemplo por. Ahora se pueden acceder a los datos del sistema de archivos externo desde el clúster de macrodatos de SQL Server. Puede ejecutar Spark trabajos y consultas SQL en estos datos de la misma manera que debiera ejecutar en todos los datos locales almacenados en HDFS en el clúster.

### <a name="caching"></a>Almacenamiento en memoria caché
Hoy en día, de forma predeterminada, 1% del almacenamiento HDFS total se reservará para el almacenamiento en caché de datos montados. Almacenamiento en caché es una configuración global en montajes.

> [!NOTE]
> Los niveles de HDFS es una característica desarrollada por Microsoft, y se ha publicado una versión anterior del mismo como parte de la distribución de Apache Hadoop 3.1. Para obtener más información, consulte [ https://issues.apache.org/jira/browse/HDFS-9806 ](https://issues.apache.org/jira/browse/HDFS-9806) para obtener más información.

Las secciones siguientes proporcionan un ejemplo de cómo configurar la organización en niveles con un origen de datos de Azure Data Lake Storage Gen2 HDFS.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos implementada](deployment-guidance.md)
- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
  - **mssqlctl**
  - **kubectl**

## <a name="mounting-instructions"></a>Instrucciones de montaje

Se admite la conexión a Azure Data Lake Storage Gen2 y Amazon S3. Puede encontrar instrucciones sobre cómo montar frente a estos tipos de almacenamiento en los siguientes artículos:

- [Cómo Gen2 de ADLS de montaje para los niveles en un clúster de macrodatos HDFS](hdfs-tiering-mount-adlsgen2.md)
- [Cómo S3 de montaje para los niveles en un clúster de macrodatos HDFS](hdfs-tiering-mount-s3.md)

## <a id="issues"></a> Limitaciones y problemas conocidos

En la lista siguiente proporciona los problemas conocidos y limitaciones actuales cuando se usa HDFS en clústeres de macrodatos de SQL Server:

- Si el montaje está atascado en un `CREATING` estado durante mucho tiempo, lo más probable es que ha fallado. En esta situación, cancelar el comando y elimine el montaje si es necesario. Compruebe que los parámetros y las credenciales son correctas antes de Reintentar.

- No se puede crear montajes en directorios existentes.

- No se puede crear montajes dentro de montajes existentes.

- Si alguno de los antecesores del punto de montaje no existe, se crearán con los permisos r xr xr-x (555) de forma predeterminada.

- Creación de montaje puede tardar algún tiempo dependiendo del número y tamaño de los archivos que se va a montar. Durante este proceso, los archivos en el montaje no son visibles para los usuarios. Mientras se crea el montaje, todos los archivos se agregarán a una ruta de acceso temporal, cuyo valor predeterminado es `/_temporary/_mounts/<mount-location>`.

- El comando de creación de montaje es asincrónico. Después de ejecuta el comando, se puede comprobar el estado de montaje para comprender el estado del montaje.

- Al crear el montaje, se usa para el argumento **: ruta de acceso de montaje** es esencialmente un identificador único del montaje. Debe usarse la misma cadena (incluido "/" al final, si está presente) en los siguientes comandos.

- Los montajes son de solo lectura. No se puede crear todos los directorios o archivos de un montaje.

- No se recomienda directorios de montaje y los archivos que se pueden cambiar. Una vez creado el montaje, los cambios o actualizaciones a la ubicación remota no se reflejarán en el montaje en HDFS. Si se producen cambios en la ubicación remota, puede elegir eliminar y volver a crear el montaje para reflejar el estado actualizado.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
