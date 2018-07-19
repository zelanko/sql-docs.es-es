---
title: Configuración de clúster RHEL para el grupo de disponibilidad de SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: 784f98acb1e8223e14d3f1e1a74e73cfdc3561bc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057213"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Configuración de clúster RHEL para el grupo de disponibilidad de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica cómo crear un clúster de grupo de disponibilidad de tres nodos para SQL Server en Red Hat Enterprise Linux. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El nivel de agrupación en clústeres se basa en Red Hat Enterprise Linux (RHEL) [complemento de alta disponibilidad](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) construidos sobre [Pacemaker](http://clusterlabs.org/). 

> [!NOTE] 
> El acceso a la documentación completa de Red Hat requiere una suscripción válida. 

Para obtener más información sobre la configuración del clúster, las opciones de los agentes de recursos y administración, visite [documentación de referencia RHEL](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> SQL Server no está integrado estrechamente como con Pacemaker en Linux como sucede con la agrupación en clústeres de conmutación por error de Windows Server. Una instancia de SQL Server no es consciente del clúster. Pacemaker proporciona orquestación de recursos de clúster. Además, el nombre de red virtual es específico para la agrupación en clústeres de conmutación por error de Windows Server: no hay ningún equivalente en Pacemaker. Vistas de administración dinámica de grupo de disponibilidad (DMV) que consultar la información de clúster, devuelven filas vacías en clústeres de Pacemaker. Para crear un agente de escucha para la reconexión después de la conmutación por error transparente, registrar manualmente el nombre de agente de escucha en el DNS con la dirección IP usada para crear el recurso IP virtual. 

Las siguientes secciones se recorra los pasos para configurar un clúster de Pacemaker y agregar un grupo de disponibilidad como recurso en el clúster de alta disponibilidad.

## <a name="roadmap"></a>Mapa de ruta

Los pasos para crear un grupo de disponibilidad en los servidores de Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto nivel: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar un administrador de recursos de clúster, como Pacemaker. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos del clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Entornos de producción requieren a un agente de vallado, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de vallado. Las demostraciones son para pruebas y validación solo. 
   
   >Un clúster de Linux usa vallado para devolver el clúster a un estado conocido. La manera de configurar vallado depende de la distribución y el entorno. Actualmente, la barrera no está disponible en algunos entornos de nube. Para obtener más información, consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440).

