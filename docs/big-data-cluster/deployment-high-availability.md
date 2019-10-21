---
title: Implementación de SQL Server clúster de Big Data con alta disponibilidad
titleSuffix: Deploy SQL Server Big Data Cluster with high availability
description: Aprenda a implementar SQL Server clúster de Big Data con alta disponibilidad.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 43d651c46282d7de0ffdd60f326740e7821b9bbe
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542161"
---
# <a name="deploy-sql-server-big-data-cluster-with-high-availability"></a>Implementación de SQL Server clúster de Big Data con alta disponibilidad

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En el momento de implementar un clúster de Big Data (BDC), puede configurar SQL Server maestro que se va a implementar en una configuración de grupo de disponibilidad. Esta configuración aumenta la confiabilidad de SQL Server Master, además de lo que la infraestructura Kubernetes habilita con su supervisión de estado integrada, la detección de errores y los mecanismos de conmutación por error. Los grupos de disponibilidad (AG) agregan redundancia a la instancia de SQL Server. En esta configuración, la supervisión, la detección de errores y las tareas de conmutación por error se administran mediante el servicio de administración de clúster de Big Data, es decir, el servicio de control.

Además, otras tareas de administración como la configuración de puntos de conexión de creación de reflejo de la base de datos, la creación del grupo de disponibilidad y la adición de bases de datos al grupo de disponibilidad se proporcionan mediante la plataforma de clúster de Big Data.

Estas son algunas de las funcionalidades que los grupos de disponibilidad habilitan:

1. Si se especifica la configuración de alta disponibilidad en el archivo de configuración de implementación, se crea un único grupo de disponibilidad denominado `containedag`. De forma predeterminada, `containedag` tiene tres réplicas, incluida la principal. Todas las operaciones CRUD para el grupo de disponibilidad se administran internamente.
1. Todas las bases de datos se agregan automáticamente al grupo de disponibilidad, incluidas `master` y `msdb`. Las bases de datos de configuración de polybase no se incluyen en el grupo de disponibilidad porque incluyen metadatos de nivel de instancia específicos de cada réplica.
1. Un punto de conexión externo se aprovisiona automáticamente para conectarse a las bases de datos de AG. Este punto de conexión `master-svc-external` desempeña el rol del agente de escucha de AG.
1. Se aprovisiona un segundo extremo externo para las conexiones de solo lectura a las réplicas secundarias. 


## <a name="deploy"></a>Implementación

Para implementar SQL Server maestro en un grupo de disponibilidad:

1. Habilitar la característica `hadr`
1. Especificar el número de réplicas para el AG (el mínimo es 3)
1. Configurar los detalles del segundo extremo externo creado para las conexiones a las réplicas secundarias de solo lectura

En los pasos siguientes se muestra cómo crear un archivo de revisión que incluye esta configuración y cómo aplicarla a los perfiles de configuración de `aks-dev-test` o `kubeadm-dev-test`. En estos pasos se describe un ejemplo de cómo revisar el perfil de `aks-dev-test` para agregar los atributos de alta disponibilidad. En el caso de una implementación en un clúster de kubeadm, se aplicaría una revisión similar, pero asegúrese de que está usando *NodePort* para el **serviceType** en la sección de **puntos de conexión** .

