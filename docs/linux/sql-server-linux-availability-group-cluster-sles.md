---
title: Configuración de clúster SLES para grupo de disponibilidad de SQL Server | Documentos de Microsoft
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 05/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.workload: Inactive
ms.openlocfilehash: 4fa3cd388fc1f4d22ee781721145d0fc4c465682
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configuración de clúster SLES para grupo de disponibilidad de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Esta guía proporciona instrucciones para crear un clúster de tres nodos para SQL Server en SUSE Linux Enterprise Server (SLES) 12 SP2. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos: vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El nivel de agrupación en clústeres se basa en SUSE [extensión de alta disponibilidad (HAE)](https://www.suse.com/products/highavailability) construidos sobre [marcapasos](http://clusterlabs.org/). 

Para obtener más información sobre la configuración de clúster, opciones de recurso del agente, administración, prácticas recomendadas y recomendaciones, consulte [SUSE Linux Enterprise alta disponibilidad extensión 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>En este momento, la integración de SQL Server con marcapasos en Linux no es como acoplamiento como con WSFC en Windows. Servicio de SQL Server en Linux no es compatible con clústeres. Marcapasos controla todas las de la orquestación de los recursos de clúster, incluido el recurso de grupo de disponibilidad. En Linux, no deben depender siempre en disponibilidad grupo vistas de administración dinámica (DMV) que proporcionan información de clúster como sys.dm_hadr_cluster. Además, el nombre de red virtual es específico de WSFC, no hay ningún equivalente de la misma en marcapasos. Puede crear un agente de escucha para usarlo para la reconexión transparente después de la conmutación por error, pero tendrá que registrar manualmente el nombre de agente de escucha en el servidor DNS con la dirección IP utilizada para crear el recurso IP virtual (como se explica en las secciones siguientes).


## <a name="roadmap"></a>Guía básica

El procedimiento para crear un grupo de disponibilidad para la alta disponibilidad es diferente entre servidores Linux y un clúster de conmutación por error de Windows Server. En la lista siguiente describe los pasos generales: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-failover-ha.md). 

3. Configurar un administrador de recursos de clúster, como marcapasos. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos de clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Los entornos de producción requieren a un agente de barrera, como STONITH para lograr alta disponibilidad. Los ejemplos de este artículo no utilizan a agentes de barrera. Son para pruebas y la validación solo. 
   
   >Un clúster marcapasos usa barrera para devolver el clúster a un estado conocido. La manera de configurar la barrera depende de la distribución y el entorno. En este momento, no está disponible en algunos entornos de nube barrera. Vea [extensión de alta disponibilidad SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a extremo, necesita tres equipos para implementar el clúster de tres nodos. Los pasos siguientes describen cómo configurar estos servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar y configurar el sistema operativo en cada nodo del clúster 

El primer paso es configurar el sistema operativo en los nodos del clúster. Para este tutorial, utilice SLES 12 SP2 con una suscripción válida para el complemento de alta disponibilidad.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Instalar y configurar el servicio de SQL Server en cada nodo del clúster

1. Instalar y configurar el servicio de SQL Server en todos los nodos. Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).

1. Designar un nodo como nodos principales y otros como elementos secundarios. Utilice estos términos a lo largo de esta guía.

1. Asegúrese de que los nodos que se van a formar parte del clúster pueden comunicarse entre sí.

   El ejemplo siguiente muestra `/etc/hosts` con las adiciones de tres nodos denominados SLES1, SLES2 y SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Todos los nodos del clúster deben poder tener acceso entre sí a través de SSH. Herramientas como `hb_report` o `crm_report` (para la solución de problemas) y el Explorador de historial del Hawk necesitan passwordless SSH acceso entre los nodos, en caso contrario, solo pueden recopilar datos desde el nodo actual. En caso de usar un puerto SSH no estándar, utilice la opción -X (consulte `man` página). Por ejemplo, si el puerto SSH es 3479, invoque un `crm_report` con:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Para obtener más información, consulte el [SLES Administration Guide - sección Miscellaneous](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para marcapasos

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurar un grupo de disponibilidad AlwaysOn

En servidores Linux, configure el grupo de disponibilidad y, a continuación, configurar los recursos de clúster. Para configurar el grupo de disponibilidad, consulte [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar y configurar a marcapasos en cada nodo del clúster

1. Instalar la extensión de alta disponibilidad

   Como referencia, vea [instalar SUSE Linux Enterprise Server y extensión de alta disponibilidad](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Instalar un paquete de agente de recursos de SQL Server en ambos nodos.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurar el primer nodo

   Hacer referencia a [las instrucciones de instalación de SLES](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Inicie sesión como `root` para la máquina física o virtual que desea usar como nodo de clúster.
2. Iniciar la secuencia de arranque mediante la ejecución:
   ```bash
   sudo ha-cluster-init
   ```

   Si no se ha configurado el NTP para iniciar al arrancar el sistema, aparece un mensaje. 

   Si decide continuar en cualquier caso, la secuencia de comandos automáticamente genera claves para el acceso SSH y la herramienta de sincronización de Csync2 e inicia los servicios necesarios para ambos. 

3. Para configurar el nivel de comunicación de clúster (Corosync): 

   A. Escriba una dirección de red para enlazar a. De forma predeterminada, la secuencia de comandos propuestos por la dirección de red de eth0. O bien, escriba una dirección de red diferente, por ejemplo la dirección de bond0. 

   B. Escriba una dirección de multidifusión. La secuencia de comandos propone una dirección aleatoria que puede usar como valor predeterminado. 

   c. Escriba un puerto de multidifusión. La secuencia de comandos propone 5405 como valor predeterminado. 

   d. Para configurar `SBD ()`, escriba una ruta de acceso persistente para la partición del dispositivo de bloque que se va a utilizar para el mismo día Laborable. La ruta de acceso debe ser coherente en todos los nodos del clúster. 
   Por último, la secuencia de comandos iniciará el servicio de marcapasos para poner en línea el clúster de un nodo y habilitar la interfaz de administración de Web Hawk2. La dirección URL que se usará para Hawk2 se muestra en la pantalla. 

4. Para obtener los detalles del proceso de instalación, compruebe `/var/log/sleha-bootstrap.log`. Ahora tiene un clúster de ejecución de un nodo. Compruebe el estado de clúster con el estado de crm:

   ```bash
   sudo crm status
   ```

   También puede ver la configuración de clúster con `crm configure show xml` o `crm configure show`.

5. El procedimiento de arranque, crea un usuario de Linux con el nombre hacluster con la contraseña de linux. Reemplace la contraseña predeterminada con una cadena segura tan pronto como sea posible: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Agregar nodos al clúster existente

Si tiene un clúster que ejecute con uno o más nodos, agregar más nodos del clúster con el script de arranque de ha de clúster-combinación. La secuencia de comandos sólo necesita acceso a un nodo del clúster existente y se completará automáticamente la configuración básica de la máquina actual. Siga estos pasos:

Si ha configurado los nodos del clúster existente con el `YaST` módulo de clúster, asegúrese de que se cumplen los siguientes requisitos previos antes de ejecutar `ha-cluster-join`:
- El usuario raíz en los nodos existentes tiene claves SSH en su lugar para inicio de sesión passwordless. 
- `Csync2` se configura en los nodos existentes. Para obtener más información, consulte Configurar Csync2 con YaST. 

1. Inicie sesión como raíz para la máquina física o virtual debe unirse al clúster. 
2. Iniciar la secuencia de arranque mediante la ejecución: 

   ```bash
   sudo ha-cluster-join
   ```

   Si no se ha configurado el NTP para iniciar al arrancar el sistema, aparece un mensaje. 

3. Si decide continuar de todos modos, se le pedirá para la dirección IP de un nodo existente. Escriba la dirección IP. 

4. Si ya no ha configurado un acceso SSH passwordless entre ambos equipos, también se pedirá la contraseña raíz del nodo existente. 

   Después de iniciar sesión el nodo especificado, el script copia la configuración de Corosync, configura SSH y `Csync2`y pone el equipo actual en línea como nuevo nodo de clúster. Aparte de eso, se inicia el servicio necesario para Hawk. Si ha configurado el almacenamiento compartido con `OCFS2`, se crea automáticamente el directorio de punto de montaje para el `OCFS2` sistema de archivos. 

5. Repita los pasos anteriores para todos los equipos que desea agregar al clúster. 

6. Para obtener información detallada del proceso, consulte `/var/log/ha-cluster-bootstrap.log`. 

1. Comprobar el estado de clúster con `sudo crm status`. Si ha agregado el segundo nodo correctamente, el resultado debería parecerse al siguiente:

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` es el recurso de clúster IP virtual que se configura durante la instalación inicial de un nodo de clúster.

Después de agregar todos los nodos, compruebe si necesita ajustar la directiva de quórum de ninguna de las opciones de clúster global. Esto es especialmente importante para los clústeres de dos nodos. Para obtener más información, vea la sección 4.1.2, opción no-quórum-policy. 

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Establecer propiedades de clúster inicio error-es-grave en false

`Start-failure-is-fatal` indica si un error al iniciar un recurso en un nodo impide más intentos de inicio en ese nodo. Cuando se establece en `false`, el clúster decide si debe intentar iniciar en el mismo nodo nuevo, en función actual error recuento y migración el umbral del recurso. Por lo tanto, después de producirse la conmutación por error, a partir de la disponibilidad de reintentos de marcapasos recurso de grupo en la primera estructura principal una vez que la instancia de SQL está disponible. Marcapasos se encarga de disminuir de nivel de la réplica secundaria y vuelve a unirse automáticamente el grupo de disponibilidad. Además, si `start-failure-is-fatal` se establece en `false`, el clúster vuelve a los límites configurados failcount configurados con el umbral de migración. Asegúrese de que el valor predeterminado de umbral de migración se actualiza en consecuencia.

Para actualizar el valor de propiedad para ejecución false:
```bash
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Si la propiedad tiene el valor predeterminado de `true`, si el primer intento de iniciar el recurso se produce un error, la intervención del usuario es necesario después de una conmutación por error automática para limpiar el recuento de errores de recursos y restablecer la configuración mediante: `sudo crm resource cleanup <resourceName>` comando.

Para obtener más información sobre propiedades de clúster marcapasos, consulte [configurar recursos de clúster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

# <a name="configure-fencing-stonith"></a>Configurar la barrera (STONITH)
Los proveedores de clúster marcapasos requieren STONITH esté habilitado y un dispositivo de barrera configurado para una instalación de clúster compatibles. Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, barrera se utiliza para poner el clúster en un estado conocido de nuevo.

Barrera de nivel de recurso principalmente garantiza que no hay ningún daños en los datos durante una interrupción del sistema mediante la configuración de un recurso. Puede usar la barrera de nivel de recurso, por ejemplo, con DRBD (Distributed replican bloque dispositivo) para marcar el disco en un nodo como obsoleto cuando el vínculo de comunicación deja de funcionar.

Barrera de nivel de nodo se asegura de que un nodo no ejecuta todos los recursos. Para ello, restablecer el nodo y la implementación de marcapasos del mismo se denomina STONITH (que es el acrónimo "grabar el otro nodo en el encabezado"). Marcapasos admite una gran variedad de dispositivos, como tarjetas de interfaz de una fuente de alimentación o de administración de sistema de alimentación ininterrumpida para servidores de barrera.

Para obtener más información, consulte [marcapasos clústeres desde el principio](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [barrera y Stonith](http://clusterlabs.org/doc/crm_fencing.html) y [SUSE HA documentación: barrera y STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

En el momento de inicialización de clúster, STONITH está deshabilitada si no se detecta ninguna configuración. Se puede habilitar más tarde ejecutando el comando siguiente:

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar marcapasos en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y manténgala habilitada. SUSE no proporciona a agentes de barrera para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad con la ejecución de clústeres de producción en estos entornos. Estamos trabajando en una solución para este vacío que estará disponible en futuras versiones.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar los recursos de clúster de SQL Server

Hacer referencia a [SLES administración Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>Crear el recurso de grupo de disponibilidad

El siguiente comando crea y configura el recurso de grupo de disponibilidad para las tres réplicas de grupo de disponibilidad [ag1]. Las operaciones de monitor y tiempos de espera tienen que especificarse explícitamente en SLES basada en que los tiempos de espera muy dependen de la carga de trabajo y que deba ajustar cuidadosamente para cada implementación.
Ejecute el comando en uno de los nodos del clúster:

1. Ejecute `crm configure` para abrir el símbolo del sistema de crm:

   ```bash
   sudo crm configure 
   ```

1. En el símbolo del sistema de crm, ejecute el comando siguiente para configurar las propiedades del recurso.

   ```bash
primitive ag_cluster \
   ocf:mssql:ag \
   params ag_name="ag1" \
   op start timeout=60s \
   op stop timeout=60s \
   op promote timeout=60s \
   op demote timeout=10s \
   op monitor timeout=60s interval=10s \
   op monitor timeout=60s interval=11s role="Master" \
   op monitor timeout=60s interval=12s role="Slave" \
   op notify timeout=60s
ms ms-ag_cluster ag_cluster \
   meta master-max="1" master-node-max="1" clone-max="3" \
  clone-node-max="1" notify="true" \
commit
   ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>Crear el recurso de IP virtual

Si no ha creado el recurso IP virtual cuando ejecutó `ha-cluster-init` ahora puede crear este recurso. El comando siguiente crea un recurso IP virtual. Reemplace `<**0.0.0.0**>` con una dirección disponible desde la red y `<**24**>` con el número de bits de la máscara de subred CIDR. Ejecutar en un nodo.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Agregar restricción de colocación
Casi cada decisión en un clúster marcapasos, como elegir dónde se debe ejecutar un recurso, se realiza comparando las puntuaciones. Las puntuaciones se calculan por recurso y el Administrador de recursos de clúster elige el nodo con la máxima puntuación de un recurso concreto. (Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.) Se pueden manipular las decisiones del clúster con restricciones. Las restricciones tienen una puntuación. Si una restricción que tiene una puntuación menor que infinito, es sólo una recomendación. Una puntuación de infinito significa que es un requisito indispensable. Es deseable para asegurarse de que principal del grupo de disponibilidad y el virtual recurso de ip se ejecutan en el mismo host, por lo que se define una restricción de colocación con una puntuación de infinito. 

Para establecer la restricción de colocación para la dirección IP virtual para que se ejecute en el mismo nodo que el maestro, ejecute el siguiente comando en un nodo:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Agregar restricción de ordenación
La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que pase el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos: 

1. Migrar recursos de problemas de usuario al maestro del grupo de disponibilidad del Nodo1 al Nodo2.
2. El recurso IP virtual se detiene en el nodo 1.
3. El recurso IP virtual se inicia en el nodo 2. En este punto, la dirección IP temporalmente puntos al nodo 2 mientras el nodo 2 sigue siendo una pre-conmutación por error secundario. 
4. El maestro del grupo de disponibilidad en el nodo 1 se degrada para subordinado.
5. Se promueve el subordinado del grupo de disponibilidad en el nodo 2 al maestro. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior la conmutación por error, agregue una restricción de ordenación. Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede usar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En SLES usar `crm`. 

Conmutar por error manualmente el grupo de disponibilidad con `crm`. No iniciar la conmutación por error con Transact-SQL. Para obtener más información, consulte [conmutación por error](sql-server-linux-availability-group-failover-ha.md#failover).


Para obtener más información, vea:
- [Administración de recursos de clúster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [HA de conceptos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Referencia rápida de marcapasos](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)
