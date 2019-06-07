---
title: Notas de la versión
titleSuffix: SQL Server big data clusters
description: En este artículo se describe las últimas actualizaciones y problemas conocidos de clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: f4520fe88844fcece48ca397041e0e1b8845519c
ms.sourcegitcommit: 32dce314bb66c03043a93ccf6e972af455349377
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744150"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Notas de la versión para los clústeres de datos de gran tamaño en SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se enumeran las actualizaciones y saber que los problemas de las versiones más recientes de los clústeres de macrodatos de SQL Server.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp30"></a> CTP 3.0 (mayo)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de macrodatos en CTP 3.0 de SQL Server de 2019.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| **mssqlctl** updates | Varias [actualizaciones de comandos y parámetros](../big-data-cluster/reference-mssqlctl.md) de **mssqlctl**. Esto incluye una actualización del comando **mssqlctl login**, que ahora se dirige al punto de conexión y al nombre de usuario del controlador. |
| Mejoras en el almacenamiento | Compatibilidad con distintas configuraciones de almacenamiento para registros y datos. Además, se ha reducido el número de notificaciones de volumen persistentes para un clúster de macrodatos. |
| Varias instancias de grupos de procesos | Compatibilidad con varias instancias de grupos de procesos. |
| Nuevas características y nuevo comportamiento del grupo | Ahora, el grupo de procesos se utiliza de forma predeterminada para las operaciones de grupo de almacenamiento y grupo de datos solo en distribución **ROUND_ROBIN**. Ahora, el grupo de datos puede utilizar un nuevo tipo de distribución, **REPLICATED**, lo que significa que los mismos datos están presentes en todas las instancias del grupo de datos. |
| Mejoras en la tabla externa | Las tablas externas de tipo origen de datos HADOOP ahora admiten la lectura de filas de hasta 1 MB. Ahora, las tablas externas (ODBC, bloque de almacenamiento, grupo de datos) admiten filas tan anchas como las tablas de SQL Server. |

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes describen los problemas conocidos y limitaciones con esta versión.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio devuelve un error al intentar crear una nueva carpeta en HDFS. Para habilitar esta funcionalidad, instale la compilación de Insider de Azure Data Studio:
  
   - [Instalador de usuario de Windows - **compilación de Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Instalador de sistema de Windows - **compilación de Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP - **compilación de Insider**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP - **compilación de Insider**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR. GZ - **compilación de Insider**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Si hace clic derecho en un archivo de HDFS para obtener la vista previa, puede aparecer el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos mayores de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración HDFS que implican cambios en hdfs-site.xml.

#### <a name="deployment"></a>Implementación

- No se admiten los procedimientos de implementación anteriores para los clústeres grandes de datos habilitadas para GPU en CTP 3.0. Se está investigando un procedimiento de implementación alternativo. Por ahora, el artículo "Implementar un big data con compatibilidad con GPU de clúster y ejecutar TensorFlow" ha sido temporalmente no publicado para evitar confusiones.

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior.

   > [!IMPORTANT]
   > Debe los datos de copia de seguridad y, a continuación, eliminar el clúster existente de datos de gran tamaño (con la versión anterior de **mssqlctl**) antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- Implementación del clúster de macrodatos ya no crea el **SqlDataPool** y **SqlStoragePool** orígenes de datos externos. Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos para el grupo de datos y el grupo de almacenamiento.

   > [!NOTE]
   > El URI para la creación de estos orígenes de datos externo es diferente entre las versiones de CTP. Consulte los siguientes comandos de Transact-SQL para ver cómo crearlas 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc:8080/default');
   ```

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que usan tipos de datos de caracteres, el Asistente para la virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de tabla externa. Esto provocará un error en el DDL de tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2, o crear manualmente las instrucciones de la tabla externa y especificar NVARCHAR en lugar de usar al asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Al llamar a una aplicación de R, Python o MLeap desde la API de REST, la llamada a veces horizontal en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y cuadernos

- Pueden cambiar las direcciones IP de POD en el entorno de Kubernetes como reinicios de PODs. En el escenario donde se reinicia el patrón de pod, puede producir un error de la sesión de Spark con `NoRoteToHostException`. Esto se produce por las cachés JVM que no se actualiza con la nueva dirección IP direcciones.

- Si tiene Jupyter ya instalado y un independiente de Python en Windows, se pueden producir un error en cuadernos de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un bloc de notas, si hace clic en el **agregar texto** comando, se agrega el texto de la celda en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para activar o desactivar para el modo de edición y editar la celda.

#### <a name="security"></a>Seguridad

- El contraseña_sa forma parte del entorno y reconocibles (por ejemplo, en un archivo de volcado de cable). Debe restablecer el contraseña_sa en la instancia principal después de la implementación. Esto no es un error, pero un paso de seguridad. Para obtener más información sobre cómo cambiar el contraseña_sa en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros AKS pueden contener la contraseña de SA para las implementaciones de clústeres de datos de gran tamaño.

## <a id="ctp25"></a> CTP 2.5 (abril)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de macrodatos en 2.5 de CTP de SQL Server de 2019.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| Perfiles de implementación | Utiliza los [archivos JSON de configuración de la implementación](deployment-guidance.md#configfile) predeterminados y personalizados para las implementaciones de clústeres de macrodatos en lugar de las variables de entorno. |
| Implementaciones solicitadas | `mssqlctl cluster create` ahora le pide los valores necesarios para realizar implementaciones predeterminadas. |
| Cambios de nombre de punto de conexión de servicio y pod | Los puntos de conexión externos siguientes han cambiado los nombres:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| Mejoras de **mssqlctl** | Use **mssqlctl** para [enumerar los puntos de conexión externos](deployment-guidance.md#endpoints) y compruebe la versión de **mssqlctl** con el parámetro `--version`. |
| Instalación sin conexión | Guía para las implementaciones de clústeres de datos de gran tamaño sin conexión. |
| Mejoras en los niveles de HDFS | Los niveles S3, el almacenamiento en caché de montaje y OAuth compatibilidad con ADLS Gen2. |
| Nuevo `mssql` conector de Spark SQL Server | |

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes describen los problemas conocidos y limitaciones con esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior.

   > [!IMPORTANT]
   > Debe los datos de copia de seguridad y, a continuación, eliminar el clúster existente de datos de gran tamaño (con la versión anterior de **mssqlctl**) antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- Implementación del clúster de macrodatos ya no crea el **SqlDataPool** y **SqlStoragePool** orígenes de datos externos. Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos para el grupo de datos y el grupo de almacenamiento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que usan tipos de datos de caracteres, el Asistente para la virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de tabla externa. Esto provocará un error en el DDL de tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2, o crear manualmente las instrucciones de la tabla externa y especificar NVARCHAR en lugar de usar al asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Al llamar a una aplicación de R, Python o MLeap desde la API de REST, la llamada a veces horizontal en 5 minutos.

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

## <a id="ctp24"></a> CTP 2.4 (marzo)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.4.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| Orientación sobre la compatibilidad de GPU para la ejecución de aprendizaje profundo con TensorFlow en Spark. | [Implementa un clúster de macrodatos con compatibilidad con GPU y ejecuta TensorFlow](spark-gpu-tensorflow.md). |
| Los orígenes de datos **SqlDataPool** y **SqlStoragePool** ya no se crean de forma predeterminada. | Puede crearlos manualmente según sea necesario. Consulte los [problemas conocidos](#externaltablesctp24). |
| Compatibilidad de `INSERT INTO SELECT` con el grupo de datos. | Para obtener un ejemplo, vea [Tutorial: Introducir datos en un grupo de datos de SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md). |
| Opción `FORCE SCALEOUTEXECUTION` y `DISABLE SCALEOUTEXECUTION`. | Fuerza o deshabilita el uso de la agrupación de proceso para las consultas en las tablas externas. Por ejemplo, `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Recomendaciones actualizadas para implementar AKS. | Al evaluar los clústeres de macrodatos en AKS, ahora se recomienda utilizar un único nodo del tamaño **Standard_L8s**. |
| Actualización del entorno de ejecución de Spark a Spark 2.4. | |

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes describen los problemas conocidos y limitaciones con esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior.

   > [!IMPORTANT]
   > Debe los datos de copia de seguridad y, a continuación, eliminar el clúster existente de datos de gran tamaño (con la versión anterior de **mssqlctl**) antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="kubeadm-deployments"></a>implementaciones de kubeadm

Si usa kubeadm para implementación de Kubernetes en varios equipos, el portal de administración de clúster no mostrar correctamente los puntos de conexión necesarias para conectarse al clúster de macrodatos. Si experimenta este problema, utilice la siguiente solución alternativa para conocer las direcciones IP de punto de conexión de servicio:

- Si se conecta desde dentro del clúster, consultar Kubernetes para la dirección IP de servicio para el punto de conexión que desea conectarse. Por ejemplo, la siguiente **kubectl** comando muestra la dirección IP de la instancia principal de SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Si se conecta desde fuera del clúster, use los pasos siguientes para conectarse:

   1. Obtenga la dirección IP del nodo que ejecuta la instancia principal de SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conéctese a la instancia principal de SQL Server con esta dirección IP.

   1. Consulta el **cluster_endpoint_table** en la base de datos maestra para otros puntos de conexión externos.

      Si se produce un error con un tiempo de espera de conexión, es posible que el nodo respectivo atraviesa el firewall. En este caso, debe ponerse en contacto con el Administrador de clústeres de Kubernetes y solicitar la dirección IP del nodo que se expone externamente. Podría tratarse de cualquier nodo. A continuación, puede utilizar esa dirección IP y el puerto correspondiente para conectarse a diversos servicios que se ejecutan en el clúster. Por ejemplo, el administrador puede encontrar esta dirección IP mediante la ejecución:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Eliminar clúster produce un error

Cuando se intenta eliminar un clúster con **mssqlctl**, se produce un error con el siguiente error:

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

Un nuevo cliente de Python Kubernetes (versión 9.0.0) puede cambiar los espacios de nombres de eliminación API, lo que interrumpe actualmente **mssqlctl**. Esto sólo ocurre si tiene instalado un cliente de python de Kubernetes más reciente. Puede solucionar este problema mediante la eliminación directamente el clúster con **kubectl** (`kubectl delete ns <ClusterName>`), o puede instalar la versión anterior mediante `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a> Tablas externas

- Implementación del clúster de macrodatos ya no crea el **SqlDataPool** y **SqlStoragePool** orígenes de datos externos. Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos para el grupo de datos y el grupo de almacenamiento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que usan tipos de datos de caracteres, el Asistente para la virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de tabla externa. Esto provocará un error en el DDL de tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2, o crear manualmente las instrucciones de la tabla externa y especificar NVARCHAR en lugar de usar al asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Al llamar a una aplicación de R, Python o MLeap desde la API de REST, la llamada a veces horizontal en 5 minutos.

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

## <a id="ctp23"></a> CTP 2.3 (febrero)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.3.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
| :---------- | :------ |
| Envío de trabajos de Spark en clústeres de macrodatos en IntelliJ. | [Envío de trabajos de Spark en clústeres de macrodatos de SQL Server en IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| CLI comunes para la implementación de la aplicación y la administración de clústeres. | [Cómo implementar una aplicación en un clúster de macrodatos de SQL Server 2019 (versión preliminar)](big-data-cluster-create-apps.md) |
| Extensión de VS Code para implementar aplicaciones en un clúster de macrodatos. | [Cómo utilizar VS Code para implementar aplicaciones en clústeres de macrodatos de SQL Server](app-deployment-extension.md) |
| Cambios en el uso del comando de la herramienta **mssqlctl**. | Para obtener más información, vea los [problemas conocidos con mssqlctl](#mssqlctlctp23). |
| Usar Sparklyr en clúster de macrodatos | [Uso de Sparklyr en clústeres de macrodatos de SQL Server 2019](sparklyr-from-RStudio.md) |
| Montaje de almacenamiento externo compatible con HDFS en clústeres de macrodatos con **niveles de HDFS**. | Vea [Niveles de HDFS](hdfs-tiering.md). |
| Nueva experiencia de conexión unificada para la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS. | Consulte la [instancia principal de SQL Server y la puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md). |
| Al eliminar un clúster con la función **eliminar clúster mssqlctl** ahora solo se eliminan los objetos en el espacio de nombres que formaban parte del clúster de macrodatos. | El espacio de nombres no se elimina. Sin embargo, en versiones anteriores, este comando sí que eliminaba todo el espacio de nombres. |
| Los nombres de punto de conexión de _seguridad_ se han cambiado y consolidado. | **service-security-lb** y **service-security-nodeport** se han consolidado en el punto de conexión **endpoint-security**. |
| Los nombres de punto de conexión de _proxy_ se han cambiado y consolidado. | **service-proxy-lb** y **service-proxy-nodeport** se han consolidado en el punto de conexión **endpoint-sevice-proxy**. |
| Los nombres de punto de conexión de _controller_ se han cambiado y consolidado. | **service-mssql-controller-lb** y **service-mssql-controller-nodeport** se han consolidado en el punto de conexión **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes describen los problemas conocidos y limitaciones con esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior.

   > [!IMPORTANT]
   > Debe los datos de copia de seguridad y, a continuación, eliminar el clúster existente de datos de gran tamaño (con la versión anterior de **mssqlctl**) antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

- El **ACCEPT_EULA** variable de entorno debe ser "yes" o "Sí" para aceptar los términos de licencia. Las versiones anteriores permiten "y" e "Y", pero estos ya no se aceptan y producirá un error de implementación.

- El **CLUSTER_PLATFORM** variables de entorno no tiene valor predeterminado es igual que en versiones anteriores.

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="kubeadm-deployments"></a>implementaciones de kubeadm

Si usa kubeadm para implementación de Kubernetes en varios equipos, el portal de administración de clúster no mostrar correctamente los puntos de conexión necesarias para conectarse al clúster de macrodatos. Si experimenta este problema, utilice la siguiente solución alternativa para conocer las direcciones IP de punto de conexión de servicio:

- Si se conecta desde dentro del clúster, consultar Kubernetes para la dirección IP de servicio para el punto de conexión que desea conectarse. Por ejemplo, la siguiente **kubectl** comando muestra la dirección IP de la instancia principal de SQL Server:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Si se conecta desde fuera del clúster, use los pasos siguientes para conectarse:

   1. Obtenga la dirección IP del nodo que ejecuta la instancia principal de SQL Server: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Conéctese a la instancia principal de SQL Server con esta dirección IP.

   1. Consulta el **cluster_endpoint_table** en la base de datos maestra para otros puntos de conexión externos.

      Si se produce un error con un tiempo de espera de conexión, es posible que el nodo respectivo atraviesa el firewall. En este caso, debe ponerse en contacto con el Administrador de clústeres de Kubernetes y solicitar la dirección IP del nodo que se expone externamente. Podría tratarse de cualquier nodo. A continuación, puede utilizar esa dirección IP y el puerto correspondiente para conectarse a diversos servicios que se ejecutan en el clúster. Por ejemplo, el administrador puede encontrar esta dirección IP mediante la ejecución:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="mssqlctlctp23"></a> mssqlctl

- El **mssqlctl** herramienta cambió de un comando verbo-nombre pedidos a un pedido de nombre-verbo. Por ejemplo, `mssqlctl create cluster` es ahora `mssqlctl cluster create`.

- El `--name` parámetro ahora es necesario al crear un clúster con `mssqlctl cluster create`.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- Para obtener información importante sobre cómo actualizar a la versión más reciente de los clústeres de macrodatos y **mssqlctl**, consulte [actualizar a una nueva versión](deployment-upgrade.md).

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que usan tipos de datos de caracteres, el Asistente para la virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de tabla externa. Esto provocará un error en el DDL de tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2, o crear manualmente las instrucciones de la tabla externa y especificar NVARCHAR en lugar de usar al asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Al llamar a una aplicación de R, Python o MLeap desde la API de REST, la llamada a veces horizontal en 5 minutos.

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

## <a id="ctp22"></a> CTP 2.2 (diciembre de 2018)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.2.

### <a name="new-features"></a>Nuevas características

- Portal de administración de clúster que se accede con `/portal` (**https://\<ip-address\>: 30777/portal**).
- Nombre del grupo principal de servicio cambió de `service-master-pool-lb` y `service-master-pool-nodeport` a `endpoint-master-pool`.
- Nueva versión de **mssqlctl** y actualiza las imágenes.
- Mejoras y correcciones de errores.

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes describen los problemas conocidos y limitaciones con esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior. Debe de copia de seguridad y eliminar cualquier clúster de macrodatos existente antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="cluster-administration-portal"></a>Portal de administración de clústeres

El portal de administración de clúster no muestra el punto de conexión para la instancia principal de SQL Server. Para encontrar la dirección IP y puerto de la instancia maestra, use el siguiente **kubectl** comando:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

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

## <a id="ctp21"></a> CTP 2.1 (noviembre de 2018)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.1.

### <a name="new-features"></a>Nuevas características

- [Implementar aplicaciones de Python y R](big-data-cluster-create-apps.md) en un clúster de macrodatos.
- Nueva versión de **mssqlctl** y actualiza las imágenes. 
- Mejoras y correcciones de errores.

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes proporcionan los problemas conocidos para los clústeres de macrodatos de SQL Server en CTP 2.1.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior. Debe de copia de seguridad y eliminar cualquier clúster de macrodatos existente antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-upgrade.md).

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

### <a name="new-features"></a>Nuevas características

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
