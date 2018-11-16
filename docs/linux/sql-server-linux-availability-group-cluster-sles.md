---
title: Configuración de clúster SLES para el grupo de disponibilidad de SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 3db679a5df861cbdbf08443b5fdd85e99b01d3b3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670624"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configuración de clúster SLES para el grupo de disponibilidad de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Esta guía proporciona instrucciones para crear un clúster de tres nodos para SQL Server en SUSE Linux Enterprise Server (SLES) 12 SP2. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El nivel de agrupación en clústeres se basa en SUSE [extensión de alta disponibilidad (HAE)](https://www.suse.com/products/highavailability) construidos sobre [Pacemaker](https://clusterlabs.org/). 

Para obtener más información sobre la configuración del clúster, las opciones del agente de recursos, administración, procedimientos recomendados y recomendaciones, consulte [SUSE Linux Enterprise alta disponibilidad extensión 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>En este momento, integración de SQL Server con Pacemaker en Linux no es tan acoplamiento como con WSFC en Windows. Servicio de SQL Server en Linux no es compatible con clústeres. Pacemaker controla todo de la orquestación de los recursos de clúster, incluido el recurso de grupo de disponibilidad. En Linux, no deben depender siempre en disponibilidad grupo vistas de administración dinámica (DMV) que proporcionan información del clúster como sys.dm_hadr_cluster. Además, nombre de red virtual es WSFC específico, no hay ningún equivalente de la misma en Pacemaker. Puede crear un agente de escucha para que lo utilicen para la reconexión después de la conmutación por error transparente, pero tendrá que registrar manualmente el nombre de agente de escucha en el servidor DNS con la dirección IP usada para crear el recurso IP virtual (como se explica en las secciones siguientes).


## <a name="roadmap"></a>Mapa de ruta

El procedimiento para crear un grupo de disponibilidad para alta disponibilidad difiere entre los servidores Linux y un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto nivel: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-failover-ha.md). 

3. Configurar un administrador de recursos de clúster, como Pacemaker. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos del clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Entornos de producción requieren a un agente de vallado, como STONITH para lograr alta disponibilidad. Los ejemplos de este artículo no usan a los agentes de barrera. Son para pruebas y validación solo. 
   
   >Un clúster de Pacemaker usa vallado para devolver el clúster a un estado conocido. La manera de configurar vallado depende de la distribución y el entorno. En este momento, la barrera no está disponible en algunos entornos de nube. Consulte [extensión de alta disponibilidad SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Requisitos previos

Para completar el siguiente escenario de extremo a otro, necesita tres equipos para implementar el clúster de tres nodos. Los siguientes pasos describen cómo configurar estos servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar y configurar el sistema operativo en cada nodo del clúster 

El primer paso es configurar el sistema operativo en los nodos del clúster. Para este tutorial, use SLES 12 SP2 con una suscripción válida para el complemento de alta disponibilidad.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Instalar y configurar el servicio SQL Server en cada nodo del clúster

1. Instalar y configurar el servicio de SQL Server en todos los nodos. Para obtener instrucciones detalladas, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).

1. Designar un nodo como nodos principales y otros como elementos secundarios. Use estos términos a lo largo de esta guía.

