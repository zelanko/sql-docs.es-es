---
title: Vista del estado del clúster
titleSuffix: SQL Server big data clusters
description: En este artículo, se explica cómo ver el estado de un clúster de macrodatos mediante Azure Data Studio, cuadernos y comandos de azdata.
author: yualan
ms.author: alayu
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 45cf5461b9154d397ee5365fd275d2545a3cc376
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531585"
---
# <a name="how-to-view-the-status-of-a-big-data-cluster"></a>Procedimiento para ver el estado de un clúster de macrodatos 

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo acceder a los puntos de conexión del servicio y ver el estado de los componentes de un clúster de macrodatos de SQL Server. Puede usar tanto Azure Data Studio como **azdata**, y en este artículo se describen las dos técnicas.

## <a id="datastudio"></a> Usar Azure Data Studio

Después de descargar la versión más reciente de la **compilación para los participantes del programa Insider** de [Azure Data Studio](https://aka.ms/getazuredatastudio), podrá ver los puntos de conexión del servicio y el estado de un clúster de macrodatos con el panel del clúster de macrodatos de SQL Server. Algunas de las siguientes características solo estarán disponibles por primera vez en la compilación de los participantes del programa Insider de Azure Data Studio.

1. Primero, cree una conexión al clúster de macrodatos en Azure Data Studio. Para obtener más información, vea [Conectarse a un clúster de macrodatos de SQL Server con Azure Data Studio](connect-to-big-data-cluster.md).

1. Haga clic con el botón derecho en el punto de conexión del clúster de macrodatos y, después, seleccione **Administrar**.

   ![botón derecho y administrar](media/view-cluster-status/right-click-manage.png)

1. Seleccione la pestaña **Clúster de macrodatos de SQL Server** para acceder al panel del clúster de macrodatos.

   ![Panel del clúster de macrodatos](media/view-cluster-status/bdc-dashboard.png)

### <a name="service-endpoints"></a>Puntos de conexión del servicio

Es importante que se pueda acceder fácilmente a distintos servicios de un clúster de macrodatos. En el panel del clúster de macrodatos, se proporciona una tabla de puntos de conexión del servicio que le permite ver y copiar los puntos de conexión del servicio.

![puntos de conexión del servicio](media/view-cluster-status/service-endpoints.png)

En estos servicios, se muestran los puntos de conexión que se pueden copiar y pegar si necesita usar el punto de conexión para conectarse a esos servicios. Por ejemplo, puede hacer clic en el icono de copiar a la derecha del punto de conexión y, después, pegarlo en una ventana de texto en la que se solicite este punto de conexión. El punto de conexión del servicio de administración de clústeres es necesario para ejecutar el [cuaderno de estado del clúster](#notebook).

### <a name="dashboards"></a>Paneles

En la tabla de puntos de conexión del servicio, también se muestran varios paneles de supervisión:

- Métricas (Grafana)
- Registros (Kibana)
- Supervisión de trabajos de Spark
- Administración de recursos de Spark

Puede hacer clic directamente de estos vínculos. Se le pedirá que se autentique al acceder a estos paneles. En el caso de los paneles de métricas y registros, indique las credenciales de administrador del controlador que estableció en el momento de la implementación mediante las variables de entorno **AZDATA_USERNAME** y **AZDATA_PASSWORD**. Los paneles de Spark usarán credenciales de puerta de enlace (Knox), ya sea la identidad de AD en un clúster integrado con AD o el usuario **raíz** y **AZDATA_PASSWORD**, si se usa la autenticación básica en el clúster. 

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

5. Si la conexión se establece correctamente, en el resto del cuaderno se mostrará el resultado de cada componente del clúster de macrodatos. Para volver a ejecutar una determinada celda de código, mantenga el puntero sobre la celda de código y haga clic en el icono de **Ejecutar**.

## <a name="use-azdata"></a>Usar azdata

También puede usar los comandos de [azdata](deploy-install-azdata.md) para ver tanto los puntos de conexión como el estado del clúster.

### <a name="service-endpoints"></a>Puntos de conexión del servicio

1. Inicie sesión en el clúster de macrodatos con [azdata login](reference-azdata.md). Establezca el parámetro **--controller-endpoint** en la dirección IP externa del punto de conexión del controlador.

   ```bash
   azdata login --endpoint https://<ip-address-of-controller-svc-external>:30080 --username <user-name>
   ```

   Especifique el nombre de usuario y la contraseña que configuró para el controlador (AZDATA_USERNAME y AZDATA_PASSWORD) durante la implementación. 
   En la autenticación de AD, el comando es:

  ```bash
   azdata login --endpoint https://<control_domain_name>:30080 --auth ad
   ```

1. Ejecute [`azdata bdc endpoint list`](reference-azdata-bdc-endpoint.md) para obtener una lista con una descripción de cada punto de conexión y los valores correspondientes de dirección IP y puerto. 

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

Puede ver el estado del clúster con el comando [`azdata bdc status show`](reference-azdata-bdc-status.md).

```bash
azdata bdc status show
```

> [!TIP]
> Para ejecutar los comandos de estado, primero necesita iniciar sesión con el comando **azdata login**, que se ha mostrado en la sección de puntos de conexión anterior.

Este es un resultado de ejemplo de este comando:

```output
 Bdc: ready                                                                                                                                                                                                          Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Services: ready                                                                                                                                                                                                     Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Servicename    State    Healthstatus    Details

 spark          ready    healthy         -
 sql            ready    healthy         -
 hdfs           ready    healthy         -
 control        ready    healthy         -
 gateway        ready    healthy         -
 app            ready    healthy         -


 Spark Services: ready                                                                                                                                                                                               Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sql Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 master          ready    healthy         StatefulSet master is healthy
 compute-0       ready    healthy         StatefulSet compute-0 is healthy
 data-0          ready    healthy         StatefulSet data-0 is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Hdfs Services: ready                                                                                                                                                                                                Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 nmnode-0        ready    healthy         StatefulSet nmnode-0 is healthy
 zookeeper       ready    healthy         StatefulSet zookeeper is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy
 sparkhead       ready    healthy         StatefulSet sparkhead is healthy


 Control Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 controldb       ready    healthy         StatefulSet controldb is healthy
 control         ready    healthy         ReplicaSet control is healthy
 metricsdc       ready    healthy         DaemonSet metricsdc is healthy
 metricsui       ready    healthy         ReplicaSet metricsui is healthy
 metricsdb       ready    healthy         StatefulSet metricsdb is healthy
 logsui          ready    healthy         ReplicaSet logsui is healthy
 logsdb          ready    healthy         StatefulSet logsdb is healthy
 mgmtproxy       ready    healthy         ReplicaSet mgmtproxy is healthy
 controlwd       ready    healthy         ReplicaSet controlwd is healthy


 Gateway Services: ready                                                                                                                                                                                             Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 gateway         ready    healthy         StatefulSet gateway is healthy


 App Services: ready                                                                                                                                                                                                 Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 appproxy        ready    healthy         ReplicaSet appproxy is healthy
```

### <a name="view-specific-resource-status"></a>Visualización del estado de un recurso específico

Puede ver el estado de un recurso específico en el clúster con el comando [azdata bdc status show](reference-azdata-bdc-status.md). Cuando se usa este comando, se puede filtrar con el parámetro `--resource`. Estos son algunos ejemplos de entradas del parámetro `--resource`:

- maestra
- control
- compute-0
- storage-0
- gateway

Por ejemplo, el siguiente comando muestra el estado del grupo de almacenamiento:

```bash
azdata bdc status show --all --resource storage-0
```

Para ver el estado de todos los componentes que ejecutan un servicio específico, deberá usar el grupo de comandos correspondiente `azdata bdc <serviceName> status show`. Por ejemplo:

- azdata bdc sql status show --all
- azdata bdc hdfs status show --all
- azdata bdc spark status show --all

Esta es una salida de ejemplo:

```output
  Storage-0: ready                                                                                                                                                                                                    Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Instances: running                                                                                                                                                                                                  Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


 Dashboards
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Name            Url

 nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
 sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
 logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
 ```

> [!TIP]
> Ejecute el comando de estado con parámetros `--all` para ver más detalles sobre el estado, como los vínculos a paneles de métricas y registros correspondientes a la instancia específica. Esta es una salida de ejemplo cuando se usan parámetros `--all`:

```output
 Spark: ready                                                                                                                                                                                                        Health Status:  healthy
 ===========================================================================================================================================================================================================================================
 Resources: ready                                                                                                                                                                                                    Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Resourcename    State    Healthstatus    Details

 sparkhead       ready    healthy         StatefulSet sparkhead is healthy
 storage-0       ready    healthy         StatefulSet storage-0 is healthy


 Sparkhead Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 sparkhead-0     running  healthy         Pod sparkhead-0 is healthy
 sparkhead-1     running  healthy         Pod sparkhead-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/sparkhead-1/status/logs/ui


 Storage-0 Resources: running                                                                                                                                                                                        Health Status:  healthy
 -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Instancename    State    Healthstatus    Details

 storage-0-0     running  healthy         Pod storage-0-0 is healthy
 storage-0-1     running  healthy         Pod storage-0-1 is healthy


      Dashboards
      --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
      Name            Url

      nodeMetricsUrl  https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/nodemetrics/ui
      sqlMetricsUrl   https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/sqlmetrics/ui
      logsUrl         https://13.91.50.9:30777/api/v1/bdc/instances/storage-0-1/status/logs/ui
```

El valor `logsUrl` vincula a un panel de Kibana:

![Panel de Kibana](./media/view-cluster-status/kibana-dashboard.png)

> [!NOTE]
> El explorador Microsoft Edge (antiguo) no es compatible con Kibana; deberá usar el explorador basado en Chromium para que el panel se muestre correctamente. Si se usa un explorador no compatible, aparecerá una página en blanco al cargar los paneles. Consulte aquí qué exploradores son compatibles con Kibana.

Los valores `nodeMetricsUrl` y `sqlMetricsUrl` vinculan a un panel de Grafana para supervisar las métricas de nodo de Kubernetes y las métricas de servicio del clúster de macrodatos:

![Panel de Grafana](./media/view-cluster-status/grafana-dashboard.png)

![SQL](./media/view-cluster-status/grafana-sql-status.png)

### <a name="view-controller-status"></a>Ver el estado del controlador

Puede ver el estado del controlador con el comando [`azdata bdc control status show`](reference-azdata-bdc-control-status.md). Proporciona vínculos similares a los paneles de supervisión relacionados con los complementos de controlador del clúster de macrodatos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre los clústeres de macrodatos, vea [¿Qué son [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?](big-data-cluster-overview.md)
