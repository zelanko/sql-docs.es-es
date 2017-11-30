Cada grupo de disponibilidad tiene solo una réplica principal. La réplica principal permite lecturas y escrituras. Para cambiar qué réplica principal, puede conmutar por error. En un grupo de disponibilidad de alta disponibilidad, el administrador de clústeres automatiza el proceso de conmutación por error. En un grupo de disponibilidad de escalado de lectura, el proceso de conmutación por error es manual. 

Hay dos maneras para conmutar la réplica principal en un grupo de disponibilidad de la escala de lectura:

- Forzar la conmutación por error manual con pérdida de datos
- Conmutación por error manual sin pérdida de datos

### <a name="forced-manual-failover-with-data-loss"></a>Forzar la conmutación por error manual con pérdida de datos

Use este método cuando la réplica principal no está disponible y no se puede recuperar. 

Para forzar la conmutación por error con pérdida de datos, conéctese a la instancia de SQL Server que hospeda la réplica secundaria de destino y ejecute:

```SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-failover-without-data-loss"></a>Conmutación por error manual sin pérdida de datos

Use este método si la réplica principal está disponible, pero necesita modificar temporal o permanentemente la configuración y la instancia de SQL Server que hospeda la réplica principal. Antes de emitir la conmutación por error manual, asegúrese de que la réplica secundaria de destino está actualizada para evitar la posible pérdida de datos. 

Conmutación por error manual sin pérdida de datos:

1. Realizar la réplica secundaria de destino `SYNCHRONOUS_COMMIT`.

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        MODIFY REPLICA ON N'**<node2>*' 
        WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```

2. Ejecute la consulta siguiente para identificar los que las transacciones activas se confirman en la réplica principal y al menos una réplica secundaria sincrónica: 

   ```SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

   La réplica secundaria se sincroniza si `synchronization_state_desc` es `SYNCHRONIZED`.

3. Actualización `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 1.

   El siguiente script establece `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en 1 en un grupo de disponibilidad denominado `ag1`. Antes de ejecutar el script siguiente, reemplace `ag1` con el nombre del grupo de disponibilidad:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = 1;
   ```

   Este valor garantiza que todas las transacciones activas se compromete a la réplica principal y al menos una réplica secundaria sincrónica. 

4. Disminuir el nivel de la réplica principal a una réplica secundaria. Después de que la réplica principal se degrada, es de solo lectura. Ejecute este comando en la instancia de SQL Server que hospeda la réplica principal para el rol de actualizar `SECONDARY`:

   ```SQL
   ALTER AVAILABILITY GROUP [ag1] 
        SET (ROLE = SECONDARY); 
   ```

5. Ascienda la réplica secundaria de destino a principal. 

   ```SQL
   ALTER AVAILABILITY GROUP ag1 FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para eliminar un grupo de disponibilidad, utilice [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para un grupo de disponibilidad creado con CLUSTER_TYPE ninguno o externa, el comando debe ejecutarse en todas las réplicas que forman parte del grupo de disponibilidad.