1. Asegúrese de que los nodos que se van a formar parte del clúster pueden comunicarse entre sí.

   El ejemplo siguiente muestra `/etc/hosts` con adiciones de tres nodos denominados SLES1, SLES2 y SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Todos los nodos del clúster deben poder tener acceso entre sí a través de SSH. Herramientas como `hb_report` o `crm_report` (para la solución de problemas) y el Explorador de historial de Hawk requieren el acceso SSH sin contraseña entre los nodos, en caso contrario, solo puede recopilar datos desde el nodo actual. En caso de usar un puerto SSH no estándar, use la opción -X (consulte `man` página). Por ejemplo, si el puerto SSH es 3479, invoque un `crm_report` con:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Para obtener más información, consulte el [SLES Administration Guide - sección varios](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurar un grupo de disponibilidad AlwaysOn

En los servidores de Linux, configure el grupo de disponibilidad y luego configure los recursos de clúster. Para configurar el grupo de disponibilidad, consulte [Configurar grupo de disponibilidad AlwaysOn para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalación y configuración de Pacemaker en cada nodo del clúster

1. Instalar la extensión de alta disponibilidad

   Como referencia, vea [instalación de SUSE Linux Enterprise Server y la extensión de alta disponibilidad](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Instalar el paquete del agente de recursos de SQL Server en ambos nodos.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurar el primer nodo

   Consulte [instrucciones de instalación de SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Inicie sesión como `root` a la máquina física o virtual que desea utilizar como nodo de clúster.
2. Iniciar la secuencia de arranque mediante la ejecución:
   ```bash
   sudo ha-cluster-init
   ```

   Si no se configuró para iniciarse en el tiempo de arranque NTP, aparece un mensaje. 

   Si decide continuar de todos modos, el script genera claves para el acceso SSH y la herramienta de sincronización Csync2 automáticamente e inicia los servicios necesarios para ambos. 

3. Para configurar la capa de comunicación de clúster (Corosync): 

   A. Escriba una dirección de red para enlazar a. De forma predeterminada, la secuencia de comandos propone la dirección de red de eth0. Como alternativa, escriba una dirección de red diferente, por ejemplo, la dirección de bond0. 

   B. Escriba una dirección de multidifusión. El script propone una dirección aleatoria que puede usar como valor predeterminado. 

   c. Escriba un puerto de multidifusión. El script propone 5405 como valor predeterminado. 

   d. Para configurar `SBD ()`, escriba una ruta de acceso persistente a la partición del dispositivo de bloque que se va a usar para SBD. La ruta de acceso debe ser coherente en todos los nodos del clúster. 
   Por último, el script iniciará el servicio de Pacemaker para poner en línea el clúster de un nodo y habilitar la interfaz de administración Web Hawk2. La dirección URL que se usará para Hawk2 se muestra en la pantalla. 

4. Para obtener los detalles del proceso de instalación, compruebe `/var/log/sleha-bootstrap.log`. Ahora tiene un clúster de un nodo en ejecución. Compruebe el estado del clúster con el estado de crm:

   ```bash
   sudo crm status
   ```

   También puede ver la configuración del clúster con `crm configure show xml` o `crm configure show`.

5. El procedimiento de arranque crea un usuario de Linux denominado hacluster coincida con la contraseña de linux. Reemplace la contraseña predeterminada por una segura tan pronto como sea posible: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Agregar nodos al clúster existente

Si tiene un clúster que ejecute con uno o varios nodos, agregar más nodos de clúster con el script de arranque de alta disponibilidad-cluster-join. El script solo necesita tener acceso a un nodo de clúster existente y se completará automáticamente la configuración básica en el equipo actual. Use los pasos siguientes:

Si ha configurado los nodos del clúster existente con el `YaST` módulo del clúster, asegúrese de que se cumplen los siguientes requisitos previos antes de ejecutar `ha-cluster-join`:
- El usuario raíz en los nodos existentes tiene claves SSH en su lugar para el inicio de sesión. 
- `Csync2` se configura en los nodos existentes. Para obtener más información, consulte Configurar Csync2 con YaST. 

1. Inicie sesión como raíz para la máquina física o virtual debe unirse al clúster. 
2. Iniciar la secuencia de arranque mediante la ejecución: 

   ```bash
   sudo ha-cluster-join
   ```

   Si no se configuró para iniciarse en el tiempo de arranque NTP, aparece un mensaje. 

3. Si decide continuar de todos modos, se le pedirá para la dirección IP de un nodo existente. Escriba la dirección IP. 

4. Si ya no ha configurado un acceso SSH sin contraseña entre ambos equipos, también se le pedirá la contraseña raíz del nodo existente. 

   Después de iniciar sesión el nodo especificado, el script copia la configuración de Corosync, configura SSH y `Csync2`y pone el equipo actual en línea como nuevo nodo de clúster. Aparte de eso, se inicia el servicio necesario para Hawk. Si ha configurado el almacenamiento compartido con `OCFS2`, crea también automáticamente en el directorio de punto de montaje para el `OCFS2` sistema de archivos. 

5. Repita los pasos anteriores para todas las máquinas que desea agregar al clúster. 

6. Para obtener información detallada del proceso, consulte `/var/log/ha-cluster-bootstrap.log`. 

1. Compruebe el estado del clúster con `sudo crm status`. Si ha agregado el segundo nodo correctamente, el resultado debería parecerse al siguiente:

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

Después de agregar todos los nodos, compruebe si tiene que ajustar la directiva de quórum de no en las opciones de clúster global. Esto es especialmente importante para los clústeres de dos nodos. Para obtener más información, consulte la sección 4.1.2, opción no-quórum-policy. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Establecer propiedad de clúster clúster-comprobar de nuevo-intervalo

`cluster-recheck-interval` indica el intervalo de sondeo en el que el clúster comprueba los cambios en los parámetros de recursos, las restricciones u otras opciones de clúster. Si una réplica deja de funcionar, el clúster intenta reiniciar la réplica en un intervalo que está limitado por el `failure-timeout` valor y el `cluster-recheck-interval` valor. Por ejemplo, si `failure-timeout` se establece en 60 segundos y `cluster-recheck-interval` se establece en 120 segundos, se prueba el reinicio en un intervalo que es mayor que 60 segundos, pero menos de 120 segundos. Se recomienda establecer tiempo de espera de un error en 60 y volver a comprobar-cluster-interval en un valor que es mayor que 60 segundos. No se recomienda establecer intervalo de volver a comprobar de clúster en un valor pequeño.

Para actualizar el valor de propiedad `2 minutes` ejecutar:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Si ya tiene un recurso de grupo de disponibilidad administrado por un clúster de Pacemaker, tenga en cuenta que todas las distribuciones que usan la última 1.1.18-11.el7 disponible del paquete Pacemaker introducen un cambio de comportamiento para el clúster de inicio-error-es-irrecuperable valor cuando su el valor es false. Este cambio afecta el flujo de trabajo de conmutación por error. Si una réplica principal sufre una interrupción, se espera el clúster de conmutación por error a una de las réplicas secundarias disponibles. En su lugar, los usuarios observarán que el clúster sigue intentando iniciar la réplica principal con errores. Si ese principal nunca se pone en línea (debido a una interrupción permanente), el clúster nunca conmuta por error a otra réplica secundaria disponible. Debido a este cambio, una configuración recomendada anteriormente para establecer inicio-error-es-irrecuperable ya no es válida y debe volver al valor predeterminado de la configuración `true`. Además, el recurso de grupo de disponibilidad debe actualizarse para incluir el `failover-timeout` propiedad. 
>
>Para actualizar el valor de propiedad `true` ejecutar:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>Actualizar la propiedad de recurso de grupo de disponibilidad existente `failure-timeout` a `60s` ejecutar (reemplace `ag1` con el nombre del recurso de grupo de disponibilidad): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Para obtener más información sobre las propiedades de clúster de Pacemaker, vea [configurar recursos de clúster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

## <a name="configure-fencing-stonith"></a>Configurar vallado (STONITH)
Los proveedores de clúster de pacemaker requieren STONITH esté habilitado y un dispositivo de vallado configurado para una configuración de clúster compatibles. Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, vallado sirve para poner el clúster en un estado conocido de nuevo.

Vallado de nivel de recurso principalmente garantiza que no hay ningún daño de datos durante una interrupción mediante la configuración de un recurso. Puede usar la barrera de nivel de recurso, por ejemplo, con DRBD (distribuida replica bloque dispositivo) para marcar el disco en un nodo como obsoletos cuando el vínculo de comunicación deja de funcionar.

Vallado de nivel de nodo, se garantiza que un nodo no ejecuta todos los recursos. Para ello, al restablecer el nodo y su implementación Pacemaker se denomina STONITH (que es el acrónimo "grabar el otro nodo en el encabezado"). Pacemaker es compatible con una gran variedad de dispositivos, como tarjetas de interfaz de una fuente de alimentación o de administración de alimentación ininterrumpida para servidores de barrera.

Para obtener más información, consulte [clústeres de Pacemaker desde cero](https://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [vallado y Stonith](https://clusterlabs.org/doc/crm_fencing.html) y [documentación de alta disponibilidad de SUSE: vallado y STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

En tiempo de inicialización de clúster, STONITH está deshabilitada si no se detecta ninguna configuración. Se puede habilitar más tarde ejecutando el comando siguiente:

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar a Pacemaker en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y déjela habilitada. SUSE no proporciona a vallado agentes para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad para ejecutar clústeres de producción en estos entornos. Estamos trabajando en una solución para este vacío que estará disponible en futuras versiones.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar los recursos de clúster de SQL Server

Consulte [SLES administración Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>Habilitar Pacemaker

Habilitar a Pacemaker, por lo que se inicie automáticamente.

Ejecute el siguiente comando en todos los nodos del clúster.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>Crear recurso de grupo de disponibilidad

El siguiente comando crea y configura el recurso de grupo de disponibilidad de tres réplicas de grupo de disponibilidad [ag1]. La supervisión de operaciones y los tiempos de espera tienen que especificarse explícitamente en SLES basada en el hecho que los tiempos de espera son altamente dependientes de la carga de trabajo y deben ajustarse cuidadosamente para cada implementación.
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
      meta failure-timeout=60s \
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

### <a name="create-virtual-ip-resource"></a>Crear recurso IP virtual

Si no ha creado el recurso IP virtual cuando ejecutó `ha-cluster-init` ahora puede crear este recurso. El siguiente comando crea un recurso IP virtual. Reemplace `<**0.0.0.0**>` con una dirección disponible en la red y `<**24**>` con el número de bits de la máscara de subred CIDR. Ejecutar en un nodo.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Agregar restricción de colocación
Prácticamente cualquier decisión en un clúster de Pacemaker, como elegir dónde se debe ejecutar un recurso, se realiza mediante la comparación de puntuaciones. Las puntuaciones se calculan por recurso y cluster resource manager elige el nodo con la puntuación más alta para un recurso determinado. (Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.) Se pueden manipular las decisiones del clúster con las restricciones. Las restricciones tienen una puntuación. Si una restricción tiene una puntuación menor que infinito, es sólo una recomendación. Una puntuación de infinito significa que es imprescindible. Queremos asegurarnos de que principal del grupo de disponibilidad y el virtual recurso de ip se ejecutan en el mismo host, por lo que se define una restricción de colocación con una puntuación de infinito. 

Para establecer la restricción de colocación de la dirección IP virtual ejecutar en el mismo nodo que el maestro, ejecute el siguiente comando en un nodo:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Agregar restricción de ordenación
La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que mueva el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos: 

1. Migrar recursos de problemas del usuario al maestro del grupo de disponibilidad del Nodo1 al Nodo2.
2. El recurso IP virtual se detiene en el nodo 1.
3. El recurso IP virtual se inicia en el nodo 2. En este momento, la dirección IP temporalmente puntos al nodo 2 mientras el nodo 2 sigue siendo un pre-conmutación por error secundaria. 
4. El maestro de grupo de disponibilidad en el nodo 1 se degrada para subordinado.
5. El subordinado del grupo de disponibilidad en el nodo 2 se promueve al maestro. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior a la conmutación por error, agregue una restricción de ordenación. Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede utilizar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio de SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En SLES usar `crm`. 

Conmutar por error manualmente el grupo de disponibilidad con `crm`. No iniciar la conmutación por error con Transact-SQL. Para obtener más información, consulte [conmutación por error](sql-server-linux-availability-group-failover-ha.md#failover).


Para obtener más información, vea:
- [Administración de recursos de clúster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [Alta disponibilidad de conceptos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Referencia rápida de pacemaker](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)
