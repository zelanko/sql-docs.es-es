---
title: Vista del estado del clúster
titleSuffix: SQL Server big data clusters
description: En este artículo se explica cómo ver el estado de un clúster de Big Data mediante Azure Data Studio, notebooks y comandos azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419292"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Cómo ver el estado de un clúster de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo acceder a los puntos de conexión de servicio y ver el estado de un clúster de macrodatos SQL Server (versión preliminar). Puede usar Azure Data Studio y **azdata**, y en este artículo se explican ambas técnicas.

## <a id="datastudio"></a>Usar Azure Data Studio

Después de descargar la **versión** más reciente de la compilación de [Azure Data Studio](https://aka.ms/azdata-insiders), puede ver los puntos de conexión de servicio y el estado de un clúster de Big Data con el panel del clúster de macrodatos SQL Server. Tenga en cuenta que algunas de las características siguientes solo están disponibles en primer lugar en la compilación de Azure Data Studio.

1. En primer lugar, cree una conexión a su clúster de Big Data en Azure Data Studio. Para más información, consulte [conexión a un clúster de SQL Server Big Data con Azure Data Studio](connect-to-big-data-cluster.md).

1. Haga clic con el botón derecho en el punto de conexión del clúster de Big Data y haga clic en **administrar**.

   ![Haga clic con el botón derecho en administrar](media/view-cluster-status/right-click-manage.png)

1. Seleccione la pestaña clúster de macrodatos de **SQL Server** para acceder al panel del clúster de Big Data.

   ![Panel del clúster de Big Data](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Puntos de conexión de servicio

Es importante poder acceder fácilmente a los distintos servicios dentro de un clúster de Big Data. El panel del clúster de Big Data proporciona una tabla de puntos de conexión de servicio que le permite ver y copiar los puntos de conexión de servicio.

![Puntos de conexión de servicio](media/view-cluster-status/service-endpoints.png)

Las primeras filas exponen los siguientes servicios:

- Proxy de aplicación
- Servicio de administración de clústeres
- HDFS y Spark
- Proxy de administración

Estos servicios enumeran los extremos que se pueden copiar y pegar cuando se necesita el punto de conexión para conectarse a esos servicios. Por ejemplo, puede hacer clic en el icono de copia situado a la derecha del punto de conexión y, a continuación, pegarlo en una ventana de texto que solicite ese extremo. El punto de conexión del servicio de administración de clústeres es necesario para ejecutar el [Bloc de notas de estado de clúster](#notebook).

### <a name="dashboards"></a>Paneles

La tabla de puntos de conexión de servicio también expone varios paneles para la supervisión:

- Métricas (Grafana)
- Registros (Kibana)
- Supervisión de trabajos de Spark
- Administración de recursos de Spark

Puede hacer clic directamente en estos vínculos. Se le pedirá dos veces que proporcione su nombre de usuario y contraseña antes de conectarse al servicio.

### <a id="notebook"></a>Cuaderno de estado del clúster

1. También puede ver el estado de clúster del clúster de Big Data si inicia el Bloc de notas de estado de clúster. Para iniciar el cuaderno, haga clic en la tarea **Estado del clúster** .

    ![Launch](media/view-cluster-status/cluster-status-launch.png)

2. Antes de empezar, necesitará los siguientes elementos:

    - Nombre del clúster de Big Data
    - Nombre de usuario del controlador
    - Contraseña del controlador
    - Puntos de conexión del controlador

    El nombre del clúster de macrodatos predeterminado es **MSSQL-Cluster** a menos que lo personalizara durante la implementación. Puede encontrar el punto de conexión del controlador en el panel del clúster de Big Data en la tabla de puntos de conexión de servicio. El punto de conexión aparece como **servicio de administración**de clústeres. Si no conoce las credenciales, pregunte al administrador que implementó el clúster.

3. Haga clic en **Ejecutar celdas** en la barra de herramientas superior.

4. Siga las indicaciones de sus credenciales. Presione entrar después de escribir cada credencial para el nombre del clúster de Big Data, el nombre de usuario del controlador y la contraseña del controlador.

    > [!Note]
    > Si no tiene un archivo de configuración configurado con los macrodatos, se le pedirá el punto de conexión del controlador. Escríbala o péguela y, a continuación, presione Entrar para continuar.

5. Si se ha conectado correctamente, el resto del cuaderno mostrará el resultado de cada componente del clúster de Big Data. Cuando desee volver a ejecutar una determinada celda de código, mantenga el mouse sobre la celda de código y haga clic en el icono **Ejecutar** .

## <a name="use-azdata"></a>Usar azdata

También puede usar los comandos [azdata](deploy-install-azdata.md) para ver los puntos de conexión y el estado del clúster.

### <a name="service-endpoints"></a>Puntos de conexión de servicio

Puede obtener las direcciones IP de los puntos de conexión externos para el clúster de Big Data mediante los pasos siguientes.

1. Busque la dirección IP del punto de conexión del controlador examinando la salida EXTERNAL-IP del siguiente comando de **kubectl** :

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no cambió el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **MSSQL-Cluster** es el nombre predeterminado para el clúster de Big Data.

1. Inicie sesión en el clúster de Big Data con el [Inicio de sesión de azdata](reference-azdata.md). Establezca el parámetro **--Controller-Endpoint** en la dirección IP externa del punto de conexión del controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y la contraseña que configuró para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute la [lista de puntos de conexión de BDC de azdata](reference-azdata-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y sus valores de puerto y dirección IP correspondientes. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   En la lista siguiente se muestra la salida de ejemplo de este comando:

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

Puede ver el estado del clúster con el comando [azdata BDC status show](reference-azdata-bdc-status.md) .

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero debe iniciar sesión con el comando de **Inicio de sesión de azdata** , que se mostró en la sección puntos de conexión anteriores.

En el siguiente ejemplo se muestra la salida de este comando:

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

### <a name="view-pool-status"></a>Ver el estado del grupo

Puede ver el estado de los grupos del clúster con el comando de [Estado de grupo de BDC de azdata](reference-azdata-bdc-pool-status.md) . Para usar este comando, especifique el tipo de grupo con el `--kind` parámetro. Los tipos de grupo son:

- Proceso
- data
- maestra
- Vinos
- Discos

Por ejemplo, el comando siguiente muestra el estado del grupo de almacenamiento:

```bash
azdata bdc pool status show --kind storage
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

El `logsUrl` valor se vincula a un panel de Kibana con información de registro:

![Panel de Kibana](./media/view-cluster-status/kibana-dashboard.png)

Los `nodeMetricsUrl` valores `sqlMetricsUrl` y se vinculan a un panel de grafana para supervisar el estado de los nodos y las métricas de SQL:

![Panel de Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Ver el estado del controlador

Puede ver el estado del controlador con el comando [azdata BDC control status show](reference-azdata-bdc-control-status.md) . Proporciona vínculos similares a los paneles de supervisión relacionados con los nodos de controlador del clúster de Big Data.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son](big-data-cluster-overview.md)los clústeres de macrodatos SQL Server.
