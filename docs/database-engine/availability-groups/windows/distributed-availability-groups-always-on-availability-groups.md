---
title: "Grupos de disponibilidad distribuidos (grupos de disponibilidad AlwaysOn) | Microsoft Docs"
ms.custom: ""
ms.date: "08/30/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7c7acc5-a350-4a17-95e1-e689c78a0900
caps.latest.revision: 28
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 28
---
# Grupos de disponibilidad distribuidos (grupos de disponibilidad AlwaysOn)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gracias a los grupos de disponibilidad distribuidos, podrá asociar dos grupos de disponibilidad que residan en diferentes clústeres de conmutación por error de Windows Server (WSFC). Uno de los usos principales de los grupos de disponibilidad distribuidos es realizar tareas de recuperación ante desastres en las que el sitio principal está alejado geográficamente del de recuperación ante desastres. Quiere que los datos se repliquen continuamente en el sitio de recuperación ante desastres, pero no desea que un posible problema de red en dicho sitio provoque que el principal quede fuera de servicio.  
  
 En el siguiente diagrama se ilustra la arquitectura de un grupo de disponibilidad distribuido.  
  
 ![AlwaysOn Distributed Availability Groups](../../../database-engine/availability-groups/windows/media/alwayson-distributed-availability-groups.png "AlwaysOn Distributed Availability Groups")  
  
 En el diagrama anterior, hay dos clústeres de conmutación por error de Windows Server (WFSC 1 y WFSC 2). Cada clúster tiene su propio grupo de disponibilidad con una configuración coincidente de bases de datos. Un grupo de disponibilidad distribuido puede considerarse un "grupo de disponibilidad de grupos de disponibilidad". AG 1 se convierte en el grupo de disponibilidad principal en este ejemplo. Todas las inserciones y actualizaciones se realizan a la réplica principal, AG 1 y, a después, se replican en sus secundarias. Sin embargo, también se replican una vez los cambios al grupo de disponibilidad secundario de WSFC 2 a través de la red. El grupo de disponibilidad AG 2 replica esos cambios en sus réplicas secundarias.  
  
> [!IMPORTANT]  
>  Cuando se establece una relación de grupo de disponibilidad distribuidos entre dos grupos de disponibilidad, el de disponibilidad secundaria se convierte automáticamente en solo lectura. Las actualizaciones e inserciones solo pueden realizarse en la réplica principal del grupo de disponibilidad principal (en este ejemplo, la réplica principal de AG 1).  
  
 Los grupos de disponibilidad distribuidos se diferencian de un grupo de disponibilidad de un único clúster de conmutación por error de Windows Server de las siguientes formas:  
  
-   Cada WSFC mantiene su propio modo de cuórum y la configuración de votación de nodos. Es decir, el estado del WSFC secundario no afecta al principal.  
  
-   Los datos se envían una vez a través de la red al WSFC secundario y, después, se replican dentro de ese clúster. En un único WSFC, los datos se envían individualmente a cada réplica. En lo que respecta a los sitios secundarios alejados geográficamente, los grupos de disponibilidad distribuidos son más eficaces.  
  
-   La versión del sistema operativo que se utiliza en los clústeres principales y secundarios puede diferir. En un único WSFC, todos los servidores deben tener la misma versión del sistema operativo. De este modo, se pueden usar grupos de disponibilidad distribuidos con actualizaciones graduales del sistema operativo.  
  
-   Los grupos de disponibilidad principal y secundario deben tener la misma configuración de bases de datos.  
  
-   No se admite la conmutación por error automática al grupo de disponibilidad secundario.  
  
## Creación de un grupo de disponibilidad distribuido  
 Para crear un grupo de disponibilidad distribuido, debe crear un grupo de disponibilidad y el agente de escucha en cada WSFC. Después, combine estos elementos en un grupo de disponibilidad distribuido. En los pasos siguientes se proporciona un ejemplo básico de Transact-SQL. En este ejemplo no se cubren toda la información relativa a la creación de grupos de disponibilidad y agentes de escucha; en su lugar, se centra en resaltar los requisitos clave.  
  
