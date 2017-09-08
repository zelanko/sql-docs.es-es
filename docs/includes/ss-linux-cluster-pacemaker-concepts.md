## <a name="pacemakerNotify"></a>Información sobre el agente de recursos de SQL Server para Pacemaker

Antes de la versión CTP 1.4, el agente de recursos de Pacemaker para grupos de disponibilidad no podía saber si una réplica marcada como `SYNCHRONOUS_COMMIT` estaba realmente actualizada o no. Era posible que la réplica hubiera dejado de sincronizarse con la réplica principal pero que no lo supiera. Por tanto, el agente podía promover a principal una réplica obsoleta, lo que provocaría una pérdida de datos si se llevara a cabo correctamente. 

SQL Server 2017 CTP 1.4 ha agregado `sequence_number` a `sys.availability_groups` para resolver este problema. `sequence_number` es un valor BIGINT con una progresión continua que representa el grado de actualización de la réplica del grupo de disponibilidad local con respecto al resto de réplicas del grupo de disponibilidad. Las conmutaciones por error, la adición o la eliminación de réplicas y otras operaciones del grupo de disponibilidad actualizan este número. El número se actualiza en la réplica principal y, después, se inserta en las réplicas secundarias. Por tanto, una réplica secundaria que esté actualizada tendrá el mismo número de secuencia que la principal. 

Cuando Pacemaker decide promover una réplica a principal, en primer lugar envía una notificación a todas las réplicas para extraer el número de secuencia y almacenarlo (esto se denomina notificación previa a la promoción). Después, cuando Pacemaker intenta realmente promover una réplica a principal, la réplica solo se promueve a sí misma si su número de secuencia es el más alto de todos los números de secuencia de todas las réplicas. En caso contrario, rechaza la operación de promoción. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos. 

Tenga en cuenta que solo se garantiza que esto funcione si al menos una réplica disponible para la promoción tiene el mismo número de secuencia que la réplica principal anterior. Para asegurarse de esto, el comportamiento predeterminado es que el agente de recursos de Pacemaker establezca automáticamente `REQUIRED_COPIES_TO_COMMIT` de forma que al menos una réplica secundaria de confirmación sincrónica está actualizada y disponible para ser el destino de una conmutación por error automática. Con cada acción de supervisión, el valor de `REQUIRED_COPIES_TO_COMMIT` se calcula (y actualiza, si es necesario) como ("número de réplicas de confirmación sincrónica" / 2). Después, en tiempo de conmutación por error, el agente de recursos requerirá que (`total number of replicas` - `required_copies_to_commit` réplicas) respondan a la notificación previa a la promoción para poder promover una de ellas a principal. La réplica con el valor de `sequence_number` más alto se promoverá a principal. 

Por ejemplo, consideremos el caso de un grupo de disponibilidad con tres réplicas sincrónicas (una réplica principal y dos réplicas secundarias de confirmación sincrónica).

- `REQUIRED_COPIES_TO_COMMIT` es 3 / 2 = 1

- El número necesario de réplicas para responder a la acción previa a la promoción es de 3 - 1 = 2. Por lo que 2 réplicas tienen que estar activas para que se desencadene la conmutación por error. Esto significa que, en el caso de una interrupción principal, si una de las réplicas secundarias no responde y solo responde una de las secundarias a la acción previa a la promoción, el agente de recursos no puede garantizar que la réplica secundaria que ha respondido tenga el sequence_number más alto y no se desencadena una conmutación por error.

Un usuario puede elegir invalidar el comportamiento predeterminado y configurar el recurso de grupo de disponibilidad para no establecer `REQUIRED_COPIES_TO_COMMIT` automáticamente como se ha mostrado anteriormente.

>[!IMPORTANT]
>Cuando `REQUIRED_COPIES_TO_COMMIT` es 0, existe riesgo de pérdida de datos. En el caso de una interrupción de la réplica principal, el agente de recursos no desencadenará automáticamente una conmutación por error. El usuario tiene que decidir si quiere esperar para que la principal se recupere o conmute por error de forma manual.

Para establecer `REQUIRED_COPIES_TO_COMMIT` en 0, ejecute:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=0
```

El comando equivalente con crm (en SLES) es:

```bash
sudo crm resource param <**ag_cluster**> set required_synchronized_secondaries_to_commit 0
```

Para revertir al valor calculado predeterminado, ejecute:

```bash
sudo pcs resource update <**ag_cluster**> required_copies_to_commit=
```

>[!NOTE]
>Actualizar las propiedades de recursos hace que todas las réplicas se detengan y reinicien. Esto significa que la réplica principal se degradará temporalmente a secundaria y se volverá a promover de nuevo, lo que causará una falta de disponibilidad de escritura temporal. El nuevo valor de REQUIRED_COPIES_TO_COMMIT solo se establecerá una vez que se reinicien las réplicas, por lo que no será instantáneo al ejecutar el comando del equipo.

## <a name="balancing-high-availability-and-data-protection"></a>Equilibrio de la alta disponibilidad y la protección de datos 

El comportamiento predeterminado anterior también se aplica en el caso de 2 réplicas sincrónicas (principal + secundaria). Pacemaker tendrá como valor predeterminado `REQUIRED_COPIES_TO_COMMIT = 1` para asegurarse de que la réplica secundaria siempre esté actualizada para la máxima protección de datos.  

>[!WARNING]
>Esto viene con un mayor riesgo de falta de disponibilidad de la réplica principal debido a interrupciones previstas e imprevistas en la réplica secundaria. El usuario puede elegir cambiar el comportamiento predeterminado del agente de recursos e invalidar `REQUIRED_COPIES_TO_COMMIT` en 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Una vez que se invalida, el agente de recursos usará la nueva configuración para `REQUIRED_COPIES_TO_COMMIT` y dejará de calcularlo. Esto significa que los usuarios tienen que actualizarlo de forma manual según corresponda (por ejemplo, si aumentan el número de réplicas).

En las tablas siguientes, se describe el resultado de una interrupción para las réplicas principal o secundaria en configuraciones de recursos de grupo de disponibilidad diferentes:

### <a name="availability-group---2-sync-replicas"></a>Grupo de disponibilidad: 2 réplicas de sincronización

| |Interrupción principal |Interrupción de réplica secundaria
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|El usuario tiene que emitir una conmutación por error manual. <br>Es posible que haya pérdida de datos.<br> La nueva réplica principal es de L/E. |La réplica principal es de L/E, la ejecución se expone a pérdida de datos.
|`REQUIRED_COPIES_TO_COMMIT=1` * |El clúster emitirá automáticamente la conmutación por error. <br>No se produce pérdida de datos. <br> La nueva réplica principal rechazará todas las conexiones hasta que la réplica principal anterior se recupere y una al grupo de disponibilidad como réplica secundaria. |La réplica principal rechazará todas las conexiones hasta que se recupere la secundaria.

\* Comportamiento predeterminado del agente de recursos de SQL Server para Pacemaker.

### <a name="availability-group---3-sync-replicas"></a>Grupo de disponibilidad: 3 réplicas de sincronización

| |Interrupción principal |Interrupción de réplica secundaria
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|El usuario tiene que emitir una conmutación por error manual. <br>Es posible que haya pérdida de datos. <br>La nueva réplica principal es de L/E. |La réplica principal es de L/E.
|`REQUIRED_COPIES_TO_COMMIT=1` * |El clúster emitirá automáticamente la conmutación por error. <br>No se produce pérdida de datos. <br>La nueva réplica principal es de L/E. |La réplica principal es de L/E. 

\* Comportamiento predeterminado del agente de recursos de SQL Server para Pacemaker.