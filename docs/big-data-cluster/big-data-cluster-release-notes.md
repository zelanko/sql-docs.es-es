---
title: Notas para los clústeres de SQL Server 2019 macrodatos | Microsoft Docs
description: En este artículo se describe las últimas actualizaciones y problemas conocidos de clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: b39b7ff732d068214e257061d7fbf60015070985
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221681"
---
# <a name="release-notes-for-sql-server-2019-big-data-clusters"></a>Notas de la versión para los clústeres de macrodatos de SQL Server 2019

Este artículo proporciona las últimas actualizaciones y problemas conocidos de la última versión de clústeres de macrodatos de SQL Server. La tabla siguiente incluye vínculos a la sección para las versiones se trata en este artículo.

| Versión | date |
|---|---|
| [CTP 2.1](#ctp21) | Noviembre de 2018 |
| [EN CTP 2.0](#ctp20) | Octubre de 2018 |


[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp21"></a> CTP 2.1 (noviembre de 2018)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.1.

### <a name="whats-in-the-ctp-21-release"></a>¿Qué es la versión de CTP 2.1?

- [Implementar aplicaciones de Python y R](big-data-cluster-create-apps.md) en un clúster de macrodatos.
- Nueva versión de **mssqlctl** y actualiza las imágenes. 
- Mejoras y correcciones de errores.

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes proporcionan los problemas conocidos para los clústeres de macrodatos de SQL Server en CTP 2.1.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior. Debe de copia de seguridad y eliminar cualquier clúster de macrodatos existente antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="admin-portal"></a>Portal de administración

- Cuando se [crear una aplicación con el comando msqlctl ctp](big-data-cluster-create-apps.md) e implementarlo en un clúster de macrodatos, el Portal de administración de clúster muestra los pods donde la aplicación se implementó como "Desconocido" en la sección del controlador de la parte del Administrador de SQL Server.

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark y cuadernos

- Pueden cambiar las direcciones IP de POD en el entorno de Kubernetes como reinicios de PODs. En el escenario donde se reinicia el patrón de pod, puede producir un error de la sesión de Spark con `NoRoteToHostException`. Esto se produce por las cachés JVM que no se actualiza con la nueva dirección IP direcciones.

- Si tiene Jupyter ya instalado y un independiente de Python en Windows, se pueden producir un error en cuadernos de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un bloc de notas, si hace clic en el **agregar texto** comando, se agrega el texto de la celda en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para activar o desactivar para el modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic derecho en un archivo de HDFS para obtener la vista previa, puede aparecer el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos mayores de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración HDFS que implican cambios en hdfs-site.xml.

#### <a name="security"></a>Seguridad

- El contraseña_sa forma parte del entorno y reconocibles (por ejemplo, en un archivo de volcado de cable). Debe restablecer el contraseña_sa en la instancia principal después de la implementación. Esto no es un error, pero un paso de seguridad. Para obtener más información sobre cómo cambiar el contraseña_sa en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros AKS pueden contener la contraseña de SA para las implementaciones de clústeres de datos de gran tamaño.

## <a id="ctp20"></a> En CTP 2.0 (octubre de 2018)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.0.

### <a name="whats-in-the-ctp-20-release"></a>¿Qué es la versión de CTP 2.0?

- Experiencia de implementación sencilla mediante la herramienta de administración mssqlctl
- Experiencia de cuaderno nativa en Azure Data Studio
- Archivos HDFS de consulta a través de almacenamiento de instancia de SQL Server
- Virtualización de datos a través maestro para SQL Server, Oracle, MongoDB y HDFS
- Asistente para la virtualización de datos de SQL Server y Oracle en Azure Data Studio
- Servicios de aprendizaje automático en maestro
- Portal de administración de clúster que puede usar para la supervisión y solución de problemas
- Enviar trabajo de Spark en Azure Data Studio 
- Interfaz de usuario de Spark en el portal de administración de clúster
- Para clases de almacenamiento de montaje de volumen
- Realizar consultas sobre los grupos de datos de master
- Muestra el plan para consultas distribuidas en SSMS
- Paquete de PIP para mssqlctl herramienta de administración
- Motor de implementación integradas a través del servicio de controlador

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes proporcionan los problemas conocidos para los clústeres de macrodatos de SQL Server en CTP 2.0.

#### <a name="deployment"></a>Implementación

- Si usa Azure Kubernetes Service (AKS), la versión recomendada de Kubernetes es 1.10. *, que no admite el cambio de tamaño de disco. Debe asegurarse de que se cambia el tamaño del almacenamiento en consecuencia en tiempo de implementación. Para obtener más información sobre cómo ajustar el tamaño de almacenamiento, consulte el [persistencia de datos](concept-data-persistence.md) artículo. Para Kubernetes implementado en máquinas virtuales, la versión recomendada es 1.11.

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark y cuadernos

- Pueden cambiar las direcciones IP de POD en el entorno de Kubernetes como reinicios de PODs. En el escenario donde se reinicia el patrón de pod, puede producir un error de la sesión de Spark con `NoRoteToHostException`. Esto se produce por las cachés JVM que no se actualiza con la nueva dirección IP direcciones.

- Si tiene Jupyter ya instalado y un independiente de Python en Windows, se pueden producir un error en cuadernos de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un bloc de notas, si hace clic en el **agregar texto** comando, se agrega el texto de la celda en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para activar o desactivar para el modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic derecho en un archivo de HDFS para obtener la vista previa, puede aparecer el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos mayores de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración HDFS que implican cambios en hdfs-site.xml.

#### <a name="security"></a>Seguridad

- El contraseña_sa forma parte del entorno y reconocibles (por ejemplo, en un archivo de volcado de cable). Debe restablecer el contraseña_sa en la instancia principal después de la implementación. Esto no es un error, pero un paso de seguridad. Para obtener más información sobre cómo cambiar el contraseña_sa en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros AKS pueden contener la contraseña de SA para las implementaciones de clústeres de datos de gran tamaño.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