5. [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Configurar la alta disponibilidad para RHEL

Para configurar alta disponibilidad para RHEL, habilitar la suscripción de alta disponibilidad y, a continuación, configure Pacemaker.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Habilitación de la suscripción de alta disponibilidad para RHEL

Cada nodo del clúster debe tener una suscripción adecuada para RHEL y la alta disponibilidad agregar en. Revise los requisitos en [cómo instalar paquetes de clúster de alta disponibilidad en Red Hat Enterprise Linux](http://access.redhat.com/solutions/45930). Siga estos pasos para configurar la suscripción y repositorios:

1. Registrar el sistema.

   ```bash
   sudo subscription-manager register
   ```

   Proporcione el nombre de usuario y la contraseña.   

1. Lista de los grupos disponibles para el registro.

   ```bash
   sudo subscription-manager list --available
   ```

   En la lista de grupos de disponibilidad, tenga en cuenta el identificador del grupo de la suscripción de alta disponibilidad.

1. Actualice el script siguiente. Reemplace `<pool id>` con el identificador del grupo de alta disponibilidad en el paso anterior. Ejecute el script para adjuntar la suscripción.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Habilitación del repositorio.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Para obtener más información, consulte [del clúster de Pacemaker: el código abierto, alta disponibilidad](http://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/). 

Después de haber configurado la suscripción, complete los pasos siguientes para configurar a Pacemaker:

### <a name="configure-pacemaker"></a>Configuración de Pacemaker

Después de registrar la suscripción, complete los pasos siguientes para configurar a Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Después de que Pacemaker se configura, utilice `pcs` para interactuar con el clúster. Ejecutar todos los comandos en un nodo del clúster. 

## <a name="configure-fencing-stonith"></a>Configurar vallado (STONITH)

Los proveedores de clúster de pacemaker requieren STONITH esté habilitado y un dispositivo de vallado configurado para una configuración de clúster compatibles. STONITH es el acrónimo "grabar el otro nodo en el encabezado". Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, vallado pone el clúster a un estado conocido de nuevo.

Vallado de nivel de recursos garantiza que no hay ningún daño de datos en el caso de una interrupción del servicio mediante la configuración de un recurso. Por ejemplo, puede usar vallado de nivel de recurso para marcar el disco en un nodo como obsoletos cuando deja de funcionar el vínculo de comunicación. 

Vallado de nivel de nodo, se garantiza que un nodo no ejecuta todos los recursos. Para ello, al restablecer el nodo. Pacemaker es compatible con una gran variedad de dispositivos de la barrera. Algunos ejemplos son tarjetas de interfaz de una fuente de alimentación o de administración de alimentación ininterrumpida para servidores.

Para obtener información acerca de STONITH y vallado, consulte los artículos siguientes:

* [Clústeres de pacemaker desde cero](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [Vallado y STONITH](http://clusterlabs.org/doc/crm_fencing.html)
* [Complemento de alta disponibilidad de Red Hat con Pacemaker: vallado](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

Dado que el nivel del nodo Configuración de vallado depende en gran medida en su entorno, deshabilitarla en este tutorial (se puede configurar más adelante). El script siguiente deshabilita la barrera de nivel de nodo:

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar a Pacemaker en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y déjela habilitada. RHEL no proporciona a vallado agentes para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad para ejecutar clústeres de producción en estos entornos. Estamos trabajando en una solución para este vacío que estará disponible en futuras versiones.

## <a name="set-cluster-property-cluster-recheck-interval"></a>Establecer propiedad de clúster clúster-comprobar de nuevo-intervalo

`cluster-recheck-interval` indica el intervalo de sondeo en el que el clúster comprueba los cambios en los parámetros de recursos, las restricciones u otras opciones de clúster. Si una réplica deja de funcionar, el clúster intenta reiniciar la réplica en un intervalo que está limitado por el `failure-timeout` valor y el `cluster-recheck-interval` valor. Por ejemplo, si `failure-timeout` se establece en 60 segundos y `cluster-recheck-interval` se establece en 120 segundos, se prueba el reinicio en un intervalo que es mayor que 60 segundos, pero menos de 120 segundos. Se recomienda establecer tiempo de espera de un error en 60 y volver a comprobar-cluster-interval en un valor que es mayor que 60 segundos. No se recomienda establecer intervalo de volver a comprobar de clúster en un valor pequeño.

Para actualizar el valor de propiedad `2 minutes` ejecutar:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Todas las distribuciones (incluidos RHEL 7.3 y 7.4) que usan la última 1.1.18-11.el7 disponible del paquete Pacemaker introducen un cambio de comportamiento para la configuración de clúster inicio-error-es-grave cuando su valor es false. Este cambio afecta el flujo de trabajo de conmutación por error. Si una réplica principal sufre una interrupción, se espera el clúster de conmutación por error a una de las réplicas secundarias disponibles. En su lugar, los usuarios observarán que el clúster sigue intentando iniciar la réplica principal con errores. Si ese principal nunca se pone en línea (debido a una interrupción permanente), el clúster nunca conmuta por error a otra réplica secundaria disponible. Debido a este cambio, una configuración recomendada anteriormente para establecer inicio-error-es-irrecuperable ya no es válida y debe volver al valor predeterminado de la configuración `true`. Además, el recurso de grupo de disponibilidad debe actualizarse para incluir el `failover-timeout` propiedad. 

Para actualizar el valor de propiedad `true` ejecutar:

```bash
sudo pcs property set start-failure-is-fatal=true
```

Para actualizar el `ag1` propiedad de recurso `failure-timeout` a `60s` ejecutar:

```bash
pcs resource update ag1 meta failure-timeout=60s
```


Para obtener información sobre las propiedades de clúster de Pacemaker, vea [propiedades de clústeres de Pacemaker](http://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para Pacemaker

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crear recurso de grupo de disponibilidad

Para crear el recurso de grupo de disponibilidad, use `pcs resource create` comando y establezca las propiedades del recurso. El comando siguiente crea un `ocf:mssql:ag` maestro/subordinado el recurso de tipo para el grupo de disponibilidad con el nombre `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Crear recurso IP virtual

Para crear el recurso de dirección IP virtual, ejecute el siguiente comando en un nodo. Use una dirección IP estática disponible desde la red. Reemplace la dirección IP entre `<10.128.16.240>` con una dirección IP válida.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

No hay ningún nombre de servidor virtual equivalente en Pacemaker. Para usar una cadena de conexión que apunta a un nombre de servidor de la cadena en lugar de una dirección IP, registrar la dirección del recurso IP virtual y el nombre del servidor virtual deseado en DNS. Para las configuraciones de recuperación ante desastres, registre el nombre del servidor virtual deseado y la dirección IP con los servidores DNS en principal y el sitio de recuperación ante desastres.

## <a name="add-colocation-constraint"></a>Agregar restricción de colocación

Prácticamente cualquier decisión en un clúster de Pacemaker, como elegir dónde se debe ejecutar un recurso, se realiza mediante la comparación de puntuaciones. Las puntuaciones se calculan por recurso. Cluster resource manager elige el nodo con la puntuación más alta para un recurso determinado. Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.

En un clúster de pacemaker, puede manipular las decisiones del clúster con las restricciones. Las restricciones tienen una puntuación. Si una restricción tiene una puntuación inferior `INFINITY`, Pacemaker considera como recomendación. Una puntuación de `INFINITY` es obligatorio.

Para garantizar que la réplica principal y los recursos de dirección ip virtual se ejecutan en el mismo host, definir una restricción de colocación con una puntuación de infinito. Para agregar la restricción de colocación, ejecute el siguiente comando en un nodo.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Agregar restricción de ordenación

La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que mueva el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos:

1. Problemas de usuarios `pcs resource move` al grupo de disponibilidad principal del Nodo1 al Nodo2.
1. El recurso IP virtual se detiene en el nodo 1.
1. El recurso IP virtual se inicia en el nodo 2.
  
   >[!NOTE]
   >En este momento, la dirección IP temporalmente puntos al nodo 2 mientras el nodo 2 sigue siendo un pre-conmutación por error secundaria. 
   
1. El grupo de disponibilidad principal en el nodo 1 se degrada al secundario.
1. El grupo de disponibilidad secundario en el nodo 2 se promueve a principal. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior a la conmutación por error, agregue una restricción de ordenación. 

Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede utilizar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio de SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs` y está en uso SLES `crm` herramientas. 

Conmutar por error manualmente el grupo de disponibilidad con `pcs`. No se inicie la conmutación por error con Transact-SQL. Para obtener instrucciones, consulte [conmutación por error](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)
