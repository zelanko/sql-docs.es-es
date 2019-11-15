---
title: Notas de la versión para clústeres de macrodatos de SQL Server
titleSuffix: SQL Server big data clusters
description: En este artículo se describen las actualizaciones más recientes y los problemas conocidos de los clústeres de macrodatos de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bc5928a7e3015545d36900b52ef01a42d9694cc0
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706172"
---
# <a name="sql-server-big-data-clusters-release-notes"></a>Notas de la versión para clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Obtenga información casi en tiempo real de todos los datos con [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], que proporcionan un entorno completo para trabajar con grandes conjuntos de datos, incluidas funciones de inteligencia artificial y aprendizaje automático.

En este artículo se enumeran las actualizaciones y los problemas conocidos de las versiones más recientes de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC).

## <a id="rtm"></a> SQL Server 2019

En [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] se introducen los clústeres de macrodatos de SQL Server.

Use los clústeres de macrodatos de SQL Server para:

- [Implementar clústeres escalables](../big-data-cluster/deploy-get-started.md) de contenedores de SQL Server, Spark y HDFS que se ejecutan en Kubernetes. 
- Leer, escribir y procesar macrodatos desde Transact-SQL o Spark.
- Combinar y analizar de forma sencilla datos relacionales de alto valor con macrodatos de gran volumen.
- Consultar orígenes de datos externos.
- Almacenar macrodatos en HDFS administrados mediante SQL Server.
- Consultar datos de varios orígenes de datos externos a través del clúster.
- Usar los datos para tareas de inteligencia artificial, aprendizaje automático y otras tareas de análisis.
- [Implementación y ejecución de aplicaciones](../big-data-cluster/concept-application-deployment.md) en [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)].
- Virtualización de datos con [PolyBase](../relational-databases/polybase/polybase-guide.md). Consulte datos de orígenes de datos externos de SQL Server, Oracle, Teradata, MongoDB y ODBC con tablas externas.
- Proporcione alta disponibilidad para la instancia maestra de SQL Server y todas las bases de datos mediante la tecnología de grupos de disponibilidad AlwaysOn.

## <a name="sql-server-version"></a>Versión de SQL Server

La versión actual de SQL Server es `15.0.2070.34`.

## <a name="image-tags"></a>Etiquetas de imagen

La etiqueta de imagen de esta versión es `2019-GDR1-ubuntu-16.04`.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="supportability"></a>Compatibilidad

En esta sección se explican las plataformas compatibles con [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC).

### <a name="kubernetes-platforms"></a>Plataformas Kubernetes

|Plataforma|Versiones compatibles|
|---------|---------|
|Kubernetes|BDC requiere la versión 1.13 de Kubernetes como mínimo. Vea [Kubernetes version and version skew support policy](https://kubernetes.io/docs/setup/release/version-skew-policy/) (Versión de Kubernetes y directiva de compatibilidad de sesgo de versión) para obtener la directiva de compatibilidad con versiones de Kubernetes.|
|Azure Kubernetes Service (AKS)|BDC requiere la versión 1.13 de AKS como mínimo.<br/>Vea [Versiones de Kubernetes compatibles en Azure Kubernetes Service (AKS)](/azure/aks/supported-kubernetes-versions) para obtener la directiva de compatibilidad de versiones.|

### <a name="host-os-for-kubernetes"></a>SO del host para Kubernetes

|Plataforma|Versiones compatibles|
|---------|---------|
|Red Hat Enterprise Linux|7.3, 7.4, 7.5, 7.6|
|Ubuntu|16.04|

### <a name="tools"></a>Herramientas

|Plataforma|Versiones compatibles|
|---------|---------|
|`azdata`|Debe ser la misma versión secundaria que la del servidor (igual que la instancia maestra de SQL Server).<br/>Ejecute `azdata –-version` para validar la versión. Actualmente, esta versión es `15.0.2070`.|
|Azure Data Studio|Obtenga la versión más reciente de [Azure Data Studio](https://aka.ms/getazuredatastudio).|

### <a name="sql-server-editions"></a>Ediciones de SQL Server

|Edición|Notas|
|---------|---------|
|Enterprise<br/>Estándar<br/>Desarrollador| La edición del clúster de macrodatos la determina la edición de la instancia maestra de SQL Server. En el momento de la implementación, se implementa de forma predeterminada la edición Developer. Puede cambiar la edición después de la implementación. Vea [Configuración de la instancia maestra de SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="known-issues"></a>Problemas conocidos

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>Error 500 al enviar el trabajo de Livy desde Azure Data Studio (ADS) o curl

**Problema e impacto en el cliente**: En una configuración de alta disponibilidad, los recursos compartidos de Spark (sparkhead) se configuran con varias réplicas. En este caso, es posible que experimente errores con el envío del trabajo de Livy desde Azure Data Studio (ADS) o `curl`. Para comprobarlo, la ejecución de `curl` en cualquier pod de sparkhead da como resultado una conexión rechazada. Por ejemplo, `curl https://sparkhead-0:8998/` o `curl https://sparkhead-1:8998` devuelve el error 500.

Esto sucede en los escenarios siguientes:

- Los pods de zookeeper o el proceso de cada instancia de zookeeper se reinician varias veces.
- Cuando la conectividad de red no es confiable entre el pod de Sparkhead y los pods de Zookeeper.

**Solución**: reinicie los dos servidores de Livy.

```bash
kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

```bash
kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>Creación de una tabla optimizada para memoria cuando la instancia maestra está en un grupo de disponibilidad

- **Problema e impacto en el cliente**: no se puede usar el punto de conexión principal expuesto para conectarse a las bases de datos del grupo de disponibilidad (agente de escucha) para crear tablas optimizadas para memoria.

- **Solución**: para crear tablas optimizadas para memoria cuando la instancia maestra de SQL Server es una configuración de grupo de disponibilidad, [conéctese a la instancia de SQL Server](deployment-high-availability.md#instance-connect), exponga un punto de conexión, conéctese a la base de datos SQL Server y cree las tablas optimizadas para memoria en la sesión creada con la nueva conexión.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Inserción en el modo de autenticación de Active Directory en tablas externas

- **Problema e impacto en el cliente**: cuando la instancia maestra de SQL Server está en el modo de autenticación Active Directory, una consulta que selecciona solo en tablas externas, donde al menos una está en un grupo de almacenamiento, e inserta en otra tabla externa, devuelve lo siguiente:

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **Solución**: modifique la consulta de una de las maneras siguientes. Puede unir la tabla de bloque de almacenamiento a una tabla local, o bien insertar primero en la tabla local y después leer desde la tabla local para insertar en el grupo de datos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)?
