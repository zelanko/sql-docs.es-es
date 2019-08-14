---
title: Vista del estado del clúster
titleSuffix: SQL Server big data clusters
description: En este artículo, se explica cómo ver el estado de un clúster de macrodatos mediante Azure Data Studio, cuadernos y comandos de azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c6dca94b8bd7547222394d7809cb003b9e936982
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68419292"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Procedimiento para ver el estado de un clúster de macrodatos

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo, se describe cómo acceder a los puntos de conexión del servicio y ver el estado de un clúster de macrodatos de SQL Server (versión preliminar). Puede usar tanto Azure Data Studio como **azdata**, y en este artículo se describen las dos técnicas.

## <a id="datastudio"></a> Usar Azure Data Studio

Después de descargar la versión más reciente de la **compilación para los participantes del programa Insider** de [Azure Data Studio](https://aka.ms/azdata-insiders), podrá ver los puntos de conexión del servicio y el estado de un clúster de macrodatos con el panel del clúster de macrodatos de SQL Server. Tenga en cuenta que algunas de las características siguientes solo estarán disponibles antes para la compilación de los participantes del programa Insider de Azure Data Studio.

1. Primero, cree una conexión al clúster de macrodatos en Azure Data Studio. Para obtener más información, vea [Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

1. Haga clic con el botón derecho en el punto de conexión del clúster de macrodatos y, después, seleccione **Administrar**.

   ![botón derecho y administrar](media/view-cluster-status/right-click-manage.png)

1. Seleccione la pestaña **Clúster de macrodatos de SQL Server** para acceder al panel del clúster de macrodatos.

   ![Panel del clúster de macrodatos](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Puntos de conexión del servicio

Es importante que se pueda acceder fácilmente a distintos servicios de un clúster de macrodatos. En el panel del clúster de macrodatos, se proporciona una tabla de puntos de conexión del servicio que le permite ver y copiar los puntos de conexión del servicio.

![puntos de conexión del servicio](media/view-cluster-status/service-endpoints.png)

En las primeras filas, se muestran estos servicios:

- Proxy de aplicación
- Servicio de administración de clústeres
- HDFS y Spark
- Proxy de administración

En estos servicios, se muestran los puntos de conexión que se pueden copiar y pegar si necesita usar el punto de conexión para conectarse a esos servicios. Por ejemplo, puede hacer clic en el icono de copiar a la derecha del punto de conexión y, después, pegarlo en una ventana de texto en la que se solicite este punto de conexión. El punto de conexión del servicio de administración de clústeres es necesario para ejecutar el [cuaderno de estado del clúster](#notebook).

### <a name="dashboards"></a>Paneles

En la tabla de puntos de conexión del servicio, también se muestran varios paneles de supervisión:

- Métricas (Grafana)
- Registros (Kibana)
- Supervisión de trabajos de Spark
- Administración de recursos de Spark

Puede hacer clic directamente de estos vínculos. Antes de conectarse al servicio, se le pedirá dos veces que especifique el nombre de usuario y la contraseña.

### <a id="notebook"></a> Cuaderno de estado del clúster

1. También puede ver el estado del clúster de macrodatos si inicia el cuaderno de estado del clúster. Para iniciar el cuaderno, haga clic en la tarea **Estado del clúster**.

    ![iniciar](media/view-cluster-status/cluster-status-launch.png)

2. Antes de empezar, necesitará los elementos siguientes:

    - Nombre del clúster de macrodatos
    - Nombre de usuario del controlador
    - Contraseña del controlador
    - Puntos de conexión del controlador

    El nombre del clúster de macrodatos predeterminado es **mssql-cluster**, excepto si lo personaliza durante la implementación. Encontrará el punto de conexión del controlador del panel del clúster de macrodatos en la tabla de puntos de conexión del servicio. El punto de conexión se muestra como **Servicio de administración de clústeres**. Si no conoce las credenciales, solicítelas al administrador que implementó el clúster.

3. En la barra de herramientas superior, haga clic en **Ejecutar celdas**.

4. Verá una solicitud de credenciales. Presione ENTRAR después de escribir cada credencial para el nombre del clúster de macrodatos, el nombre de usuario del controlador y la contraseña del controlador.

    > [!Note]
    > Si no tiene un archivo de configuración preparado con los macrodatos, se le pedirá que especifique el punto de conexión del controlador. Escríbalo o péguelo y, después, presione ENTRAR para continuar.

5. Si la conexión se establece correctamente, en el resto del cuaderno se mostrará el resultado de cada componente del clúster de macrodatos. Para volver a ejecutar una determinada celda de código, mantenga el mouse sobre la celda de código y haga clic en el icono de **Ejecutar**.

## <a name="use-azdata"></a>Usar azdata

También puede usar los comandos de [azdata](deploy-install-azdata.md) para ver tanto los puntos de conexión como el estado del clúster.

### <a name="service-endpoints"></a>Puntos de conexión del servicio

Siga este procedimiento para obtener las direcciones IP de los puntos de conexión externos del clúster de macrodatos.

1. Para conocer la dirección IP del punto de conexión del controlador, vea el resultado de EXTERNAL-IP del siguiente comando de **kubectl**:

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

   > [!TIP]
   > Si no ha cambiado el nombre predeterminado durante la implementación, use `-n mssql-cluster` en el comando anterior. **mssql-cluster** es el nombre predeterminado del clúster de macrodatos.

1. Inicie sesión en el clúster de macrodatos con [azdata login](reference-azdata.md). Establezca el parámetro **--controller-endpoint** en la dirección IP externa del punto de conexión del controlador.

   ```bash
   azdata login --controller-endpoint https://<ip-address-of-controller-svc-external>:30080 --controller-username <user-name>
   ```

   Especifique el nombre de usuario y la contraseña que ha configurado para el controlador (CONTROLLER_USERNAME y CONTROLLER_PASSWORD) durante la implementación.

1. Ejecute [azdata bdc endpoint list](reference-azdata-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y los valores correspondientes de dirección IP y puerto. 

   ```bash
   azdata bdc endpoint list -o table
   ```

   En la lista siguiente, se muestra un resultado de ejemplo de este comando:

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

Puede ver el estado del clúster con el comando [azdata bdc status show](reference-azdata-bdc-status.md).

```bash
azdata bdc status show -o table
```

> [!TIP]
> Para ejecutar los comandos de estado, primero necesita iniciar sesión con el comando **azdata login**, que se ha mostrado en la sección de puntos de conexión anterior.

Este es un resultado de ejemplo de este comando:

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

### <a name="view-pool-status"></a>Ver estado del grupo

Puede ver el estado de los grupos en el clúster con el comando [azdata bdc pool status show](reference-azdata-bdc-pool-status.md). Para usar este comando, especifique el tipo de grupo con el parámetro `--kind`. Los tipos de grupo son:

- compute
- datos
- maestra
- spark
- storage

Por ejemplo, el comando siguiente muestra el estado del grupo de almacenamiento:

```bash
azdata bdc pool status show --kind storage
```

Verá un texto similar al resultado siguiente:

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

El valor `logsUrl` vincula a un panel de Kibana con información de registro:

![Panel de Kibana](./media/view-cluster-status/kibana-dashboard.png)

Los valores `nodeMetricsUrl` y `sqlMetricsUrl` vinculan a un panel de Grafana para supervisar el estado del nodo y las métricas de SQL:

![Panel de Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Ver el estado del controlador

Puede ver el estado del controlador con el comando [azdata bdc control status show](reference-azdata-bdc-control-status.md). Proporciona vínculos similares a los paneles de supervisión relacionados con los nodos de controlador del clúster de macrodatos.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos, vea [¿Qué son los clústeres de macrodatos de SQL Server?](big-data-cluster-overview.md)
