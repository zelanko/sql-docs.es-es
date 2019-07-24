---
title: Notas de la versión
titleSuffix: SQL Server big data clusters
description: En este artículo se describen las actualizaciones más recientes y los problemas conocidos de los clústeres de macrodatos de SQL Server 2019 (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0dd96d4a3227fda76921764429b4566e3e5dd28
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419297"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Notas de la versión de los clústeres de Big Data en SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se enumeran las actualizaciones y los problemas conocidos de las versiones más recientes de los clústeres de macrodatos de SQL Server.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp32"></a>CTP 3,2 (julio)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 3,2.

|Nueva característica o actualización | Detalles |
|:---|:---|
|Versión preliminar pública |Antes de la versión CTP 3,2, SQL Server clúster de Big Data estaba disponible para los pioneros registrados. Esta versión permite a todo el mundo experimentar las características de SQL Server los clústeres de macrodatos. <br/><br/> Consulte Introducción [a los clústeres de macrodatos de SQL Server](deploy-get-started.md).|
|`azdata` |CTP 3,2 presenta `azdata` una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de Big Data a través de las API de REST. `azdata`reemplaza `mssqlctl`a. Vea [install `azdata`(instalar ](deploy-install-azdata.md)). |
|PolyBase |Los nombres de las columnas de tabla externa ahora se usan para consultar orígenes de datos de SQL Server, Oracle, Teradata, MongoDB y ODBC. |
|Actualización de niveles de HDFS |Introducción a la funcionalidad de actualización de la organización en niveles de HDFS para que se pueda actualizar un montaje existente para la instantánea más reciente de los datos remotos. Vea [niveles de HDFS](hdfs-tiering.md) |
|Solución de problemas basada en Notebook |CTP 3,2 presenta cuadernos de Jupyter para ayudar a [implementar](deploy-notebooks.md) y [detectar, diagnosticar y solucionar problemas](manage-notebooks.md) de componentes en un clúster de macrodatos de SQL Server. |
| &nbsp; | &nbsp; |

## <a id="ctp31"></a>CTP 3,1 (junio)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 3,1.

|Nueva característica o actualización | Detalles |
|:---|:---|
|Versión preliminar pública |Antes de la versión CTP 3,2, SQL Server clúster de Big Data estaba disponible para los pioneros registrados. Esta versión permite a todo el mundo experimentar las características de SQL Server los clústeres de macrodatos. <br/><br/> Consulte Introducción [a los clústeres de macrodatos de SQL Server](deploy-get-started.md).|
|Solución de problemas basada en Notebook.|CTP 3,2 presenta cuadernos de Jupyter para ayudar con la [implementación](deploy-notebooks.md)y [detección, diagnóstico y solución de problemas](manage-notebooks.md) de los componentes de un clúster de macrodatos SQL Server. |
|`azdata` |CTP 3,2 presenta `azdata` una utilidad de línea de comandos escrita en Python que permite a los administradores de clústeres arrancar y administrar el clúster de Big Data a través de las API de REST. `azdata`reemplaza `mssqlctl`a. Vea [install `azdata`(instalar ](deploy-install-azdata.md)). |
|Actualización de niveles de HDFS |Introducción a la funcionalidad de actualización de la organización en niveles de HDFS para que se pueda actualizar un montaje existente para la instantánea más reciente de los datos remotos. Vea [niveles de HDFS](hdfs-tiering.md) |
| &nbsp; | &nbsp; |

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| Cambios del comando `mssqlctl` | Los comandos `mssqlctl cluster` se llaman ahora `mssqlctl bdc`. Para más información, consulte la referencia de [`mssqlctl`](reference-azdata.md). |
| Nuevos `mssqlctl` comandos de estado y eliminación del portal de administración de clústeres. | En esta versión se quita el portal de administración de clústeres. Se han agregado nuevos comandos de estado `mssqlctl` a que complementan los comandos de supervisión existentes. |
| Grupos de procesos de Spark | Cree nodos adicionales para aumentar la capacidad de proceso de Spark sin tener que escalar verticalmente el almacenamiento. Además, puede iniciar los nodos del grupo de almacenamiento que no se usan con Spark. Spark y el almacenamiento están desacoplados. Para más información, consulte [Configurar el almacenamiento sin spark](deployment-custom-configuration.md#sparkstorage). |
| Conector de Spark MSSQL | Compatibilidad con operaciones de lectura y escritura en tablas externas del grupo de datos. Las versiones anteriores solo admitían operaciones de lectura y escritura en tablas de instancias maestras. Para más información, consulte [Cómo leer y escribir en SQL Server de Spark mediante el conector de Spark MSSQL](spark-mssql-connector.md). |
| Machine Learning con MLeap | [Entrenar un modelo de aprendizaje automático MLeap en Spark y puntuarlo en SQL Server con la extensión del lenguaje Java](spark-create-machine-learning-model.md). |

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior.

   > [!IMPORTANT]
   > Debe hacer una copia de seguridad de los datos y, a continuación, eliminar el clúster de Big Data existente (con la versión anterior de **azdata**) antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- La implementación del clúster de Big Data ya no crea los orígenes de datos externos **SqlDataPool** y **SqlStoragePool** . Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos en el grupo de datos y en el bloque de almacenamiento.

   > [!NOTE]
   > El URI para crear estos orígenes de datos externos es diferente entre CTP. Consulte los siguientes comandos de Transact-SQL para ver cómo crearlos. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que utilice tipos de datos de caracteres, el Asistente para virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de la tabla externa. Esto producirá un error en el DDL de la tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2 o cree manualmente instrucciones de tabla externa y especifique NVARCHAR en lugar de usar el asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Cuando se llama a una aplicación de R, Python o MLeap desde la API de RESTful, se agota el tiempo de espera de la llamada en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

#### <a name="kibana-logs-dashboards"></a>Paneles de registros de Kibana

- Entre las versiones derivadas de CTP 3,0 y 3,1, la versión de Kibana se actualizó de 6.3.1 a 7.0.1.  Esto ha hecho que el explorador de Edge no sea compatible con Kibana. Los usuarios verán una página en blanco al cargar la versión actual de los paneles de Kibana en Edge. Consulte [aquí]( https://www.elastic.co/support/matrix#matrix_browse) para ver los exploradores compatibles con Kibana.RS 


## <a id="ctp30"></a>CTP 3,0 (mayo)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 3,0.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| **mssqlctl** updates | Varias [actualizaciones de comandos y parámetros](reference-azdata.md) de **mssqlctl**. Esto incluye una actualización del comando **mssqlctl login**, que ahora se dirige al punto de conexión y al nombre de usuario del controlador. |
| Mejoras en el almacenamiento | Compatibilidad con distintas configuraciones de almacenamiento para registros y datos. Además, se ha reducido el número de notificaciones de volumen persistentes para un clúster de macrodatos. |
| Varias instancias de grupos de procesos | Compatibilidad con varias instancias de grupos de procesos. |
| Nuevas características y nuevo comportamiento del grupo | Ahora, el grupo de procesos se utiliza de forma predeterminada para las operaciones de grupo de almacenamiento y grupo de datos solo en distribución **ROUND_ROBIN**. Ahora, el grupo de datos puede utilizar un nuevo tipo de distribución, **REPLICATED**, lo que significa que los mismos datos están presentes en todas las instancias del grupo de datos. |
| Mejoras en la tabla externa | Las tablas externas de tipo origen de datos HADOOP ahora admiten la lectura de filas de hasta 1 MB. Ahora, las tablas externas (ODBC, bloque de almacenamiento, grupo de datos) admiten filas tan anchas como las tablas de SQL Server. |

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="hdfs"></a>HDFS

- Azure Data Studio devuelve un error al intentar crear una nueva carpeta en HDFS. Para habilitar esta funcionalidad, instale la compilación Insider de Azure Data Studio:
  
   - [Instalador de usuarios de Windows- **compilación** de Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Instalador de sistema de Windows- **compilación** de Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Compilaciones  de Windows zip-Insider](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [compilar  zip de MacOS-Insider](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [TAR de Linux GZ: **compilación** de Insider](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="deployment"></a>Implementación

- Los procedimientos de implementación anteriores para los clústeres de macrodatos habilitados para GPU no se admiten en CTP 3,0. Se está investigando un procedimiento de implementación alternativo. Por ahora, el artículo "implementar un clúster de Big Data con compatibilidad con GPU y ejecutar TensorFlow" se ha anulado temporalmente la publicación para evitar confusiones.

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior.

   > [!IMPORTANT]
   > Debe hacer una copia de seguridad de los datos y, a continuación, eliminar el clúster de Big Data existente (con la versión anterior de **azdata**) antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- La implementación del clúster de Big Data ya no crea los orígenes de datos externos **SqlDataPool** y **SqlStoragePool** . Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos en el grupo de datos y en el bloque de almacenamiento.

   > [!NOTE]
   > El URI para crear estos orígenes de datos externos es diferente entre CTP. Consulte los siguientes comandos de Transact-SQL para ver cómo crearlos. 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que utilice tipos de datos de caracteres, el Asistente para virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de la tabla externa. Esto producirá un error en el DDL de la tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2 o cree manualmente instrucciones de tabla externa y especifique NVARCHAR en lugar de usar el asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Cuando se llama a una aplicación de R, Python o MLeap desde la API de RESTful, se agota el tiempo de espera de la llamada en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp25"></a>CTP 2,5 (abril)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,5.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| Perfiles de implementación | Utiliza los [archivos JSON de configuración de la implementación](deployment-guidance.md#configfile) predeterminados y personalizados para las implementaciones de clústeres de macrodatos en lugar de las variables de entorno. |
| Implementaciones solicitadas | `azdata cluster create` ahora le pide los valores necesarios para realizar implementaciones predeterminadas. |
| Cambios de nombre de punto de conexión de servicio y pod | Los siguientes puntos de conexión externos han cambiado de nombre:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **extremo-servicio-Proxy** => **mgmtproxy-SVC-externo**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| mejoras de **azdata** | Use **azdata** para [enumerar los puntos de conexión externos](deployment-guidance.md#endpoints) y comprobar la versión de `--version` **azdata** con el parámetro. |
| Instalación sin conexión | Instrucciones para las implementaciones de clúster de Big Data sin conexión. |
| Mejoras en los niveles de HDFS | Niveles S3, almacenamiento en caché de montaje y compatibilidad con OAuth para ADLS Gen2. |
| Nuevo `mssql` conector de Spark-SQL Server | |

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior.

   > [!IMPORTANT]
   > Debe hacer una copia de seguridad de los datos y, a continuación, eliminar el clúster de Big Data existente (con la versión anterior de **azdata**) antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- La implementación del clúster de Big Data ya no crea los orígenes de datos externos **SqlDataPool** y **SqlStoragePool** . Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos en el grupo de datos y en el bloque de almacenamiento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que utilice tipos de datos de caracteres, el Asistente para virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de la tabla externa. Esto producirá un error en el DDL de la tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2 o cree manualmente instrucciones de tabla externa y especifique NVARCHAR en lugar de usar el asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Cuando se llama a una aplicación de R, Python o MLeap desde la API de RESTful, se agota el tiempo de espera de la llamada en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp24"></a>CTP 2,4 (marzo)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,4.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
|:---|:---|
| Orientación sobre la compatibilidad de GPU para la ejecución de aprendizaje profundo con TensorFlow en Spark. | [Implementa un clúster de macrodatos con compatibilidad con GPU y ejecuta TensorFlow](spark-gpu-tensorflow.md). |
| Los orígenes de datos **SqlDataPool** y **SqlStoragePool** ya no se crean de forma predeterminada. | Puede crearlos manualmente según sea necesario. Consulte los [problemas conocidos](#externaltablesctp24). |
| Compatibilidad de `INSERT INTO SELECT` con el grupo de datos. | Para obtener un ejemplo, vea [Tutorial: Introducir datos en un grupo de datos de SQL Server con Transact-SQL](tutorial-data-pool-ingest-sql.md). |
| Opción `FORCE SCALEOUTEXECUTION` y `DISABLE SCALEOUTEXECUTION`. | Fuerza o deshabilita el uso del grupo de proceso para las consultas en tablas externas. Por ejemplo: `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)`. |
| Recomendaciones actualizadas para implementar AKS. | Al evaluar los clústeres de macrodatos en AKS, ahora se recomienda utilizar un único nodo del tamaño **Standard_L8s**. |
| Actualización del entorno de ejecución de Spark a Spark 2.4. | |

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior.

   > [!IMPORTANT]
   > Debe hacer una copia de seguridad de los datos y, a continuación, eliminar el clúster de Big Data existente (con la versión anterior de **azdata**) antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="kubeadm-deployments"></a>implementaciones de kubeadm

Si usa kubeadm para implementar Kubernetes en varios equipos, el portal de administración de clústeres no muestra correctamente los puntos de conexión necesarios para conectarse al clúster de Big Data. Si experimenta este problema, use la siguiente solución alternativa para detectar las direcciones IP del punto de conexión de servicio:

- Si se va a conectar desde dentro del clúster, consulte Kubernetes para obtener la dirección IP del servicio del punto de conexión al que desea conectarse. Por ejemplo, el siguiente comando **kubectl** muestra la dirección IP del SQL Server instancia maestra:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Si se va a conectar desde fuera del clúster, siga estos pasos para conectarse:

   1. Obtiene la dirección IP del nodo que ejecuta la instancia maestra de SQL Server `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`:.

   1. Conéctese a SQL Server instancia maestra con esta dirección IP.

   1. Consulte **cluster_endpoint_table** en la base de datos maestra para buscar otros puntos de conexión externos.

      Si se produce un error de tiempo de espera de conexión, es posible que el nodo respectivo esté en el firewall. En este caso, debe ponerse en contacto con el administrador de clústeres de Kubernetes y solicitar la IP del nodo que se expone externamente. Puede ser cualquier nodo. Después, puede utilizar esa dirección IP y el puerto correspondiente para conectarse a varios servicios que se ejecutan en el clúster. Por ejemplo, el administrador puede encontrar esta dirección IP mediante la ejecución de:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>Error al eliminar el clúster

Cuando intenta eliminar un clúster con **azdata**, se produce el siguiente error:

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

Un nuevo cliente de Python Kubernetes (versión 9.0.0) cambió la API Delete namespaces, que actualmente interrumpe **azdata**. Esto solo ocurre si tiene un cliente de Kubernetes Python más reciente instalado. Para solucionar este problema, elimine directamente el clúster mediante **kubectl** (`kubectl delete ns <ClusterName>`), o bien puede instalar la versión anterior mediante `sudo pip install kubernetes==8.0.1`.

#### <a id="externaltablesctp24"></a>Tablas externas

- La implementación del clúster de Big Data ya no crea los orígenes de datos externos **SqlDataPool** y **SqlStoragePool** . Puede crear estos orígenes de datos manualmente para admitir la virtualización de datos en el grupo de datos y en el bloque de almacenamiento.

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que utilice tipos de datos de caracteres, el Asistente para virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de la tabla externa. Esto producirá un error en el DDL de la tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2 o cree manualmente instrucciones de tabla externa y especifique NVARCHAR en lugar de usar el asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Cuando se llama a una aplicación de R, Python o MLeap desde la API de RESTful, se agota el tiempo de espera de la llamada en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp23"></a>CTP 2,3 (febrero)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,3.

### <a name="whats-new"></a>What's New

| Nueva característica o actualización | Detalles |
| :---------- | :------ |
| Envío de trabajos de Spark en clústeres de macrodatos en IntelliJ. | [Envío de trabajos de Spark en clústeres de macrodatos de SQL Server en IntelliJ](spark-submit-job-intellij-tool-plugin.md) |
| CLI comunes para la implementación de la aplicación y la administración de clústeres. | [Cómo implementar una aplicación en un clúster de macrodatos de SQL Server 2019 (versión preliminar)](big-data-cluster-create-apps.md) |
| Extensión de VS Code para implementar aplicaciones en un clúster de macrodatos. | [Cómo utilizar VS Code para implementar aplicaciones en clústeres de macrodatos de SQL Server](app-deployment-extension.md) |
| Cambios en el uso del comando de la herramienta **azdata** . | Para obtener más información, consulte los [problemas conocidos de azdata](#azdatactp23). |
| Uso de Sparklyr en un clúster de Big Data | [Uso de Sparklyr en clústeres de macrodatos de SQL Server 2019](sparklyr-from-RStudio.md) |
| Montaje de almacenamiento externo compatible con HDFS en clústeres de macrodatos con **niveles de HDFS**. | Vea [Niveles de HDFS](hdfs-tiering.md). |
| Nueva experiencia de conexión unificada para la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS. | Consulte la [instancia principal de SQL Server y la puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md). |
| Al eliminar un clúster con el **clúster de azdata Delete** , ahora solo se eliminan los objetos del espacio de nombres que formaban parte del clúster de Big Data. | El espacio de nombres no se elimina. Sin embargo, en versiones anteriores, este comando sí que eliminaba todo el espacio de nombres. |
| Los nombres de punto de conexión de _seguridad_ se han cambiado y consolidado. | **service-security-lb** y **service-security-nodeport** se han consolidado en el punto de conexión **endpoint-security**. |
| Los nombres de punto de conexión de _proxy_ se han cambiado y consolidado. | **service-proxy-lb** y **service-proxy-nodeport** se han consolidado en el punto de conexión **endpoint-sevice-proxy**. |
| Los nombres de punto de conexión de _controller_ se han cambiado y consolidado. | **service-mssql-controller-lb** y **service-mssql-controller-nodeport** se han consolidado en el punto de conexión **endpoint-controller**. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior.

   > [!IMPORTANT]
   > Debe hacer una copia de seguridad de los datos y, a continuación, eliminar el clúster de Big Data existente (con la versión anterior de **azdata**) antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- La variable de entorno **ACCEPT_EULA** debe ser "Yes" o "Yes" para aceptar el CLUF. Las versiones anteriores permitían "y" y "Y", pero ya no se aceptan y provocarán un error en la implementación.

- Las variables de entorno **CLUSTER_PLATFORM** no tienen un valor predeterminado, como en versiones anteriores.

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="kubeadm-deployments"></a>implementaciones de kubeadm

Si usa kubeadm para implementar Kubernetes en varios equipos, el portal de administración de clústeres no muestra correctamente los puntos de conexión necesarios para conectarse al clúster de Big Data. Si experimenta este problema, use la siguiente solución alternativa para detectar las direcciones IP del punto de conexión de servicio:

- Si se va a conectar desde dentro del clúster, consulte Kubernetes para obtener la dirección IP del servicio del punto de conexión al que desea conectarse. Por ejemplo, el siguiente comando **kubectl** muestra la dirección IP del SQL Server instancia maestra:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- Si se va a conectar desde fuera del clúster, siga estos pasos para conectarse:

   1. Obtiene la dirección IP del nodo que ejecuta la instancia maestra de SQL Server `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`:.

   1. Conéctese a SQL Server instancia maestra con esta dirección IP.

   1. Consulte **cluster_endpoint_table** en la base de datos maestra para buscar otros puntos de conexión externos.

      Si se produce un error de tiempo de espera de conexión, es posible que el nodo respectivo esté en el firewall. En este caso, debe ponerse en contacto con el administrador de clústeres de Kubernetes y solicitar la IP del nodo que se expone externamente. Puede ser cualquier nodo. Después, puede utilizar esa dirección IP y el puerto correspondiente para conectarse a varios servicios que se ejecutan en el clúster. Por ejemplo, el administrador puede encontrar esta dirección IP mediante la ejecución de:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a>azdata

- La herramienta **azdata** ha cambiado de un orden de comandos verbo-Sustantivo a un orden Sustantivo. Por ejemplo, `azdata create cluster` ahora `azdata cluster create`es.

- Ahora `--name` es necesario el parámetro al crear un clúster con `azdata cluster create`.

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- Para obtener información importante sobre la actualización a la versión más reciente de los clústeres de macrodatos y **azdata**, consulte [actualización a una nueva versión](deployment-upgrade.md).

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que utilice tipos de datos de caracteres, el Asistente para virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de la tabla externa. Esto producirá un error en el DDL de la tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2 o cree manualmente instrucciones de tabla externa y especifique NVARCHAR en lugar de usar el asistente.

#### <a name="application-deployment"></a>Implementación de la aplicación

- Cuando se llama a una aplicación de R, Python o MLeap desde la API de RESTful, se agota el tiempo de espera de la llamada en 5 minutos.

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp22"></a>CTP 2,2 (2018 de diciembre)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,2.

### <a name="new-features"></a>Nuevas características

- Portal de administración de clúster al `/portal` que se accede con ( **\<https://IP-address\>: 30777/portal**).
- El nombre del servicio del grupo `service-master-pool-lb` maestro `service-master-pool-nodeport` ha `endpoint-master-pool`cambiado de y a.
- Nueva versión de **azdata** e imágenes actualizadas.
- Correcciones de errores y mejoras varias.

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos y las limitaciones de esta versión.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior. Debe hacer una copia de seguridad y eliminar cualquier clúster de Big Data existente antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="cluster-administration-portal"></a>Portal de administración de clústeres

El portal de administración de clústeres no muestra el extremo de la instancia maestra de SQL Server. Para buscar la dirección IP y el puerto de la instancia maestra, use el siguiente comando de **kubectl** :

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp21"></a>CTP 2,1 (2018 de noviembre)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,1.

### <a name="new-features"></a>Nuevas características

- [Implemente aplicaciones de Python y R](big-data-cluster-create-apps.md) en un clúster de Big Data.
- Nueva versión de **azdata** e imágenes actualizadas. 
- Correcciones de errores y mejoras varias.

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se proporcionan problemas conocidos de los clústeres de macrodatos de SQL Server en CTP 2,1.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de datos de Big Data desde una versión anterior. Debe hacer una copia de seguridad y eliminar cualquier clúster de Big Data existente antes de implementar la versión más reciente. Para obtener más información, vea [actualizar a una nueva versión](deployment-upgrade.md).

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="admin-portal"></a>Portal de administración

- Cuando se [crea una aplicación con el comando msqlctl-CTP](big-data-cluster-create-apps.md) y se implementa en un clúster de macrodatos SQL Server, el portal de administración de clústeres muestra los pods en los que la aplicación se implementó como "desconocido" en la sección de controlador de la parte de administración.

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a id="ctp20"></a>CTP 2,0 (2018 de octubre)

En las secciones siguientes se describen las nuevas características y los problemas conocidos de los clústeres de Big Data en SQL Server 2019 CTP 2,0.

### <a name="new-features"></a>Nuevas características

- Experiencia de implementación sencilla con la herramienta de administración de azdata
- Experiencia nativa de Notebook en Azure Data Studio
- Consultar archivos HDFS a través de la instancia de almacenamiento de SQL Server
- Virtualización de datos a través de Master a SQL Server, Oracle, MongoDB y HDFS
- Asistente para la virtualización de datos para SQL Server y Oracle en Azure Data Studio
- ML Services en Master
- Portal de administración de clústeres que puede usar para la supervisión y solución de problemas
- Envío del trabajo de Spark en Azure Data Studio 
- Interfaz de usuario de Spark en el portal de administración de clústeres
- Montaje de volúmenes en clases de almacenamiento
- Consultas en grupos de datos de la maestra
- Mostrar el plan de consultas distribuidas en SSMS
- Paquete PIP para la herramienta de administración de azdata
- Motor de implementación integrado a través del servicio de controlador

### <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se proporcionan problemas conocidos de los clústeres de macrodatos de SQL Server en CTP 2,0.

#### <a name="deployment"></a>Implementación

- Si usa Azure Kubernetes Service (AKS), la versión recomendada de Kubernetes es 1,10. *, que no admite el cambio de tamaño del disco. Debe asegurarse de que está cambiando el tamaño del almacenamiento en consecuencia en el momento de la implementación. Para obtener más información sobre cómo ajustar los tamaños de almacenamiento, consulte el artículo sobre [persistencia de datos](concept-data-persistence.md) . En el caso de Kubernetes implementado en máquinas virtuales, la versión recomendada es 1,11.

- Después de la implementación en AKS, es posible que vea los dos eventos de advertencia siguientes de la implementación. Ambos eventos son problemas conocidos, pero no impiden implementar correctamente el clúster de Big Data en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de Big Data, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución alternativa consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="external-tables"></a>Tablas externas

- Es posible crear una tabla externa del grupo de datos para una tabla que tenga tipos de columna no admitidos. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del bloque de almacenamiento, podría recibir un error si el archivo subyacente se copia en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark y notebooks

- Las direcciones IP de POD pueden cambiar en el entorno de Kubernetes a medida que los PODs se reinician. En el escenario en el que se reinicia Master-Pod, se puede producir un error `NoRoteToHostException`en la sesión de Spark. Esto se debe a que las memorias caché de JVM no se actualizan con nuevas direcciones IP.

- Si ya tiene Jupyter instalado y otro Python en Windows, es posible que se produzca un error en los blocs de notas de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un cuaderno, si hace clic en el comando **Agregar texto** , la celda de texto se agrega en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para cambiar al modo de edición y editar la celda.

#### <a name="hdfs"></a>HDFS

- Si hace clic con el botón derecho en un archivo de HDFS para obtener una vista previa, es posible que vea el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos de más de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración de HDFS que impliquen cambios en HDFS-site. Xml.

#### <a name="security"></a>Seguridad

- SA_PASSWORD forma parte del entorno y es reconocible (por ejemplo, en un archivo de volcado de cable). Debe restablecer el SA_PASSWORD en la instancia maestra después de la implementación. Esto no es un error, sino un paso de seguridad. Para obtener más información sobre cómo cambiar SA_PASSWORD en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros de AKS pueden contener la contraseña de SA para implementaciones de clúster de Big Data.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los clústeres de macrodatos de SQL Server, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
