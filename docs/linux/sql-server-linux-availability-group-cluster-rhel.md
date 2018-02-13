---
title: "Configuración de clúster RHEL para grupo de disponibilidad de SQL Server | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.workload: Inactive
ms.openlocfilehash: c90eb7d5f11456a13dfa3d4354070bc506d030e5
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Configuración de clúster RHEL para grupo de disponibilidad de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica cómo crear un clúster de grupo de disponibilidad de tres nodos para SQL Server en Red Hat Enterprise Linux. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos: vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md). El nivel de agrupación en clústeres se basa en los servicios de Red Hat Enterprise Linux (RHEL) [complemento HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) construidos sobre [marcapasos](http://clusterlabs.org/). 

> [!NOTE] 
> Acceso a la documentación completa de Red Hat requiere una suscripción válida. 

Para obtener más información sobre la configuración del clúster y opciones de agentes de recursos, administración, visite [documentación de referencia RHEL](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> SQL Server no está integrado estrechamente como con marcapasos en Linux tal cual con los clústeres de conmutación por error de Windows Server. Una instancia de SQL Server no es consciente del clúster. Marcapasos proporciona la orquestación de recurso de clúster. Además, el nombre de red virtual es específico para clústeres de conmutación por error de Windows Server: no hay ningún equivalente en marcapasos. Vistas de administración dinámica de grupo de disponibilidad (DMV) que consultar la información de clúster devuelven filas vacías en clústeres marcapasos. Para crear un agente de escucha para la reconexión transparente después de la conmutación por error, registrar manualmente el nombre de agente de escucha en DNS con la dirección IP utilizada para crear el recurso IP virtual. 

En las siguientes secciones abordan los pasos para configurar un clúster marcapasos y agregar un grupo de disponibilidad como recurso en el clúster de alta disponibilidad.

## <a name="roadmap"></a>Roadmap

Los pasos para crear un grupo de disponibilidad en servidores Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente describe los pasos generales: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar un administrador de recursos de clúster, como marcapasos. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos de clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Los entornos de producción requieren a un agente de barrera, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de barrera. Las demostraciones son para pruebas y la validación solo. 
   
   >Un clúster de Linux usa barrera para devolver el clúster a un estado conocido. La manera de configurar la barrera depende de la distribución y el entorno. Actualmente, la barrera no está disponible en algunos entornos de nube. Para obtener más información, consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440).

5. [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Configurar alta disponibilidad para RHEL

Para configurar alta disponibilidad para RHEL, habilite la suscripción de alta disponibilidad y, a continuación, configurar a marcapasos.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Habilitar la suscripción de alta disponibilidad para RHEL

Cada nodo del clúster debe tener una suscripción adecuada para RHEL y la alta disponibilidad agregar. Revise los requisitos en [cómo instalar paquetes de clúster de alta disponibilidad en Red Hat Enterprise Linux](http://access.redhat.com/solutions/45930). Siga estos pasos para configurar la suscripción y repositorios:

1. Registrar el sistema.

   ```bash
   sudo subscription-manager register
   ```

   Proporcione el nombre de usuario y la contraseña.   

1. Lista de los grupos disponibles para el registro.

   ```bash
   sudo subscription-manager list --available
   ```

   En la lista de grupos de, tenga en cuenta el identificador del grupo de la suscripción de alta disponibilidad.

1. Actualice la siguiente secuencia de comandos. Reemplace `<pool id>` con el identificador del grupo de alta disponibilidad en el paso anterior. Ejecute el script para adjuntar la suscripción.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Habilitar el repositorio.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Para obtener más información, consulte [marcapasos: el código abierto, alta disponibilidad de clúster](http://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/). 

Después de haber configurado la suscripción, complete los pasos siguientes para configurar a marcapasos:

### <a name="configure-pacemaker"></a>Configurar marcapasos

Después de registrar la suscripción, complete los pasos siguientes para configurar a marcapasos:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Después de configurar marcapasos, use `pcs` para interactuar con el clúster. Ejecutar todos los comandos en un nodo del clúster. 

## <a name="configure-fencing-stonith"></a>Configurar la barrera (STONITH)

Los proveedores de clúster marcapasos requieren STONITH esté habilitado y un dispositivo de barrera configurado para una instalación de clúster compatibles. STONITH es el acrónimo "grabar el otro nodo en el encabezado". Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, barrera pone el clúster a un estado conocido de nuevo.

Barrera de nivel de recurso se asegura de que no hay ningún daños en los datos en el caso de una interrupción del sistema mediante la configuración de un recurso. Por ejemplo, puede usar barrera de nivel de recurso para marcar el disco en un nodo como obsoleto cuando el vínculo de comunicación deja de funcionar. 

Barrera de nivel de nodo se asegura de que un nodo no ejecuta todos los recursos. Esto se realiza mediante el restablecimiento del nodo. Marcapasos admite una gran variedad de dispositivos de barrera. Algunos ejemplos son tarjetas de interfaz de una fuente de alimentación o de administración de sistema de alimentación ininterrumpida para servidores.

Para obtener información acerca de STONITH y la barrera, vea los siguientes artículos:

* [Clústeres de marcapasos desde el principio](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [Barrera y STONITH](http://clusterlabs.org/doc/crm_fencing.html)
* [Complemento de alta disponibilidad de Red Hat con marcapasos: barrera](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

Puesto que el nivel del nodo Configuración de barrera depende en gran medida en su entorno, deshabilítelo para este tutorial (se puede configurar más adelante). El script siguiente deshabilita la barrera de nivel de nodo:

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar marcapasos en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y manténgala habilitada. RHEL no proporciona a agentes de barrera para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad con la ejecución de clústeres de producción en estos entornos. Estamos trabajando en una solución para este vacío que estará disponible en futuras versiones.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Establecer propiedades de clúster inicio error-es-grave en false

`start-failure-is-fatal` indica si un error al iniciar un recurso en un nodo impide más intentos de inicio en ese nodo. Cuando se establece en `false`, el clúster decide si debe intentar iniciar en el mismo nodo nuevo, en función actual error recuento y migración el umbral del recurso. Después de producirse la conmutación por error, a partir de la disponibilidad de reintentos de marcapasos recurso de grupo en la primera estructura principal una vez que la instancia de SQL está disponible. Marcapasos degrada la réplica de base de datos secundaria y vuelve a unirse automáticamente el grupo de disponibilidad. 

Para actualizar el valor de propiedad para `false` ejecutar:

```bash
sudo pcs property set start-failure-is-fatal=false
```

>[!WARNING]
>Después de una conmutación por error automática, cuando `start-failure-is-fatal = true` el Administrador de recursos intentará iniciar el recurso. Si se produce un error en el primer intento, ejecute manualmente `pcs resource cleanup <resourceName>` para limpiar el recuento de errores de recursos y restablecer la configuración.

Para obtener información sobre propiedades de clúster marcapasos, consulte [marcapasos clústeres propiedades](http://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para marcapasos

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crear el recurso de grupo de disponibilidad

Para crear el recurso de grupo de disponibilidad, utilice `pcs resource create` comando y establezca las propiedades del recurso. El comando siguiente crea un `ocf:mssql:ag` maestro/esclavo el recurso de tipo para el grupo de disponibilidad con el nombre `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 master notify=true
```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Crear el recurso de IP virtual

Para crear el recurso de dirección IP virtual, ejecute el siguiente comando en un nodo. Use una dirección IP estática disponible desde la red. Reemplace la dirección IP entre `<10.128.16.240>` con una dirección IP válida.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

No hay ningún nombre de servidor virtual equivalente en marcapasos. Para usar una cadena de conexión que apunta a un nombre de servidor de cadena en lugar de una dirección IP, registrar la dirección del recurso IP virtual y el nombre del servidor virtual deseado en DNS. Las configuraciones de recuperación ante desastres, registre el nombre del servidor virtual deseado y la dirección IP con los servidores DNS principal y el sitio de recuperación ante desastres.

## <a name="add-colocation-constraint"></a>Agregar restricción de colocación

Casi cada decisión en un clúster marcapasos, como elegir dónde se debe ejecutar un recurso, se realiza comparando las puntuaciones. Las puntuaciones se calculan por recurso. El Administrador de recursos de clúster elige el nodo con la máxima puntuación de un recurso concreto. Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.

En un clúster marcapasos, puede manipular las decisiones del clúster con restricciones. Las restricciones tienen una puntuación. Si una restricción que tiene una puntuación menor que `INFINITY`, marcapasos considera como recomendación. Una puntuación de `INFINITY` es obligatorio.

Para asegurarse de que la réplica principal y los recursos de dirección ip virtual se ejecutan en el mismo host, defina una restricción de colocación con una puntuación de infinito. Para agregar la restricción de colocación, ejecute el siguiente comando en un nodo.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Agregar restricción de ordenación

La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que pase el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos:

1. Problemas de los usuarios `pcs resource move` al grupo de disponibilidad principal del Nodo1 al Nodo2.
1. El recurso IP virtual se detiene en el nodo 1.
1. El recurso IP virtual se inicia en el nodo 2.
  
   >[!NOTE]
   >En este punto, la dirección IP temporalmente puntos al nodo 2 mientras el nodo 2 sigue siendo una pre-conmutación por error secundario. 
   
1. El grupo de disponibilidad principal en el nodo 1 se degrada a la secundaria.
1. El grupo de disponibilidad secundario en el nodo 2 se promueve a principal. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior la conmutación por error, agregue una restricción de ordenación. 

Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede usar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs` y en uso SLES `crm` herramientas. 

Conmutar por error manualmente el grupo de disponibilidad con `pcs`. No se inicie la conmutación por error con Transact-SQL. Para obtener instrucciones, consulte [conmutación por error](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)
