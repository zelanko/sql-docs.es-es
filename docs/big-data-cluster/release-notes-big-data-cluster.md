---
title: Notas de la versión para clústeres de macrodatos de SQL Server
titleSuffix: SQL Server big data clusters
description: En este artículo se describen las actualizaciones más recientes y los problemas conocidos de los clústeres de macrodatos de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9de368594383ef1f7fe3ae3c062f92873fb15698
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2020
ms.locfileid: "77256908"
---
# <a name="sql-server-2019-big-data-clusters-release-notes"></a>Notas de la versión para los Clústeres de macrodatos de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Las notas de la versión siguientes se aplican a [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Este artículo se divide en secciones para cada versión. Cada versión tiene un vínculo a un artículo de asistencia en el que se describen los cambios de la CU, así como vínculos a las descargas de los paquetes de Linux. En el artículo también se enumeran los [problemas conocidos](#known-issues) para las versiones más recientes de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] (BDC).

## <a name="supported-platforms"></a>Plataformas compatibles

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

### <a name="sql-server-editions"></a>Ediciones de SQL Server

|Edición|Notas|
|---------|---------|
|Enterprise<br/>Estándar<br/>Desarrollador| La edición del clúster de macrodatos la determina la edición de la instancia maestra de SQL Server. En el momento de la implementación, se implementa de forma predeterminada la edición Developer. Puede cambiar la edición después de la implementación. Vea [Configuración de la instancia maestra de SQL Server](../big-data-cluster/configure-sql-server-master-instance.md). |

## <a name="tools"></a>Herramientas

