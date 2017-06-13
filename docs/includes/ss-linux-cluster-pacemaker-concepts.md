## <a name="pacemakerNotify"></a>Comprender el agente de recursos de SQL Server para marcapasos

Antes de la versión 1.4 de CTP, el agente de recursos marcapasos para grupos de disponibilidad podría conocer no si una réplica se marca como `SYNCHRONOUS_COMMIT` estaban realmente actualizados o no. Era posible que la réplica hubiera dejado de sincronizarse con la réplica principal pero que no lo supiera. Por lo tanto el agente pudo promover una réplica obsoleta principales - que, si se realiza correctamente, podría provocar la pérdida de datos. 

SQL Server de 2017 CTP 1.4 agrega `sequence_number` a `sys.availability_groups` para resolver este problema. `sequence_number`es un progresión BIGINT que representa el grado de actualización es la réplica del grupo de disponibilidad local con respecto al resto de las réplicas del grupo de disponibilidad. Este número de actualización de realizar conmutaciones por error, agregar o quitar las réplicas y otras operaciones de grupo de disponibilidad. El número se actualiza en el servidor principal, a continuación, inserta en las réplicas secundarias. Por lo tanto una réplica secundaria que está actualizada tendrá el mismo sequence_number como la réplica principal. 

Cuando decida marcapasos promocionar una réplica principal, primero envía una notificación a todas las réplicas para extraer el número de secuencia y los almacene (Esto se llama el previamente promover notificación). A continuación, cuando realmente marcapasos intenta promover una réplica principal, la réplica solo promueve a sí mismo si su número de secuencia es el nivel más alto de todos los números de secuencia de todas las réplicas y rechaza la operación promover en caso contrario. De esta manera, solo se puede promover a principal la réplica con el número de secuencia más alto, lo que garantiza que no se producirá una pérdida de datos. 

Tenga en cuenta que solo se garantiza que esto funcione si al menos una réplica disponible para la promoción tiene el mismo número de secuencia que la réplica principal anterior. Para asegurarse de esto, el comportamiento predeterminado es para que el agente de recursos marcapasos establecer automáticamente `REQUIRED_COPIES_TO_COMMIT` forma que al menos una sincrónica confirmar secundaria réplica está actualizada y disponible para ser el destino de una conmutación por error automática. Con cada acción de supervisión, el valor de `REQUIRED_COPIES_TO_COMMIT` es calculada (y actualiza si es necesario) como ('número de réplicas de confirmación sincrónica' / 2). A continuación, en tiempo de conmutación por error, el agente de recursos requerirá (`total number of replicas`  -  `required_copies_to_commit` réplicas) para responder a la previamente promover notificación para poder promover uno de ellos al elemento principal. La réplica con el nivel más alto `sequence_number` se promoverá a principal. 

Por ejemplo, consideremos el caso de un grupo de disponibilidad con tres réplicas sincrónicas - una réplica principal y dos réplicas secundarias de confirmación sincrónica.

- `REQUIRED_COPIES_TO_COMMIT`es 3 / 2 = 1

- El número necesario de réplicas para responder para promover la acción previamente es 3-1 = 2. Por lo que 2 réplicas tienen que estar activos para que la conmutación por error para que se desencadene. Esto significa que, en el caso de interrupción principal, si una de las réplicas secundarias no responde y solo uno de los servidores secundarios se responde a las previamente promover acción, el agente de recursos no puede garantizar que la base de datos secundaria que respondió tiene el sequence_number más alto y no se desencadena una conmutación por error.

Un usuario puede elegir invalidar el comportamiento predeterminado y configurar el recurso de grupo de disponibilidad para no establecer `REQUIRED_COPIES_TO_COMMIT` automáticamente como arriba.

>[!IMPORTANT]
>Cuando `REQUIRED_COPIES_TO_COMMIT` es ahí 0 es el riesgo de pérdida de datos. En el caso de una interrupción de la réplica principal, el agente de recursos no desencadenará automáticamente una conmutación por error. El usuario tiene que decidir si quieren que debe esperar para que el elemento primario recuperar o conmutación por error manual.

Para establecer `REQUIRED_COPIES_TO_COMMIT` en 0, ejecute:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Para volver al valor predeterminado valor calculado, ejecute:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=
```

>[!NOTE]
>Actualizar propiedades de recursos hace que todas las réplicas detener y reiniciar. Esto significa principal se temporalmente se degrada a la base de datos secundaria y promueve nuevo que casue temporal escribirá falta de disponibilidad. El nuevo valor de REQUIRED_COPIES_TO_COMMIT solo establecerá una vez que se reinician las réplicas, por lo que no sea instantáneo al ejecutar el comando de equipos.

## <a name="balancing-high-availability-and-data-protection"></a>Equilibrio de la alta disponibilidad y protección de datos 

El comportamiento predeterminado anterior también se aplica en el caso de 2 réplicas sincrónicas (principales y secundarias). Marcapasos tendrá como valor predeterminado `REQUIRED_COPIES_TO_COMMIT = 1` para asegurarse de la base de datos secundaria réplica siempre está actualizada para la protección de datos máximo.  

>[!WARNING]
>Esto viene con mayor riesgo de falta de disponibilidad de la réplica principal debido a errores previstos e imprevistos en la base de datos secundaria. El usuario puede elegir cambiar el comportamiento predeterminado del agente de recursos e invalidar el `REQUIRED_COPIES_TO_COMMIT` en 0:

```bash
sudo pcs resource update <**ag1**> required_copies_to_commit=0
```

Una vez que se reemplaza, se utilizará la nueva configuración para el agente de recurso `REQUIRED_COPIES_TO_COMMIT` y detener calcularlo. Esto significa que los usuarios tengan que actualizarlo de forma manual según corresponda (por ejemplo, si aumenta el número de réplicas).

Las tablas siguientes se describe el resultado de una interrupción para las réplicas principales o secundarias en configuraciones de recursos de grupo de disponibilidad diferentes:

### <a name="availability-group---2-sync-replicas"></a>Grupo de disponibilidad: 2 réplicas de sincronización

| |Interrupción principal |Una interrupción de la réplica secundaria
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Usuario tiene que emitir una conmutación por error manual. <br>Podría tener la pérdida de datos.<br> Nuevo elemento principal es de lectura/escritura |Principal es de lectura/escritura, ejecución expuesta a la pérdida de datos
|`REQUIRED_COPIES_TO_COMMIT=1` * |Clúster emitirá automáticamente la conmutación por error <br>Sin pérdida de datos. <br> Nuevo elemento principal rechazará todas las conexiones hasta que el objeto principal anterior se recupera y une a grupo de disponibilidad como base de datos secundaria. |Principal rechazará todas las conexiones hasta que recupera secundaria.

\*Agente de recursos de SQL Server para el comportamiento predeterminado de marcapasos.

### <a name="availability-group---3-sync-replicas"></a>Grupo de disponibilidad: 3 réplicas de sincronización

| |Interrupción principal |Una interrupción de la réplica secundaria
|:---|:--- |:--- |
|`REQUIRED_COPIES_TO_COMMIT=0`|Usuario tiene que emitir una conmutación por error manual. <br>Podría tener la pérdida de datos. <br>Nuevo elemento principal es de lectura/escritura |Principal es de lectura/escritura
|`REQUIRED_COPIES_TO_COMMIT=1` * |Clúster emitirá automáticamente la conmutación por error. <br>Sin pérdida de datos. <br>Nuevo elemento principal es RW |Principal es de lectura/escritura 

\*Agente de recursos de SQL Server para el comportamiento predeterminado de marcapasos.