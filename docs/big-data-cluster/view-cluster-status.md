---
title: Vista del estado del clúster
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo ver el estado de un clúster de macrodatos con Azure Data Studio, blocs de notas y mssqlctl comandos.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 06/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1a8d04ab43adac77a534a82626cc4a018c24b68f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957677"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Cómo ver el estado de un clúster de macrodatos

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo tener acceso a los puntos de conexión de servicio y ver el estado de un clúster de macrodatos de SQL Server (versión preliminar). Puede usar tanto Azure Data Studio y **mssqlctl**, y este artículo tratan ambas técnicas.

## <a id="datastudio"></a> Uso de Studio datos de Azure

Después de descargar la versión más reciente **Insider** de [Azure Data Studio](https://aka.ms/azdata-insiders), puede ver los puntos de conexión de servicio y el estado de un big data de un clúster con el panel del clúster de macrodatos de SQL Server. Tenga en cuenta que algunas de las siguientes características en primer lugar solo están disponibles en la compilación de Insider de Azure Data Studio.

1. En primer lugar, cree una conexión con el clúster de macrodatos en Azure Data Studio. Para obtener más información, consulte [conectar a SQL Server del clúster macrodatos con Azure Data Studio](connect-to-big-data-cluster.md).

1. Haga doble clic en el punto de conexión del clúster de macrodatos y haga clic en **administrar**.

   ![administrar clic derecho](media/view-cluster-status/right-click-manage.png)

1. Seleccione el **clúster grande de datos de SQL Server** tab para tener acceso al panel de clúster de macrodatos.

   ![Panel de clúster de macrodatos](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Puntos de conexión de servicio

Es importante poder tener acceso fácilmente a los diversos servicios dentro de un clúster de macrodatos. El panel de clúster de macrodatos proporciona una tabla de puntos de conexión de servicio que le permite ver y copiar los extremos de servicio.

![Puntos de conexión de servicio](media/view-cluster-status/service-endpoints.png)

Las primeras filas exponen los servicios siguientes:

- Proxy de aplicación
- Servicio de administración de clúster
- HDFS y Spark
- Proxy de administración

Estos servicios enumeran los puntos de conexión que se pueden copiar y pegar cuando se necesita el punto de conexión para conectarse a esos servicios. Por ejemplo, puede haga clic en el icono de copia a la derecha del punto de conexión y, a continuación, péguelo en una ventana de texto que solicita ese punto de conexión. El punto de conexión de servicio de administración de clúster es necesario ejecutar el [Bloc de notas de estado de clúster](#notebook).

### <a name="dashboards"></a>Paneles

La tabla de puntos de conexión de servicio también expone varios paneles de supervisión:

- Métricas (Grafana)
- Registros (Kibana)
- Supervisión de trabajos de Spark
- Administración de recursos de Spark

Puede hacer clic directamente en estos vínculos. Se pide dos veces para proporcionar el nombre de usuario y la contraseña antes de conectarse al servicio.

### <a id="notebook"></a> Cuaderno de estado del clúster

1. También puede ver el estado del clúster del clúster de macrodatos, inicie el Bloc de notas de estado del clúster. Para iniciar el Bloc de notas, haga clic en el **estado del clúster** tarea.

    ![iniciar](media/view-cluster-status/cluster-status-launch.png)

2. Antes de comenzar, necesita los siguientes elementos:

    - Nombre del clúster de macrodatos
    - Nombre de usuario del controlador
    - Contraseña del controlador
    - Puntos de conexión del controlador

    Es el nombre predeterminado del clúster de macrodatos **mssql-cluster** a menos que personalice durante la implementación. Puede encontrar el punto de conexión del controlador desde el panel de clúster de macrodatos en la tabla de puntos de conexión de servicio. El punto de conexión aparece como **servicio Cluster Management**. Si no conoce las credenciales, póngase en contacto el administrador que ha implementado el clúster.

3. Haga clic en **celdas ejecutar** en la barra de herramientas superior.

4. Siga las indicaciones para sus credenciales. Presione ENTRAR después de escribir cada credencial para el nombre del clúster de macrodatos, nombre de usuario del controlador y la contraseña del controlador.

    > [!Note]
    > Si no tiene una configuración de archivo de configuración con los datos de gran tamaño, se le pedirá para el punto de conexión del controlador. Escriba o lo pegue y, a continuación, presione ENTRAR para continuar.

5. Si se conectó correctamente, el resto del cuaderno muestra la salida de cada componente del clúster de macrodatos. Cuando desee volver a ejecutar una celda de código determinado, mantenga el mouse sobre la celda de código y haga clic en el **ejecutar** icono.

## <a name="use-mssqlctl"></a>Usar mssqlctl

También puede usar [mssqlctl](deploy-install-mssqlctl.md) comandos para ver los puntos de conexión y el estado del clúster.

### <a name="service-endpoints"></a>Puntos de conexión de servicio

Puede obtener las direcciones IP de los puntos de conexión externos para el clúster de macrodatos mediante los siguientes pasos.

1. Buscar la dirección IP del punto de conexión del controlador examinando la salida EXTERNAL-IP de los siguientes **kubectl** comando:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no cambió el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **MSSQL-cluster** es el nombre predeterminado para el clúster de macrodatos.

1. Inicie sesión en el clúster de macrodatos con [inicio de sesión mssqlctl](reference-mssqlctl.md). Establecer el **--punto de conexión del controlador** parámetro a la dirección IP externa del punto de conexión del controlador.

   ```bash
   mssqlctl login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y contraseña que ha configurado para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute [lista de puntos de conexión de bdc mssqlctl](reference-mssqlctl-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y sus correspondientes valores de puerto y la dirección IP. 

   ```bash
   mssqlctl bdc endpoint list -o table
   ```

   En la lista siguiente se muestra la salida de este comando:

   ```output
   Description                                             Endpoint                                                   Ip              Name               Port    Protocol
   ------------------------------------------------------  ---------------------------------------------------------  --------------  -----------------  ------  ----------
   Gateway to access HDFS files, Spark                     https://11.111.111.111:30443                               11.111.111.111  gateway            30443   https
   Spark Jobs Management and Monitoring Dashboard          https://11.111.111.111:30443/gateway/default/sparkhistory  11.111.111.111  spark-history      30443   https
   Spark Diagnostics and Monitoring Dashboard              https://11.111.111.111:30443/gateway/default/yarn          11.111.111.111  yarn-ui            30443   https
   Application Proxy                                       https://11.111.111.111:30778                               11.111.111.111  app-proxy          30778   https
   Management Proxy                                        https://11.111.111.111:30777                               11.111.111.111  mgmtproxy          30777   https
   Log Search Dashboard                                    https://11.111.111.111:30777/kibana                        11.111.111.111  logsui             30777   https
   Metrics Dashboard                                       https://11.111.111.111:30777/grafana                       11.111.111.111  metricsui          30777   https
   Cluster Management Service                              https://11.111.111.111:30080                               11.111.111.111  controller         30080   https
   SQL Server Master Instance Front-End                    11.111.111.111,31433                                       11.111.111.111  sql-server-master  31433   tcp
   HDFS File System Proxy                                  https://11.111.111.111:30443/gateway/default/webhdfs/v1    11.111.111.111  webhdfs            30443   https
   Proxy for running Spark statements, jobs, applications  https://11.111.111.111:30443/gateway/default/livy/v1       11.111.111.111  livy               30443   https
   ```

### <a name="view-cluster-status"></a>Vista del estado del clúster

Puede ver el estado del clúster con el [Mostrar estado de mssqlctl bdc](reference-mssqlctl-bdc-status.md) comando.

```bash
mssqlctl bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero debe iniciar sesión con la **inicio de sesión mssqlctl** comando, que se mostró en la sección de puntos de conexión anterior.

A continuación muestra la salida de ejemplo de este comando:

```output
Kind     Name           State
-------  -------------  -------
BDC      mssql-cluster  Ready
Control  default        Ready
Master   default        Ready
Compute  default        Ready
Data     default        Ready
Storage  default        Ready
```

### <a name="view-pool-status"></a>Ver el estado de grupo

Puede ver el estado de grupos dentro del clúster con el [show de estado de grupo de bdc mssqlctl](reference-mssqlctl-bdc-pool-status.md) comando. Para usar este comando, especifique el tipo de grupo con el `--kind` parámetro. Los tipos de grupo son:

- Proceso
- data
- maestra
- Spark
- Almacenamiento de información

Por ejemplo, el siguiente comando muestra el estado de grupo del grupo de almacenamiento:

```bash
mssqlctl bdc pool status show --kind storage
```

Debería ver texto similar al siguiente resultado:

```output
[
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/logs/ui",
    "name": "storage-0-0",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-0/sqlmetrics/ui",
    "state": "Running"
  },
  {
    "kind": "Pod",
    "logsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/logs/ui",
    "name": "storage-0-1",
    "nodeMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/nodemetrics/ui",
    "sqlMetricsUrl": "https://11.111.111.111:30080/clusters/mssql-cluster/pods/storage-0-1/sqlmetrics/ui",
    "state": "Running"
  }
]
```

El `logsUrl` valor vínculos a un panel de kibana con información del registro:

![panel de kibana](./media/view-cluster-status/kibana-dashboard.png)

El `nodeMetricsUrl` y `sqlMetricsUrl` vinculan valores a un panel de grafana para la supervisión de estado del nodo y las métricas SQL:

![Panel de Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Estado del controlador de vista

Puede ver el estado del controlador con el [mssqlctl bdc control estado show](reference-mssqlctl-bdc-control-status.md) comando. Se proporcionan vínculos similares a los paneles de supervisión relacionados con los nodos de controlador del clúster de macrodatos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server macrodatos](big-data-cluster-overview.md).