|Plataforma|Versiones compatibles|
|---------|---------|
|`azdata`|Debe ser la misma versión secundaria que la del servidor (igual que la instancia maestra de SQL Server).<br/><br/>Ejecute `azdata –-version` para validar la versión.<br/><br/>A partir de SQL Server 2019 CU2, esta versión es `15.0.4013`.|
|Azure Data Studio|Obtenga la versión más reciente de [Azure Data Studio](https://aka.ms/getazuredatastudio).|

## <a name="release-history"></a>Historial de versiones

En la tabla siguiente, se muestra la lista del historial de versiones de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

| Release               | Versión       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CU2](#cu2)           | 15.0.4013.40    | 13-02-2020   |
| [CU1](#cu1)           | 15.0.4003.23   | 07-01-2020   |
| [GDR1](#rtm)            | 15.0.2070.34  | 2019-11-04   |

## <a name="how-to-install-updates"></a>Instalación de las actualizaciones

Para instalar las actualizaciones, consulte [Cómo actualizar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-upgrade.md).

## <a id="cu2"></a> CU2 (febrero de 2020)

Versión de actualización acumulativa 2 (CU2) para SQL Server 2019. La versión de Motor de base de datos de SQL Server de esta versión es la 15.0.4003.23.

|Versión del paquete | Etiqueta de imagen |
|-----|-----|
|15.0.4013.40 |[2019-CU2-ubuntu-16.04]

## <a id="cu1"></a> CU1 (enero de 2020)

Versión de actualización acumulativa 1 (CU1) para SQL Server 2019. La versión de Motor de base de datos de SQL Server de esta versión es la 15.0.4003.23.

|Versión del paquete | Etiqueta de imagen |
|-----|-----|
|15.0.4003.23|[2019-CU1-ubuntu-16.04]

## <a id="rtm"></a> GDR1 (noviembre de 2019)

Versión de distribución general 1 (GDR1) de SQL Server 2019, presenta la disponibilidad general para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-nover.md)]. La versión de Motor de base de datos de SQL Server de esta versión es la 15.0.2070.34.

|Versión del paquete | Etiqueta de imagen |
|-----|-----|
|15.0.2070.34|[2019-GDR1-ubuntu-16.04]

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="known-issues"></a>Problemas conocidos

### <a name="deployment-with-private-repository"></a>Implementación con repositorio privado

- **Problema e impacto en el cliente**: La actualización del repositorio privado tiene requisitos específicos

- **Solución alternativa**: si usa un repositorio privado para extraer previamente las imágenes para implementar o actualizar BDC, asegúrese de que las imágenes de compilación actuales, así como las imágenes de compilación de destino se encuentran en el repositorio privado. Esto permite una reversión correcta, si es necesario. Además, si cambió las credenciales del repositorio privado desde la implementación original, actualice el secreto correspondiente en Kubernetes antes de la actualización. `azdata` no admite la actualización de las credenciales a través de las variables de entorno `AZDATA_PASSWORD` y `AZDATA_USERNAME`. Actualice el secreto mediante [`kubectl edit secrets`](https://kubernetes.io/docs/concepts/configuration/secret/#editing-a-secret). 

No se admite la actualización mediante distintos repositorios privados para compilaciones actuales y de destino.

### <a name="upgrade-may-fail-due-to-timeout"></a>Puede generarse un error de actualización debido a un tiempo de espera

- **Problema e impacto en el cliente**: Puede generarse un error de actualización debido a un tiempo de espera.

   En el código siguiente se muestra el aspecto del error:

   ```
   >azdata.EXE bdc upgrade --name <mssql-cluster>
   Upgrading cluster to version 15.0.4003

   NOTE: Cluster upgrade can take a significant amount of time depending on
   configuration, network speed, and the number of nodes in the cluster.

   Upgrading Control Plane.
   Control plane upgrade failed. Failed to upgrade controller.
   ```

   Es más probable que este error se produzca al actualizar BDC en Azure Kubernetes Service (AKS).

- **Solución alternativa**: aumente el tiempo de espera de la actualización. 

   Para aumentar los tiempos de espera de una actualización, edite la asignación de configuración de la actualización. Para editar la asignación de configuración de la actualización:

   1. Ejecute el siguiente comando:

      ```bash
      kubectl edit configmap controller-upgrade-configmap
      ```

   2.   Edite estos campos:

       **`controllerUpgradeTimeoutInMinutes`** designa el número de minutos que se esperará a que finalice la actualización del controlador o de la base de datos del controlador. El valor predeterminado es 5. Actualice al menos a 20.

       **`totalUpgradeTimeoutInMinutes`** : designa la cantidad de tiempo para que el controlador y la base de datos del controlador terminen de actualizarse (actualización del controlador y de la base de datos del controlador). El valor predeterminado es 10. Actualice al menos a 40.

       **`componentUpgradeTimeoutInMinutes`** : designa la cantidad de tiempo en que se debe completar cada fase posterior de la actualización.  El valor predeterminado es 30. Actualice a 45.

   3.   Guarde y salga.

   El script de Python siguiente es otra manera de establecer el tiempo de espera:

   ```python
   from kubernetes import client, config
   import json

   def set_upgrade_timeouts(namespace, controller_timeout=20, controller_total_timeout=40, component_timeout=45):
       """ Set the timeouts for upgrades

       The timeout settings are as follows

       controllerUpgradeTimeoutInMinutes: sets the max amount of time for the controller
           or controllerdb to finish upgrading

       totalUpgradeTimeoutInMinutes: sets the max amount of time to wait for both the
           controller and controllerdb to complete their upgrade

       componentUpgradeTimeoutInMinutes: sets the max amount of time allowed for
           subsequent phases of the upgrade to complete
       """
       config.load_kube_config()

       upgrade_config_map = client.CoreV1Api().read_namespaced_config_map("controller-upgrade-configmap", namespace)

       upgrade_config = json.loads(upgrade_config_map.data["controller-upgrade"])

       upgrade_config["controllerUpgradeTimeoutInMinutes"] = controller_timeout

       upgrade_config["totalUpgradeTimeoutInMinutes"] = controller_total_timeout

       upgrade_config["componentUpgradeTimeoutInMinutes"] = component_timeout

       upgrade_config_map.data["controller-upgrade"] = json.dumps(upgrade_config)

       client.CoreV1Api().patch_namespaced_config_map("controller-upgrade-configmap", namespace, upgrade_config_map)
   ```

### <a name="livy-job-submission-from-azure-data-studio-ads-or-curl-fail-with-500-error"></a>Error 500 al enviar el trabajo de Livy desde Azure Data Studio (ADS) o curl

- **Problema e impacto en el cliente**: en una configuración de alta disponibilidad, los recursos compartidos de Spark `sparkhead` se configuran con varias réplicas. En este caso, es posible que experimente errores con el envío del trabajo de Livy desde Azure Data Studio (ADS) o `curl`. Para comprobarlo, la ejecución de `curl` en cualquier pod de `sparkhead` da como resultado una conexión rechazada. Por ejemplo, `curl https://sparkhead-0:8998/` o `curl https://sparkhead-1:8998` devuelve el error 500.

   Esto sucede en los escenarios siguientes:

   - Los pods de Zookeeper o los procesos de cada instancia de Zookeeper se reinician varias veces.
   - Cuando la conectividad de red no es confiable entre el pod de `sparkhead` y los pods de Zookeeper.

- **Solución alternativa**: reinicie los dos servidores de Livy.

   ```bash
   kubectl -n <clustername> exec sparkhead-0 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

   ```bash
   kubectl -n <clustername> exec sparkhead-1 -c hadoop-livy-sparkhistory supervisorctl restart livy
   ```

### <a name="create-memory-optimized-table-when-master-instance-in-an-availability-group"></a>Creación de una tabla optimizada para memoria cuando la instancia maestra está en un grupo de disponibilidad

- **Problema e impacto en el cliente**: no se puede usar el punto de conexión principal expuesto para conectarse a las bases de datos del grupo de disponibilidad (agente de escucha) para crear tablas optimizadas para memoria.

- **Solución alternativa**: para crear tablas optimizadas para memoria cuando la instancia maestra de SQL Server es una configuración de grupo de disponibilidad, [conéctese a la instancia de SQL Server](deployment-high-availability.md#instance-connect), exponga un punto de conexión, conéctese a la base de datos SQL Server y cree las tablas optimizadas para memoria en la sesión creada con la nueva conexión.

### <a name="insert-to-external-tables-active-directory-authentication-mode"></a>Inserción en el modo de autenticación de Active Directory en tablas externas

- **Problema e impacto en el cliente**: cuando la instancia maestra de SQL Server está en el modo de autenticación Active Directory, una consulta que selecciona solo en tablas externas, donde al menos una está en un grupo de almacenamiento, e inserta en otra tabla externa, devuelve lo siguiente:

   ```
   Msg 7320, Level 16, State 102, Line 1
   Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "SQLNCLI11". Only domain logins can be used to query Kerberized storage pool.
   ```

- **Solución alternativa**: modifique la consulta de una de las maneras siguientes. Puede unir la tabla de bloque de almacenamiento a una tabla local, o bien insertar primero en la tabla local y después leer desde la tabla local para insertar en el grupo de datos.

### <a name="transparent-data-encryption-capabilities-can-not-be-used-with-databases-that-are-part-of-the-availability-group-in-the-sql-server-master-instance"></a>Las funcionalidades de Cifrado de datos transparente no se pueden usar con las bases de datos que forman parte del grupo de disponibilidad en la instancia maestra de SQL Server.

- **Problema e impacto en el cliente**: en una configuración de alta disponibilidad, las bases de datos que tienen habilitado el cifrado no se pueden usar después de una conmutación por error, ya que la clave maestra usada para el cifrado es distinta en cada réplica. 

- **Solución alternativa**: No hay ninguna solución alternativa para este problema. Se recomienda no habilitar el cifrado en esta configuración hasta que se realice una corrección.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], vea [¿Qué son los [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)?