### Creación del grupo de disponibilidad principal en el primer clúster  
 Crear un grupo de disponibilidad en el primer WSFC.   En este ejemplo, el grupo de disponibilidad se denomina `ag1` en la base de datos `db1`.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag1]   
FOR DATABASE db1   
REPLICA ON N'server1' WITH (ENDPOINT_URL = N'TCP://server1.contoso.com:5022',  
    FAILOVER_MODE = AUTOMATIC,  
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server2' WITH (ENDPOINT_URL = N'TCP://server2.contoso.com:5022',   
    FAILOVER_MODE = AUTOMATIC,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
  
```  
  
 Tenga en cuenta que en este ejemplo se emplea la propagación directa, donde el valor **SEEDING_MODE** se establece en **AUTOMATIC** para las réplicas y el grupo de disponibilidad distribuido. Es decir, cuando se establece el valor, las réplicas secundarias y el grupo de disponibilidad secundario se rellenarán automáticamente sin requerir una copia de seguridad manual y la restauración de la base de datos principal.  
  
### Unión de las réplicas secundarias al grupo de disponibilidad principal  
 Cualquier réplica secundaria debe estar unida al grupo de disponibilidad mediante **ALTER AVAILABILITY GROUP** con la opción **JOIN** . Como en este ejemplo se utiliza la propagación directa, también se debe llamar a  **ALTER AVAILABILITY GROUP** con la opción **GRANT CREATE ANY DATABASE** . De esta forma, el grupo de disponibilidad puede crear la base de datos y comenzar la propagación automáticamente a partir de la réplica principal.  
  
 En este ejemplo, se ejecutan los comandos siguientes en la réplica secundaria, `server2`, para unir el grupo de disponibilidad `ag1` . Después, el grupo de disponibilidad puede crear bases de datos en la secundaria.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag1] JOIN   
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Creación de un agente de escucha para el grupo de disponibilidad principal  
 Luego, agregue un agente de escucha para el grupo de disponibilidad principal del primer WSFC. En este ejemplo, el agente de escucha se denomina " `ag1-listener`". Para obtener instrucciones detalladas sobre cómo crear un agente de escucha, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag1]    
    ADD LISTENER 'ag1-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Creación del grupo de disponibilidad secundario en el segundo clúster  
 Después, en el segundo WSFC, cree un segundo grupo de disponibilidad, `ag2`. En este caso, no se especifica la base de datos, porque se propagará automáticamente desde el grupo de disponibilidad principal.  
  
```tsql  
CREATE AVAILABILITY GROUP [ag2]   
FOR   
REPLICA ON N'server3' WITH (ENDPOINT_URL = N'TCP://server3.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC),   
N'server4' WITH (ENDPOINT_URL = N'TCP://server4.contoso.com:5022',   
    FAILOVER_MODE = MANUAL,   
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,   
    BACKUP_PRIORITY = 50,   
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO),   
    SEEDING_MODE = AUTOMATIC);   
GO  
```  
  
> [!NOTE]  
>  Tenga en cuenta que el grupo de disponibilidad secundario debe utilizar el mismo punto de conexión de creación de reflejo de la base de datos (en este ejemplo, el puerto 5022). En caso contrario, se detendrá la replicación después de una conmutación por error local.  
  
### Unión de las réplicas secundarias al grupo de disponibilidad secundario  
 En este ejemplo, se ejecutan los comandos siguientes en la réplica secundaria, `server4`, para unir el grupo de disponibilidad `ag2` . Después, el grupo de disponibilidad puede crear bases de datos en la secundaria con el fin de admitir la propagación directa.  
  
```tsql  
ALTER AVAILABILITY GROUP [ag2] JOIN   
ALTER AVAILABILITY GROUP [ag2] GRANT CREATE ANY DATABASE  
GO  
```  
  
### Creación de un agente de escucha para el grupo de disponibilidad secundario  
 Después, agregue un agente de escucha para el grupo de disponibilidad secundaria del segundo WSFC. En este ejemplo, el agente de escucha se denomina " `ag2-listener`". Para obtener instrucciones detalladas sobre cómo crear un agente de escucha, vea [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
```  
ALTER AVAILABILITY GROUP [ag2]    
    ADD LISTENER 'ag2-listener' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173);    
