---
title: Notas de la versión
titleSuffix: SQL Server 2019 big data clusters
description: En este artículo se describe las últimas actualizaciones y problemas conocidos de clústeres de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 4c178c5868789bec2dc80a4b68558f12afbc90d2
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2019
ms.locfileid: "58073231"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>Notas de la versión para los clústeres de datos de gran tamaño en SQL Server

En este artículo se enumeran las actualizaciones y saber que los problemas de las versiones más recientes de los clústeres de macrodatos de SQL Server.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp23"></a> CTP 2.3 (2019 SQL)

Febrero de 2019 &nbsp; &nbsp;  /  &nbsp; &nbsp; SQL Server 2019 &nbsp; &nbsp;  /  &nbsp; &nbsp; CTP2.3

### <a name="new-features"></a>Nuevas características

| Nueva característica | Detalles |
| :---------- | :------ |
| [Enviar trabajos de Spark en clústeres SQL Server de datos grande en IntelliJ](spark-submit-job-intellij-tool-plugin.md). | &nbsp; |
| [CLI comunes para la administración de clúster y la implementación de aplicación](big-data-cluster-create-apps.md). | &nbsp; |
| [Extensión de VS Code para implementar aplicaciones en clústeres de SQL Server macrodatos](app-deployment-extension.md). | &nbsp; |
| [Cambia a la **mssqlctl** herramienta de uso del comando](#mssqlctlctp23). | &nbsp; |
| [Usar Sparklyr en clúster de SQL Server 2019 Big data](sparklyr-from-RStudio.md). | &nbsp; |
| Monte almacenamiento compatible con HDFS externo en el clúster de macrodatos con **HDFS niveles**. | Consulte [HDFS niveles](hdfs-tiering.md). |
| Nueva experiencia de conexión unificado para la instancia principal de SQL Server y la puerta de enlace de Spark o HDFS. | Consulte [instancia principal de SQL Server y la puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md). |
| Al eliminar un clúster con **mssqlctl clúster delete** ahora elimina sólo los objetos en el espacio de nombres que formaban parte del clúster de macrodatos. | No se elimina el espacio de nombres. Sin embargo, en versiones anteriores, este comando elimina todo el espacio de nombres. |
| _Seguridad_ se han cambiado los nombres de extremo y consolidados. | _Puntos de conexión anteriores:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-security-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **servicio-seguridad-nodeport**<br/><br/>_Nuevo punto de conexión:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-security** |
| _Proxy_ se han cambiado los nombres de extremo y consolidados. | _Puntos de conexión anteriores:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-proxy-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-proxy-nodeport**<br/><br/>_Nuevo punto de conexión:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-service-proxy** |
| _Controlador_ se han cambiado los nombres de extremo y consolidados. | _Puntos de conexión anteriores:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-mssql-controller-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-mssql-controller-nodeport**<br/><br/>_Nuevo punto de conexión:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-controller** |
| &nbsp; | &nbsp; |

### <a name="known-issues-deployment"></a>Problemas conocidos: Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior.

   > [!IMPORTANT]
   > Debe los datos de copia de seguridad y, a continuación, eliminar el clúster existente de datos de gran tamaño (con la versión anterior de **mssqlctl**) antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

- El **ACCEPT_EULA** variable de entorno debe ser "yes" o "Sí" para aceptar los términos de licencia. Las versiones anteriores permiten "y" e "Y", pero estos ya no se aceptan y producirá un error de implementación.

- El **CLUSTER_PLATFORM** variables de entorno no tiene valor predeterminado es igual que en versiones anteriores.

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

### <a name="known-issues-kubeadm-deployments"></a>Problemas conocidos: kubeadm implementaciones

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

### <a id="mssqlctlctp23"></a> Problemas conocidos: mssqlctl

- El **mssqlctl** herramienta cambió de un comando verbo-nombre pedidos a un pedido de nombre-verbo. Por ejemplo, `mssqlctl create cluster` es ahora `mssqlctl cluster create`.

- El `--name` parámetro ahora es necesario al crear un clúster con `mssqlctl cluster create`.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- Para obtener información importante sobre cómo actualizar a la versión más reciente de los clústeres de macrodatos y **mssqlctl**, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

### <a name="known-issues-external-tables"></a>Problemas conocidos: Tablas externas

- Es posible crear una tabla externa de grupo de datos para una tabla que tiene no compatibles de tipos de columna. Si consulta la tabla externa, recibirá un mensaje similar al siguiente:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- Si consulta una tabla externa del grupo de almacenamiento, podría obtener un error si se está copiando el archivo subyacente en HDFS al mismo tiempo.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- Si va a crear una tabla externa a Oracle que usan tipos de datos de caracteres, el Asistente para la virtualización de Azure Data Studio interpreta estas columnas como VARCHAR en la definición de tabla externa. Esto provocará un error en el DDL de tabla externa. Modifique el esquema de Oracle para usar el tipo NVARCHAR2, o crear manualmente las instrucciones de la tabla externa y especificar NVARCHAR en lugar de usar al asistente.

### <a name="known-issues-application-deployment"></a>Problemas conocidos: Implementación de aplicaciones

- Al llamar a una aplicación de R, Python o MLeap desde la API de REST, la llamada a veces horizontal en 5 minutos.

### <a name="known-issues-spark-and-notebooks"></a>Problemas conocidos: Spark y cuadernos

- Pueden cambiar las direcciones IP de POD en el entorno de Kubernetes como reinicios de PODs. En el escenario donde se reinicia el patrón de pod, puede producir un error de la sesión de Spark con `NoRoteToHostException`. Esto se produce por las cachés JVM que no se actualiza con la nueva dirección IP direcciones.

- Si tiene Jupyter ya instalado y un independiente de Python en Windows, se pueden producir un error en cuadernos de Spark. Para solucionar este problema, actualice Jupyter a la versión más reciente.

- En un bloc de notas, si hace clic en el **agregar texto** comando, se agrega el texto de la celda en modo de vista previa en lugar de en modo de edición. Puede hacer clic en el icono de vista previa para activar o desactivar para el modo de edición y editar la celda.

### <a name="known-issues-hdfs"></a>Problemas conocidos: HDFS

- Si hace clic derecho en un archivo de HDFS para obtener la vista previa, puede aparecer el siguiente error:

   `Error previewing file: File exceeds max size of 30MB`

   Actualmente no hay ninguna manera de obtener una vista previa de los archivos mayores de 30 MB en Azure Data Studio.

- No se admiten los cambios de configuración HDFS que implican cambios en hdfs-site.xml.

### <a name="known-issues-security"></a>Problemas conocidos: Seguridad

- El contraseña_sa forma parte del entorno y reconocibles (por ejemplo, en un archivo de volcado de cable). Debe restablecer el contraseña_sa en la instancia principal después de la implementación. Esto no es un error, pero un paso de seguridad. Para obtener más información sobre cómo cambiar el contraseña_sa en un contenedor de Linux, consulte [cambiar la contraseña de SA](../linux/quickstart-install-connect-docker.md#sapassword).

- Los registros AKS pueden contener la contraseña de SA para las implementaciones de clústeres de datos de gran tamaño.

## <a id="ctp22"></a> CTP 2.2 (diciembre de 2018)

Las secciones siguientes describen las nuevas características y problemas conocidos de clústeres de datos de gran tamaño en SQL Server 2019 CTP 2.2.

### <a name="whats-in-the-ctp-22-release"></a>¿Qué es la versión de CTP 2.2?

- Portal de administración de clúster que se accede con `/portal` (**https://\<ip-address\>: 30777/portal**).
- Nombre del grupo principal de servicio cambió de `service-master-pool-lb` y `service-master-pool-nodeport` a `endpoint-master-pool`.
- Nueva versión de **mssqlctl** y actualiza las imágenes.
- Mejoras y correcciones de errores.

### <a name="known-issues"></a>Problemas conocidos

Las secciones siguientes proporcionan los problemas conocidos para los clústeres de macrodatos de SQL Server en CTP 2.2.

#### <a name="deployment"></a>Implementación

- No se admite la actualización de un clúster de macrodatos datos desde una versión anterior. Debe de copia de seguridad y eliminar cualquier clúster de macrodatos existente antes de implementar la versión más reciente. Para obtener más información, consulte [actualizar a una nueva versión](deployment-guidance.md#upgrade).

- Después de implementar en AKS, es posible que vea los siguientes dos eventos de advertencia de la implementación. Ambos de estos eventos son problemas conocidos, pero no podrá implementar correctamente el clúster de macrodatos en AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- Si se produce un error en la implementación de un clúster de macrodatos, no se quita el espacio de nombres asociado. Esto podría dar lugar a un espacio de nombres huérfano en el clúster. Una solución consiste en eliminar el espacio de nombres manualmente antes de implementar un clúster con el mismo nombre.

#### <a name="cluster-administration-portal"></a>Portal de administración de clústeres

El portal de administración de clúster no muestra el punto de conexión para la instancia principal de SQL Server. Para encontrar la dirección IP y puerto de la instancia maestra, use el siguiente **kubectl** comando:

```
kubectl get svc endpoint-master-pool -n <your-cluster-name>
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