1. Crear un archivo de `patch.json`

    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.resources.master.spec",
          "value": {
            "type": "Master",
            "replicas": 3,
            "endpoints": [
              {
                "name": "Master",
                "serviceType": "LoadBalancer",
                "port": 31433
              },
              {
                "name": "MasterSecondary",
                "serviceType": "LoadBalancer",
                "port": 31436
              }
            ],
            "settings": {
              "sql": {
                "hadr.enabled": "true"
              }
            }
          }
        }
      ]
    }
    ```

1. Clonar el perfil de destino

    ```bash
    azdata bdc config init --source aks-dev-test --target custom-aks
    ```

1. Aplicar el archivo de revisión al perfil personalizado

    ```bash
    azdata bdc config patch -c custom-aks/bdc.json --patch-file patch.json
    ```
1. Iniciar la implementación del clúster con el perfil de configuración de clúster creado anteriormente

    ```bash
    azdata bdc create --config-profile custom-aks --accept-eula yes
    ```

## <a name="connect-to-sql-server-databases"></a>Conexión a bases de datos de SQL Server

En función del tipo de carga de trabajo que desee ejecutar en SQL Server maestro, puede conectarse al servidor principal para las cargas de trabajo de lectura y escritura o a las bases de datos de las réplicas secundarias para el tipo de cargas de trabajo de solo lectura. Este es un esquema para cada tipo de conexión:

### <a name="connect-to-databases-on-the-primary-replica"></a>Conectarse a bases de datos en la réplica principal

Para las conexiones a la réplica principal, use `sql-server-master` punto de conexión. Este punto de conexión también es el agente de escucha del AG. Todas las conexiones están en el contexto del grupo de disponibilidad. Por ejemplo, una conexión predeterminada que use este extremo dará lugar a la conexión a la base de datos de `master` dentro del AG, no a la instancia de SQL Server `master` base de datos.

```bash
azdata bdc endpoint list -e sql-server-master -o table
```

`Description                           Endpoint             Name               Protocol`
`------------------------------------  -------------------  -----------------  ----------`
`SQL Server Master Instance Front-End  13.64.235.192,31433  sql-server-master  tds`

> [!NOTE]
> Los eventos de conmutación por error pueden producirse durante la ejecución de una consulta distribuida que tiene acceso a datos de orígenes de datos remotos como HDFS o un grupo de datos. Como procedimiento recomendado, las aplicaciones deben diseñarse para tener lógica de reintento de conexión en caso de desconexiones producidas por la conmutación por error.  
>

### <a name="connect-to-databases-on-the-secondary-replicas"></a>Conexión a bases de datos en las réplicas secundarias

En el caso de las conexiones de solo lectura a las bases de datos de las réplicas secundarias, utilice el punto de conexión de `sql-server-master-readonly`. Este punto de conexión actúa como un equilibrador de carga en todas las réplicas secundarias. Proporcione el contexto de la base de datos de usuario en la cadena de conexión.

```bash
azdata bdc endpoint list -e sql-server-master-readonly -o table
```

`Description                                    Endpoint            Name                        Protocol`
`---------------------------------------------  ------------------  --------------------------  ----------`
`SQL Server Master Readable Secondary Replicas  13.64.238.24,31436  sql-server-master-readonly  tds`

### <a id="instance-connect"></a>Conexión a SQL Server instancia

Para ciertas operaciones como establecer configuraciones de nivel de servidor o agregar manualmente una base de datos al grupo de disponibilidad (en caso de que se creara la base de datos con un flujo de trabajo de restauración), se necesita una conexión a la instancia. Para proporcionar esta conexión, exponga un extremo externo. Este es un ejemplo que muestra cómo exponer este punto de conexión y, a continuación, agregar la base de datos que se creó con un flujo de trabajo de restauración al grupo de disponibilidad.

- Determine el POD que hospeda la réplica principal; para ello, conéctese al punto de conexión de `sql-server-master` y ejecute:

    ```sql
    SELECT @@SERVERNAME
   ```

- Exponer el punto de conexión externo mediante la creación de un nuevo servicio Kubernetes

    Para un clúster de kubeadm, ejecute el comando siguiente. Reemplace `podName` por el nombre del servidor devuelto en el paso anterior, `serviceName` con el nombre preferido para el servicio Kubernetes creado y `namespaceName` * por el nombre del clúster de BDC.

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=NodePort
    ```

    Para ejecutar un clúster de AKS, ejecute el mismo comando, con la salvedad de que el tipo de servicio creado se `LoadBalancer`. Por ejemplo: 

    ```bash
    kubectl -n <namespaceName> expose pod <podName> --port=1533  --name=<serviceName> --type=LoadBalancer
    ```

    Este es un ejemplo de este comando que se ejecuta en AKS, donde el POD que hospeda la principal está `master-0`:

    ```bash
    kubectl -n mssql-cluster expose pod master-0 --port=1533  --name=master-sql-0 --type=LoadBalancer
    ```

    Obtiene la dirección IP del servicio Kubernetes creado:

    ```bash
    kubectl get services -n <namespaceName>
    ```

> [!IMPORTANT]
> Como práctica recomendada, debe realizar la limpieza eliminando el servicio Kubernetes creado anteriormente con este comando:
>
>```bash
>kubectl delete svc master-sql-0 -n mssql-cluster
>```

- Agregue la base de datos al grupo de disponibilidad.

    Para que la base de datos se agregue al AG, debe ejecutarse en modo de recuperación completa y debe realizarse una copia de seguridad de registros. Use la dirección IP del servicio Kubernetes creado anteriormente y conéctese a la instancia de SQL Server y, a continuación, ejecute las instrucciones TSQL como se muestra a continuación.

    ```sql
    ALTER DATABASE <databaseName> SET RECOVERY FULL;
    BACKUP DATABASE <databaseName> TO DISK='<filePath>'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE <databaseName>
    ```

    En el ejemplo siguiente se agrega una base de datos denominada `sales` que se restauró en la instancia de:

    ```sql
    ALTER DATABASE sales SET RECOVERY FULL;
    BACKUP DATABASE sales TO DISK='/var/opt/mssql/data/sales.bak'
    ALTER AVAILABILITY GROUP containedag ADD DATABASE sales
    ```

## <a name="known-limitations"></a>Restricciones conocidas

Estos son los problemas conocidos y las limitaciones de los grupos de disponibilidad de SQL Server maestro en el clúster de macrodatos:

- Las bases de datos creadas como resultado de flujos de trabajo que no sean `CREATE DATABASE` como `RESTORE`, `CREATE DATABASE FROM SNAPSHOT` no se agregan automáticamente al grupo de disponibilidad. [Conéctese a la instancia](#instance-connect) y agregue la base de datos al grupo de disponibilidad manualmente.
- Ciertas operaciones, como la ejecución de la configuración del servidor con `sp_configure` requieren una conexión a la instancia maestra. No se puede usar el punto de conexión principal correspondiente. Siga [las instrucciones](#instance-connect) para conectarse a la instancia de SQL Server y ejecute `sp_configure`.
- La configuración de alta disponibilidad debe crearse cuando se implementa el BDC. No se puede habilitar la configuración de alta disponibilidad con grupos de disponibilidad después de la implementación.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre el uso de archivos de configuración en implementaciones de clúster de Big Data, consulte [cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md#configfile).
- Para obtener más información acerca de la característica de grupos de disponibilidad para SQL Server, consulte [información general de los grupos de disponibilidad de Always On (SQL Server)](https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2017).
