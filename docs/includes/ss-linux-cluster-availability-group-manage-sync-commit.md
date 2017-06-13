## <a name="managing-synchronous-commit-mode"></a>Administrar el modo de confirmación sincrónica

>[!WARNING]
>En algunos casos, un grupo de disponibilidad de SQL Server en modo de confirmación sincrónica en Linux puede ser vulnerable a la pérdida de datos. Vea la información siguiente sobre la causa principal y la solución alternativa para evitar la pérdida de datos. Este problema se corregirá en las próximas versiones.

###<a name="pacemaker-notification-for-availability-group-resource-promotion"></a>Notificación de Pacemaker para la promoción de recursos del grupo de disponibilidad

Antes de la versión CTP 1.4, el agente de recursos de Pacemaker para grupos de disponibilidad no podía saber si una réplica marcada como `SYNCHRONOUS_COMMIT` estaba realmente actualizada o no. Era posible que la réplica hubiera dejado de sincronizarse con la réplica principal pero que no lo supiera. Por lo tanto, el agente podía promover a principal una réplica obsoleta, lo que provocaría una pérdida de datos si se llevara a cabo correctamente. 

1.4 de CTP de SQL Server de 2017 agrega `sequence_number` a `sys.availability_groups` para resolver este problema. `sequence_number` es un valor BIGINT con una progresión continua que representa el grado de actualización de la réplica del grupo de disponibilidad local con respecto al resto del sistema. Las conmutaciones por error, la adición o la eliminación de réplicas y otras operaciones del grupo de disponibilidad actualizan este número. El número se actualiza en la réplica principal y, después, se inserta en las secundarias. Por lo tanto, una réplica secundaria que esté actualizada tendrá el mismo número que la principal.

Cuando Pacemaker decide promover una réplica a principal, en primer lugar envía una notificación a todas las réplicas para extraer el número de secuencia y almacenarlo. Después, cuando Pacemaker intenta realmente promover una réplica a principal, la réplica solo se promueve a sí misma si su número de secuencia es el más alto de todos los números de secuencia. En caso contrario, rechaza la operación de promoción. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos.

Tenga en cuenta que solo se garantiza que esto funcione si al menos una réplica disponible para la promoción tiene el mismo número de secuencia que la réplica principal anterior. Dado que el agente de recursos requiere que Pacemaker envíe notificaciones a todas las réplicas, es necesario configurar el recurso de disponibilidad con `notify=true`. Para todos los recursos `ocf:mssql:ag` existentes, el usuario deberá actualizar la configuración de recursos con `notify=true` antes de actualizar el paquete `mssql-server-ha` a CTP 1.4. En caso contrario, el recurso pasará a estado de error. 

### <a name="how-to-avoid-potential-for-data-loss"></a>Cómo evitar la posible pérdida de datos 

En el caso siguiente, un grupo de disponibilidad todavía podría ser vulnerable a la pérdida de datos. En un clúster con cinco nodos, si hay un grupo de disponibilidad con réplicas en tres instancias de SQL Server, es posible que la réplica principal y una réplica secundaria estén por delante de la otra réplica secundaria. Cuando están por delante, el `sequence_number` de `sys.availability_groups` será más alto que el de las otras réplicas. En esta situación, si las dos réplicas pierden la conexión con el resto del clúster, Pacemaker podría ver los tres nodos restantes como un cuórum y permitir que la réplica latente se promueva a sí misma a principal. En esta situación, es posible que se produzca una pérdida de datos.

sql2017 presenta una nueva característica para forzar a un número determinado de servidores secundarios estén disponibles antes de que se pueden confirmar las transacciones en el servidor principal. `REQUIRED_COPIES_TO_COMMIT` permite establecer un número de réplicas que se deben confirmar en los registros de transacciones de la base de datos de la réplica secundaria antes de que una transacción pueda continuar. Puede usar esta opción con `CREATE AVAILABILITY GROUP` o `ALTER AVAILABILITY GROUP`. Vea [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx).

Para evitar la posible pérdida de datos descrita anteriormente, establezca `REQUIRED_COPIES_TO_COMMIT` en el número máximo de réplicas sincronizadas. Las próximas versiones incluirán lógica para controlar el establecimiento de `REQUIRED_COPIES_TO_COMMIT` automáticamente.
Cuando se establece `REQUIRED_COPIES_TO_COMMIT`, las transacciones en las bases de datos de la réplica principal esperarán hasta que la transacción se confirme en el número necesario de registros de transacciones de la base de datos de la réplica secundaria sincrónica. Si no hay bastantes réplicas secundarias sincrónicas en línea, las transacciones se detendrán hasta que se reanude la comunicación con las suficientes réplicas secundarias.

En el ejemplo siguiente se establece el nombre del grupo de disponibilidad [ag1] en `REQUIRED_COPIES_TO_COMMIT = 2`. 

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1]
SET (REQUIRED_COPIES_TO_COMMIT = 2)
```

En el ejemplo anterior, si el grupo de disponibilidad tiene dos réplicas secundarias, esperará hasta que ambas réplicas secundarias reconozcan las confirmaciones. Si una no responde, se bloquearán las transacciones.