GO  
```  
  
### Creación del grupo de disponibilidad distribuido en el primer clúster  
 En el primer WSFC, cree un grupo de disponibilidad distribuido (denominado "`distributedag`" en este ejemplo). Utilice el comando **CREATE AVAILABILITY GROUP** con la opción **DISTRIBUTED** . El parámetro **AVAILABILITY GROUP ON** especifica los grupos de disponibilidad de los miembros, `ag1` y `ag2`.  
  
```tsql  
CREATE AVAILABILITY GROUP [distributedag]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO   
```  
  
> [!NOTE]  
>  **LISTENER_URL** especifica el agente de escucha de cada grupo de disponibilidad, con el punto de conexión de creación de reflejo de la base de datos del grupo de disponibilidad. En este ejemplo, es el puerto `5022` (no el puerto `60173` usado para crear el agente de escucha).  
  
### Unión al grupo de disponibilidad distribuido en el segundo clúster  
 Después, únase al grupo de disponibilidad distribuido del segundo WSFC.  
  
```tsql  
ALTER AVAILABILITY GROUP [distributedag]   
   JOIN   
   AVAILABILITY GROUP ON  
      'ag1' WITH    
      (   
         LISTENER_URL = 'tcp://ag1-listener:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      ),   
      'ag2' WITH    
      (   
         LISTENER_URL = 'tcp://ag2-listener:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC   
      );    
GO  
```  

  
## Conmutación por error a un grupo de disponibilidad secundario  
 En estos momentos, solo se admite la conmutación por error manual. La siguiente instrucción Transact-SQL fuerza la conmutación por error al grupo de disponibilidad distribuido denominado "`distributedag`":  


1. Establezca el modo de disponibilidad en confirmación sincrónica para el grupo de disponibilidad secundaria. 
    
      ```tsql  
      ALTER AVAILABILITY GROUP [distributedag] 
      MODIFY 
      AVAILABILITY GROUP ON
      'ag1' WITH  
         ( 
          LISTENER_URL = 'tcp://ag1-listener:5022',  
          AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = MANUAL, 
          SEEDING_MODE = MANUAL 
          ), 
      'ag2' WITH  
        ( 
        LISTENER_URL = 'tcp://ag2-listener:5022', 
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
        FAILOVER_MODE = MANUAL, 
        SEEDING_MODE = MANUAL 
        );  
       
      ```  
  
1. Espere hasta que el estado del grupo de disponibilidad distribuida haya cambiado a `SYNCHRONIZED`. Ejecute la siguiente consulta en SQL Server que hospeda la réplica principal del grupo de disponibilidad principal. 
    
      ```tsql  
      SELECT ag.name
             , drs.database_id
             , drs.group_id
             , drs.replica_id
             , drs.synchronization_state_desc
             , drs.end_of_log_lsn 
        FROM sys.dm_hadr_database_replica_states drs,
        sys.availability_groups ag
          WHERE drs.group_id = ag.group_id;      
      ```  

    Continúe después de que el grupo de disponibilidad **synchronization_state_desc** sea `SYNCHRONIZED`. Si **synchronization_state_desc** no es `SYNCHRONIZED`, ejecute el comando cada cinco segundos hasta que cambie. No continúe hasta **synchronization_state_desc** = `SYNCHRONIZED`. 

1. En SQL Server que hospeda la réplica principal para el grupo de disponibilidad principal, establezca el rol de grupo de disponibilidad distribuido en `SECONDARY`. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag SET (ROLE = SECONDARY); 
      ```  

    Nota: En este punto, el grupo de disponibilidad distribuida no está disponible.

1. Pruebe la preparación de la conmutación por error. Ejecute la siguiente consulta:

      ```tsql
      SELECT ag.name, 
             drs.database_id, 
             drs.group_id, 
             drs.replica_id, 
             drs.synchronization_state_desc, 
             drs.end_of_log_lsn 
      FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
      WHERE drs.group_id = ag.group_id; 
      ```  
    El grupo de disponibilidad está preparado para la conmutación por error cuando **synchronization_state_desc** es `SYNCHRONIZED` y **end_of_log_lsn** es igual para ambos grupos de disponibilidad. 

1. Conmute por error desde el grupo de disponibilidad principal al grupo de disponibilidad secundario. Ejecute el siguiente comando en SQL Server que hospeda la réplica principal para el grupo de disponibilidad principal. 

      ```tsql
      ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
      ```  
      Nota: Después de este paso, el grupo de disponibilidad distribuido no está disponible.
      
Después de completar los pasos anteriores, el grupo de disponibilidad distribuido conmuta por error sin pérdida de datos. Microsoft recomienda cambiar el modo de disponibilidad a ASYNCHRONOUS_COMMIT si los grupos de disponibilidad se encuentran a una distancia geográfica que provoca latencia. 
  
## Eliminación de un grupo de disponibilidad distribuido  
 La siguiente instrucción Transact-SQL quita un grupo de disponibilidad distribuido denominado "`distributedag`":  
  
```tsql  
DROP AVAILABILITY GROUP [distributedag]  
```  

## Creación de un grupo de disponibilidad distribuido con instancias del clúster de conmutación por error

Puede crear un grupo de disponibilidad distribuido mediante un grupo de disponibilidad en una instancia de clúster de conmutación por error (FCI). En este caso, no necesita un agente de escucha del grupo de disponibilidad. Use el nombre de red virtual (VNN) para la réplica principal de la instancia FCI. El ejemplo siguiente muestra un grupo de disponibilidad distribuido llamado SQLFCIDAG. Un grupo de disponibilidad es SQLFCIAG. SQLFCIAG tiene 2 réplicas FCI. El VNN para la réplica FCI principal es SQLFCIAG-1 y el VNN para la réplica FCI secundaria es SQLFCIAG-2. El grupo de disponibilidad distribuido también incluye SQLAG-DR, para recuperación ante desastres.

![Grupo de disponibilidad distribuido AlwaysOn](../../../database-engine/availability-groups/windows/media/always-on-availability-group-distributed.png)

 
 
 El siguiente DDL crea este grupo de disponibilidad distribuido. 

```tsql  
CREATE AVAILABILITY GROUP [SQLFCIDAG]  
   WITH (DISTRIBUTED)   
   AVAILABILITY GROUP ON  
  'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-1:5022',    
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      ),   
  'SQLAG-DR' WITH    
       (   
         LISTENER_URL = 'tcp://SQLAG-DR:5022',   
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,   
         FAILOVER_MODE = MANUAL,   
         SEEDING_MODE = AUTOMATIC
      );   
```  

Tenga en cuenta que la dirección URL del agente de escucha es el VNN de la instancia FCI principal.

## Conmutar por error FCI manualmente en el grupo de disponibilidad distribuido

Para conmutar por error manualmente el grupo de disponibilidad FCI, actualice el grupo de disponibilidad distribuido para reflejar el cambio de dirección URL del agente de escucha. Por ejemplo, ejecute el siguiente DDL tanto en el grupo de disponibilidad principal como en el grupo de disponibilidad secundario de SQLFCIAG:

```tsql  
ALTER AVAILABILITY GROUP [SQLFCIDAG]  
   MODIFY AVAILABILITY GROUP ON  
 'SQLFCIAG' WITH    
    (   
        LISTENER_URL = 'tcp://SQLFCIAG-2:5022'
    )
```  
  
## Vea también  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  