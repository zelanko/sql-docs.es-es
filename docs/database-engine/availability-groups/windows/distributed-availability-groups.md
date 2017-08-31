---
title: Grupos de disponibilidad distribuidos (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], distributed
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 80642503480add90fc75573338760ab86139694c
ms.openlocfilehash: 534cc0e8f798c8d231936e1c89835257832c4b16
ms.contentlocale: es-es
ms.lasthandoff: 08/21/2017

---
# <a name="distributed-availability-groups"></a>Grupos de disponibilidad distribuidos

Los grupos de disponibilidad distribuidos son una característica nueva que se incluyó en SQL Server 2016 como variante de la característica Grupos de disponibilidad AlwaysOn existente. En este artículo se aclaran algunos aspectos de los grupos de disponibilidad distribuidos y se complementa la [documentación de SQL Server](https://docs.microsoft.com/en-us/sql/sql-server/sql-server-technical-documentation) existente.

> [!NOTE]
> "DAG" no es la abreviatura oficial de *grupo de disponibilidad distribuido*, porque esa abreviatura ya se usa para hacer referencia a la característica de grupo de disponibilidad de base de datos de Exchange. Esta característica de Exchange no tiene relación alguna con los grupos de disponibilidad de SQL Server ni con los grupos de disponibilidad distribuidos.

Para configurar un grupo de disponibilidad distribuido, vea [Configure distributed availability groups](configure-distributed-availability-groups.md) (Configurar grupos de disponibilidad distribuidos).

## <a name="understand-distributed-availability-groups"></a>Conceptos de los grupos de disponibilidad distribuidos

Un grupo de disponibilidad distribuido es un tipo especial de grupo de disponibilidad que abarca dos tipos distintos de grupo de disponibilidad. Los grupos de disponibilidad subyacentes se configuran en dos clústeres de conmutación por error de Windows Server (WSFC) distintos. No es necesario que los grupos de disponibilidad que participan en un grupo de disponibilidad distribuido estén en la misma ubicación. Pueden ser físicos, virtuales, hospedarse localmente, en la nube pública o en cualquier lugar donde se puedan implementar grupos de disponibilidad. Siempre que dos grupos de disponibilidad puedan comunicarse, se podrá configurar un grupo de disponibilidad distribuido con ellos.

Los grupos de disponibilidad tradicionales tienen recursos configurados en un clúster WSFC, mientras que los grupos de disponibilidad distribuidos no tienen nada configurado en este tipo de clúster: todo se mantiene en SQL Server. Para más información sobre cómo consultar información relativa a un grupo de disponibilidad distribuido, vaya a [Ver la información de grupo de disponibilidad distribuido](#viewing-distributed-availability-group-information). 

Un grupo de disponibilidad distribuido requiere que los grupos de disponibilidad subyacentes tengan un agente de escucha. Al contrario de lo que haría en un grupo de disponibilidad tradicional, en vez de proporcionar el nombre de servidor subyacente de una instancia independiente (o, si se trata de una instancia de clúster de conmutación por error de SQL Server, el valor asociado al recurso de nombre de red), cuando se cree el grupo de disponibilidad distribuido hay que especificar el agente de escucha configurado por medio del parámetro ENDPOINT_URL. Aunque cada grupo de disponibilidad subyacente del grupo de disponibilidad distribuido tiene un agente de escucha, el grupo de disponibilidad distribuido carece de dicho agente.

En la siguiente imagen se muestra una vista de alto nivel de un grupo de disponibilidad distribuido que abarca dos grupos de disponibilidad (AG 1 y AG 2), cada uno de ellos configurado en su propio clúster WSFC. El grupo de disponibilidad distribuido tiene un total de cuatro réplicas, dos en cada grupo de disponibilidad. Cada grupo de disponibilidad tiene cabida para el número máximo de réplicas, con lo cual un grupo de disponibilidad distribuido basado en Standard Edition puede tener hasta cuatro réplicas, mientras que uno basado en Enterprise Edition puede tener hasta 18 réplicas en total.

<a name="fig1"></a>
![Vista de alto nivel de un grupo de disponibilidad distribuido][1]

El movimiento de datos en los grupos de disponibilidad distribuidos se puede configurar como sincrónico o como asincrónico. Con todo, el movimiento de datos en el caso de los grupos de disponibilidad distribuidos es ligeramente distinto al de los grupos de disponibilidad tradicionales. A pesar de que cada grupo de disponibilidad tiene una réplica principal, solo hay una copia de las bases de datos que participan en un grupo de disponibilidad distribuido que puede aceptar inserciones, actualizaciones y eliminaciones. Como se aprecia en la siguiente imagen, AG 1 es el grupo de disponibilidad principal. Su réplica principal envía transacciones tanto a las réplicas secundarias de AG 1 como a la réplica principal de AG 2. De esta forma, la réplica principal de AG 2 mantiene las réplicas secundarias de AG 2 actualizadas. 


![Grupo de disponibilidad distribuido y movimiento de datos][2]

La única manera de que la réplica principal de AG 2 acepte inserciones, actualizaciones y eliminaciones es conmutar por error el grupo de disponibilidad distribuido de AG 1 manualmente. En la imagen anterior, como AG 1 contiene la copia de la base de datos de escritura, cuando se realiza una conmutación por error, AG 2 se convierte en el grupo de disponibilidad que puede controlar las inserciones, actualizaciones y eliminaciones. Para más información sobre cómo realizar una conmutación por error de un grupo de disponibilidad distribuido a otro, vea [Conmutación por error a un grupo de disponibilidad secundario]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups).

> [!NOTE]
> En los grupos de disponibilidad distribuidos de SQL Server 2016, la conmutación por error de un grupo de disponibilidad a otro solo puede realizarse a través de la opción FORCE_FAILOVER_ALLOW_DATA_LOSS.

## <a name="sql-server-version-and-edition-requirements-for-distributed-availability-groups"></a>Requisitos de versión y edición de SQL Server de los grupos de disponibilidad distribuidos

Actualmente, los grupos de disponibilidad distribuidos solo funcionan con grupos de disponibilidad que se hayan creado con la misma versión principal de SQL Server. Así, en la actualidad todos los grupos de disponibilidad que participan en un grupo de disponibilidad distribuido deben crearse con SQL Server 2016. Dado que la característica de grupos de disponibilidad distribuidos no existía en SQL Server 2012 ni en 2014, los grupos de disponibilidad que se crearon con esas versiones no pueden participar en grupos de disponibilidad distribuidos. 

> [!NOTE]
> Los grupos de disponibilidad distribuidos se pueden configurar con las ediciones Enterprise o Standard, pero no admiten la combinación de ediciones.

Dado que hay dos grupos de disponibilidad diferentes, el proceso para instalar un Service Pack o una actualización acumulativa en una réplica que participa en un grupo de disponibilidad distribuido es ligeramente diferente del de un grupo de disponibilidad tradicional:

1. Empiece actualizando las réplicas del segundo grupo de disponibilidad del grupo de disponibilidad distribuido.

2. Aplique revisiones a las réplicas del grupo de disponibilidad principal del grupo de disponibilidad distribuido.

3. Como haría con un grupo de disponibilidad estándar, conmute por error el grupo de disponibilidad principal a una de sus propias réplicas (y no a la réplica principal del segundo grupo de disponibilidad) y aplíquele las revisiones pertinentes. Si no hay ninguna réplica aparte de la principal, será necesario realizar una conmutación por error manual al segundo grupo de disponibilidad.

> [!NOTE]
> No hay ningún anuncio relativo a si en futuras versiones de SQL Server se va a permitir que las versiones anteriores puedan participar en el mismo grupo de disponibilidad distribuido. Si este escenario fuera factible, permitiría que los grupos de disponibilidad distribuidos formaran parte de un plan de actualización de versión de SQL Server.

### <a name="windows-server-versions-and-distributed-availability-groups"></a>Grupos de disponibilidad distribuidos y versiones de Windows Server

Un grupo de disponibilidad distribuido abarca varios grupos de disponibilidad (cada uno en su propio clúster WSFC subyacente) y es además una construcción solo de SQL Server.  Esto significa que los clústeres WSFC que hospedan grupos de disponibilidad individuales pueden tener versiones principales de Windows Server distintas. Las versiones principales de SQL Server deben ser la misma, como se ha indicado en la sección anterior. De forma bastante parecida a [la imagen inicial](#fig1), la siguiente imagen muestra los grupos AG 1 y AG 2 que participan en un grupo de disponibilidad distribuido, pero cada clúster WSFC pertenece a una versión de Windows Server distinta.


![Grupos de disponibilidad distribuidos con clústeres WSFC con distintas versiones de Windows Server][3]

Los clústeres WSFC individuales y sus correspondientes grupos de disponibilidad siguen las reglas tradicionales; es decir, pueden estar o no unidos a un dominio (Windows Server 2016 o posterior). Cuando dos grupos de disponibilidad diferentes se combinan en un único grupo de disponibilidad distribuido, hay cuatro escenarios posibles:

* Ambos clústeres WSFC están unidos al mismo dominio.
* Cada clúster WSFC está unido a un dominio distinto.
* Un clúster WSFC está unido a un dominio y el otro no.
* Ninguno de los dos clústeres WSFC está unido a un dominio.

Cuando ambos clústeres WSFC están unidos al mismo dominio (dominios que no son de confianza), no es necesario hacer nada especial al crear el grupo de disponibilidad distribuido. En el caso de los grupos de disponibilidad y clústeres WSFC que no están unidos al mismo dominio, use certificados para que el grupo de disponibilidad distribuido funcione, como haría en gran medida al crear un grupo de disponibilidad para un grupo de disponibilidad independiente del dominio. Para saber cómo configurar certificados para un grupo de disponibilidad distribuido, siga los pasos 3-13 de [Create a domain-independent availability group](domain-independent-availability-groups.md#create-a-domain-independent-availability-group) (Crear un grupo de disponibilidad independiente del dominio).

En un grupo de disponibilidad distribuido, las réplicas principales de cada grupo de disponibilidad subyacente deben tener los certificados de todas las demás. Si ya tiene puntos de conexión que no usan certificados, reconfigure esos puntos de conexión con [ALTER ENDPOINT](https://docs.microsoft.com/en-us/sql/t-sql/statements/alter-endpoint-transact-sql) para reflejar el uso de certificados.

## <a name="distributed-availability-group-usage-scenarios"></a>Escenarios de uso de grupos de disponibilidad distribuidos

Estos son los tres escenarios más importantes de uso de un grupo de disponibilidad distribuido: 

* [Recuperación ante desastres y configuraciones de varios sitios más sencillas](#disaster-recovery-and-multi-site-scenarios)
* [Migración a un nuevo hardware o nuevas configuraciones, lo que puede conllevar el uso de hardware nuevo o el cambio de los sistemas operativos subyacentes](#migration-using-a-distributed-availability-group)
* [Expansión de varios grupos de disponibilidad para aumentar el número de réplicas legibles a más de ocho en un mismo grupo de disponibilidad](#scaling-out-readable-replicas-with-distributed-accessibility-groups)

### <a name="disaster-recovery-and-multi-site-scenarios"></a>Escenarios de recuperación ante desastres y configuraciones de varios sitios

Un grupo de disponibilidad tradicional requiere que todos los servidores formen parte del mismo clúster WSFC, de modo que la expansión de varios centros de datos puede suponer un desafío. En la siguiente imagen se muestra cómo es una arquitectura de grupo de disponibilidad tradicional de varios sitios, incluido el flujo de datos. No hay una réplica principal que envíe transacciones a todas las réplicas secundarias. Esta configuración es menos flexible en cierto modo que la de un grupo de disponibilidad distribuido. Por ejemplo, deberá implementar elementos como Active Directory (si procede) y el testigo de un cuórum en el clúster WSFC. También tendrá que tener en cuenta otros aspectos de un clúster WSFC, como modificar los votos de nodos.

![Grupo de disponibilidad tradicional de varios sitios][4]

Los grupos de disponibilidad distribuidos ofrecen un escenario de implementación más flexible para los grupos de disponibilidad que abarcan varios centros de datos. Se pueden usar grupos de disponibilidad distribuidos donde antes se usaban características como el [trasvase de registros]( https://docs.microsoft.com/en-us/sql/database-engine/log-shipping/about-log-shipping-sql-server). Pero, a diferencia de los grupos de disponibilidad tradicionales, en los grupos de disponibilidad distribuidos no se puede retrasar la aplicación de transacciones. Esto significa que estos grupos no son de ayuda en caso de que se cometa un error humano por el cual se actualizan o eliminan datos incorrectamente.

El emparejamiento de los grupos de disponibilidad distribuidos no es muy fuerte, lo que se traduce en que no necesitan un único clúster WSFC. Se mantienen en SQL Server. Dado que los clústeres WSFC se mantienen individualmente y la sincronización es básicamente asincrónica entre los dos grupos de disponibilidad, es más fácil configurar la recuperación ante desastres en otro sitio. Las réplicas principales de cada grupo de disponibilidad sincronizan sus propias réplicas secundarias.

* Los grupos de disponibilidad distribuidos solo admiten la conmutación por error manual. En una situación de recuperación ante desastres donde se intercambian centros de datos, conviene no configurar la conmutación automática por error (salvo raras excepciones). 
* Probablemente no necesitará establecer algunos de los elementos o parámetros tradicionales de los clústeres WSFC de varios sitios o subred (como CrossSubnetThreshold), pero sí sigue siendo necesario tener presente la latencia de red en una capa diferente para el transporte de datos. La diferencia es que cada clúster WSFC mantiene su propia disponibilidad; el clúster no es una gran entidad de cuatro nodos. Existen dos clústeres WSFC de dos nodos independientes, como muestra la imagen anterior.  
* Recomendamos el movimiento de datos asincrónico, porque con este método la recuperación ante desastres sería viable.
* Si configura un movimiento de datos sincrónico entre la réplica principal y, al menos, una réplica secundaria del segundo grupo de disponibilidad y un movimiento sincrónico en el grupo de disponibilidad distribuido, el grupo de disponibilidad distribuido esperará hasta que todas las copias sincrónicas confirmen que tienen los datos.

### <a name="migrate-by-using-a-distributed-availability-group"></a>Migrar por medio de un grupo de disponibilidad distribuido

Los grupos de disponibilidad distribuidos admiten dos configuraciones de grupo de disponibilidad completamente diferentes, lo que permite no solo escenarios de varios sitios y de recuperación ante desastres más sencillos, sino también escenarios de migración. Tanto si va a migrar a un nuevo hardware o máquinas virtuales (locales o IaaS en la nube pública), la configuración de un grupo de disponibilidad distribuido facilita una migración cuando, anteriormente, había que recurrir a trabajos de copia de seguridad, copia y restauración o al trasvase de registros. 

La capacidad de migrar es especialmente útil en escenarios donde el sistema operativo subyacente se va a cambiar o a actualizar mientras se mantiene la misma versión de SQL Server. Si bien Windows Server 2016 permite una actualización gradual desde Windows Server 2012 R2 en el mismo hardware, la mayoría de los usuarios opta por implementar nuevo hardware o máquinas virtuales. 

Para completar la migración a la nueva configuración, cuando el proceso llegue a su fin, detenga todo el tráfico de datos al grupo de disponibilidad original y cambie el grupo de disponibilidad distribuido al movimiento de datos sincrónico. Con ello, se garantiza que la réplica principal del segundo grupo de disponibilidad va a estar completamente sincronizada, sin perder ningún dato. Tras comprobar la sincronización, conmute por error el grupo de disponibilidad distribuido al grupo de disponibilidad secundario. Para obtener más información, consulte [Fail over to a secondary availability group (Conmutación por error de un grupo de disponibilidad secundario)](configure-distributed-availability-groups.md#failover).

Después de la migración, cuando el segundo grupo de disponibilidad es ya el nuevo grupo de disponibilidad principal, es posible que tenga que realizar una de las siguientes acciones:

* Cambiar el nombre del agente de escucha del grupo de disponibilidad secundario (y, posiblemente, eliminar el agente anterior del grupo de disponibilidad principal original o cambiarlo de nombre) o volver a crearlo con el agente de escucha del grupo de disponibilidad principal original, de forma que las aplicaciones y los usuarios puedan acceder a la nueva configuración.
* Si no puede volver a crearlo ni cambiarlo de nombre, dirija las aplicaciones y los usuarios al agente de escucha del segundo grupo de disponibilidad.

### <a name="scale-out-readable-replicas-with-distributed-availability-groups"></a>Escalar horizontalmente réplicas legibles con grupos de disponibilidad distribuidos

Un solo grupo de disponibilidad distribuido puede tener hasta 16 réplicas secundarias legibles. Esto significa que puede tener hasta 18 copias de lectura, si incluimos las dos réplicas principales de los diferentes grupos de disponibilidad. Este método permite que más de un sitio pueda tener acceso casi en tiempo real para notificar a diversas aplicaciones.

Con los grupos de disponibilidad distribuidos, el escalado horizontal de una granja de servidores de solo lectura es más fácil que con simplemente un único grupo de disponibilidad. Un grupo de disponibilidad distribuido puede escalar réplicas legibles horizontalmente de dos maneras:

* Se puede usar la réplica principal del segundo grupo de disponibilidad de un grupo de disponibilidad distribuido para crear otro grupo de disponibilidad distribuido, aun cuando la base de datos no esté en estado RECOVERY.
* También puede usar la réplica principal del primer grupo de disponibilidad para crear otro grupo de disponibilidad distribuido.

Dicho de otro modo, una réplica principal puede participar en dos grupos de disponibilidad distribuidos diferentes. En la siguiente imagen se muestran dos grupos, AG 1 y AG 2, y ambos participan en el grupo distribuido AG 1, mientras que AG 2 y AG 3 participan en el grupo distribuido AG 2. La réplica principal de AG 2 es al mismo tiempo una réplica secundaria del grupo Distributed AG 1 y la réplica principal del grupo Distributed AG 2.

![Escalar lecturas horizontalmente con grupos de disponibilidad distribuidos][5]

En la siguiente imagen, AG 1 es la réplica principal de dos grupos de disponibilidad distribuidos diferentes: Distributed AG 1 (compuesto por AG 1 y AG 2) y Distributed AG 2 (compuesto por AG 1 y AG 3).


![Otro ejemplo de escalado horizontal de lecturas con grupos de disponibilidad distribuidos][6]


En los dos ejemplos anteriores, puede haber hasta 27 réplicas en total entre los tres grupos de disponibilidad, y todas ellas se pueden usar para consultas de solo lectura. 

Actualmente, el [enrutamiento de solo lectura]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server) no funciona con los grupos de disponibilidad distribuidos. Si usan el agente de escucha para conectarse, todas las consultas van a la réplica principal. Si no, tendrá que configurar cada réplica para permitir todas las conexiones como una réplica secundaria y tener acceso a ellas directamente. Este comportamiento podría cambiar en una actualización de SQL Server 2016 o en una versión futura de SQL Server.

## <a name="initialize-secondary-availability-groups-in-a-distributed-availability-group"></a>Inicializar grupos de disponibilidad secundarios en un grupo de disponibilidad distribuido

Los grupos de disponibilidad distribuidos están diseñados con la [propagación automática]( https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group) como método principal para inicializar la réplica principal en el segundo grupo de disponibilidad. Si hace lo siguiente, realizará una restauración de base de datos completa en la réplica principal del segundo grupo de disponibilidad:

1. Restaure las copias de seguridad de las bases de datos con WITH NORECOVERY.
2. Si procede, restaure las copias de seguridad de registro de transacciones apropiadas con WITH NORECOVERY.
3. Cree el segundo grupo de disponibilidad sin especificar un nombre de base de datos y con SEEDING_MODE establecido en AUTOMATIC.
4. Cree el grupo de disponibilidad distribuido por medio de la propagación automática.

Cuando la réplica principal del segundo grupo de disponibilidad se agrega al grupo de disponibilidad distribuido, dicha réplica se compara con las bases de datos principales del primer grupo de disponibilidad y la propagación detecta la base de datos hasta el origen. Existen varios inconvenientes:

* El resultado que consta en `sys.dm_hadr_automatic_seeding` en la réplica principal del segundo grupo de disponibilidad mostrará `current_state` como FAILED con el motivo "Seeding Check Message Timeout" (se agotó el tiempo de espera del mensaje de comprobación de propagación).

* El registro de SQL Server actual de la réplica principal del segundo grupo de disponibilidad reflejará que la propagación ha funcionado y que los [LSN]( https://docs.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-log-architecture-and-management-guide) se sincronizaron.

* El resultado que consta en `sys.dm_hadr_automatic_seeding` en la réplica principal del primer grupo de disponibilidad mostrará current_state como COMPLETED. 

* La propagación tiene un comportamiento distinto también con los grupos de disponibilidad distribuidos. Para que la propagación comience en la segunda réplica, hay que emitir el comando `ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE` en la réplica. Aunque esto sigue siendo así en cualquier réplica secundaria que participa en el grupo de disponibilidad subyacente, la réplica principal del segundo grupo de disponibilidad ya tiene los permisos adecuados para permitir que la propagación se inicie después de que se haya agregado al grupo de disponibilidad distribuido. 

### <a name="view-distributed-availability-group-information"></a>Ver la información de grupo de disponibilidad distribuido 
    
Tal y como se ha dicho antes, un grupo de disponibilidad distribuido es una construcción solo de SQL Server y no se ve en el clúster WSFC subyacente. En la siguiente imagen aparecen dos clústeres WSFC distintos (CLUSTER_A y CLUSTER_B), cada uno con sus propios grupos de disponibilidad. Aquí solo nos centraremos en AG1 en CLUSTER_A y en AG2 en CLUSTER_B. 

<!-- ![Two WSFC clusters with multiple availability groups through PowerShell Get-ClusterGroup command][7]  -->
<a name="fig7"></a>

```
PS C:\> Get-ClusterGroup -Cluster CLUSTER_A

Name                            OwnerNode             State
----                            ---------             -----
AG1                             DENNIS                Online
Available Storage               GLEN                  Offline
Cluster Group                   JY                    Online
New_RoR                         DENNIS                Online
Old_RoR                         DENNIS                Online
SeedingAG                       DENNIS                Online


PS C:\> Get-ClusterGroup -Cluster CLUSTER_B

Name                            OwnerNode             State
----                            ---------             -----
AG2                             TOMMY                 Online
Available Storage               JC                    Offline
Cluster Group                   JC                    Online
```

Toda la información detallada sobre un grupo de disponibilidad distribuido está en SQL Server, concretamente en las vistas de administración dinámica de grupos de disponibilidad. Actualmente, la única información que se muestra en SQL Server Management Studio sobre un grupo de disponibilidad distribuido está disponible en la réplica principal de los grupos de disponibilidad. Tal como se muestra en la figura siguiente, en la carpeta Grupos de disponibilidad, SQL Server Management Studio muestra que hay un grupo de disponibilidad distribuido. La figura muestra GD1 como una réplica principal de un grupo de disponibilidad específico que se encuentra en la instancia en lugar de un grupo de disponibilidad distribuido.

![Vista de la réplica principal del primer clúster WSFC de un grupo de disponibilidad distribuido en SQL Server Management Studio][8]


En cambio, si hace clic con el botón derecho en el grupo de disponibilidad distribuido, no se mostrará ninguna opción (consulte la figura siguiente), mientras que las carpetas expandidas Bases de datos de disponibilidad, Agentes de escucha de grupos de disponibilidad y Réplicas de disponibilidad estarán vacías. SQL Server Management Studio 16 muestra este resultado, pero puede cambiar en una versión futura de la herramienta.

![No hay opciones disponibles para la acción][9]

Tal como se muestra en la figura siguiente, las réplicas secundarias no muestran ningún elemento relacionado con el grupo de disponibilidad distribuido en SQL Server Management Studio. Estos nombres de grupo de disponibilidad se ajustan a los roles que se muestran en la imagen anterior, [Clúster WSFC CLUSTER_A](#fig7).

![Vista de una réplica secundaria en SQL Server Management Studio][10]

Al usar las vistas de administración dinámica, se aplican los mismos conceptos. Mediante el uso de la consulta siguiente, puede ver todos los grupos de disponibilidad (normales y distribuidos), así como los nodos implicados. Este resultado se muestra solo si realiza una consulta a la réplica principal en uno de los clústeres WSFC que forman parte del grupo de disponibilidad distribuido. Hay una nueva columna en la vista de administración dinámica `sys.availability_groups` denominada `is_distributed`, que es 1 cuando el grupo de disponibilidad es del tipo distribuido. Para ver esta columna:

```sql
SELECT ag.[name] as 'AG Name', 
    ag.Is_Distributed, 
    ar.replica_server_name as 'Replica Name'
FROM    sys.availability_groups ag, 
    sys.availability_replicas ar       
WHERE   ag.group_id = ar.group_id
```

En la figura siguiente se muestra un ejemplo de salida desde el segundo clúster WSFC que participa en un grupo de disponibilidad distribuido. SPAG1 se compone de dos réplicas: DENNIS y JY. En cambio, el grupo de disponibilidad distribuido denominado SPDistAG contiene los nombres de los dos grupos de disponibilidad implicados (SPAG1 y SPAG2) en lugar de los nombres de las instancias, al igual que sucede con un grupo de disponibilidad tradicional. 

![Ejemplo de salida de la consulta anterior][11]

En SQL Server Management Studio, cualquier tipo de estado que se muestra en el panel y en otras áreas está diseñado para la sincronización local solo dentro del grupo de disponibilidad. Para mostrar el estado de un grupo de disponibilidad distribuido, consulte las vistas de administración dinámica. La consulta de ejemplo siguiente amplía y mejora la consulta anterior:

```sql
SELECT ag.[name] as 'AG Name', ag.is_distributed, ar.replica_server_name as 'Underlying AG', ars.role_desc as 'Role', ars.synchronization_health_desc as 'Sync Status'
FROM    sys.availability_groups ag, 
sys.availability_replicas ar,       
sys.dm_hadr_availability_replica_states ars       
WHERE   ar.replica_id = ars.replica_id
and     ag.group_id = ar.group_id 
and ag.is_distributed = 1
```
       
       
![Estado del grupo de disponibilidad distribuido][12]


Para ampliar aún más la consulta anterior, también puede ver el rendimiento subyacente mediante las vistas de administración dinámica agregando `sys.dm_hadr_database_replicas_states`. La vista de administración dinámica actualmente solo almacena información sobre el segundo grupo de disponibilidad. La consulta de ejemplo siguiente, al ejecutarse en el grupo de disponibilidad principal, genera el resultado de ejemplo que se muestra a continuación:

```
SELECT ag.[name] as 'Distributed AG Name', ar.replica_server_name as 'Underlying AG', dbs.[name] as 'DB', ars.role_desc as 'Role', drs.synchronization_health_desc as 'Sync Status', drs.log_send_queue_size, drs.log_send_rate, drs.redo_queue_size, drs.redo_rate
FROM    sys.databases dbs,
    sys.availability_groups ag,
    sys.availability_replicas ar,
    sys.dm_hadr_availability_replica_states ars,
    sys.dm_hadr_database_replica_states drs
WHERE   drs.group_id = ag.group_id
and ar.replica_id = ars.replica_id
and ars.replica_id = drs.replica_id
and dbs.database_id = drs.database_id
and ag.is_distributed = 1
```

![Información sobre el rendimiento de un grupo de disponibilidad distribuido][13]


### <a name="next-steps"></a>Pasos siguientes 

* [Usar el Asistente para grupo de disponibilidad (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

* [Usar el cuadro de diálogo Nuevo grupo de disponibilidad (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
* [Crear un grupo de disponibilidad (Transact-SQL)](create-an-availability-group-transact-sql.md)

Contenido escrito por [Allan Hirt](http://mvp.microsoft.com/en-us/PublicProfile/4025254?fullName=Allan%20Hirt), profesional más valioso (MVP) de Microsoft.

<!--Image references-->
[1]: ./media/dag-01-high-level-view-distributed-ag.png
[2]: ./media/dag-02-distributed-ag-data-movement.png
[3]: ./media/dag-03-distributed-ags-wsfcs-different-versions-windows-server.png
[4]: ./media/dag-04-traditional-multi-site-ag.png
[5]: ./media/dag-05-scaling-out-reads-with-distributed-ags.png
[6]: ./media/dag-06-another-scaling-out-reads-using-distributed-ags-example.png
[7]: ./media/dag-07-two-wsfcs-multiple-ags-through-get-clustergroup-command.png
[8]: ./media/dag-08-view-smss-primary-replica-first-wsfc-distributed-ag.png
[9]: ./media/dag-09-no-options-available-action.png
[10]: ./media/dag-10-view-ssms-secondary-replica.png
[11]: ./media/dag-11-example-output-of-query-above.png
[12]: ./media/dag-12-distributed-ag-status.png
[13]: ./media/dag-13-performance-information-distributed-ag.png

 

