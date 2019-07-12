---
title: Configurar clúster de Ubuntu para el grupo de disponibilidad de SQL Server
titleSuffix: SQL Server
description: Obtenga información acerca de cómo crear clústeres de grupo de disponibilidad para Ubuntu
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 39753e86cc4d6f82d8bddb0c10356d9be172e90f
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834332"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar el clúster de Ubuntu y recursos del grupo de disponibilidad

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica cómo crear un clúster de tres nodos en Ubuntu y agregar un grupo de disponibilidad creado anteriormente como un recurso en el clúster. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos, consulte [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> En este momento, integración de SQL Server con Pacemaker en Linux no es tan acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y Pacemaker controla el servicio como una instancia independiente. Además, nombre de red virtual es WSFC específico, no hay ningún equivalente de la misma en Pacemaker. Siempre en vistas de administración dinámica que consultar la información de clúster, se devuelven filas vacías. Puede crear un agente de escucha para que lo utilicen para la reconexión después de la conmutación por error transparente, pero tendrá que registrar manualmente el nombre de agente de escucha en el servidor DNS con la dirección IP usada para crear el recurso IP virtual (como se explica en las secciones siguientes).

Las siguientes secciones se guiarán por los pasos para configurar una solución de clúster de conmutación por error. 

## <a name="roadmap"></a>Roadmap

Los pasos para crear un grupo de disponibilidad en los servidores de Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto nivel: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar un administrador de recursos de clúster, como Pacemaker. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos del clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Entornos de producción requieren a un agente de vallado, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de vallado. Las demostraciones son para pruebas y validación solo. 
   
   >Un clúster de Linux usa vallado para devolver el clúster a un estado conocido. La manera de configurar vallado depende de la distribución y el entorno. En este momento, la barrera no está disponible en algunos entornos de nube. Consulte [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440) para obtener más información.

5.  [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalación y configuración de Pacemaker en cada nodo del clúster

1. En todos los nodos, abra los puertos de firewall. Abra el puerto para el servicio de alta disponibilidad de Pacemaker, instancia de SQL Server y el punto de conexión del grupo de disponibilidad. El puerto TCP predeterminado para el servidor que ejecuta SQL Server es 1433.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   Como alternativa, puede deshabilitar el firewall:
        
   ```bash
   sudo ufw disable
   ```

1. Instalar paquetes de Pacemaker. En todos los nodos, ejecute los siguientes comandos:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Use la misma contraseña en todos los nodos. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Habilitar e iniciar el servicio pcsd y Pacemaker

El siguiente comando habilita y pacemaker y pcsd servicio inicia. Ejecutar en todos los nodos. Esto permite que los nodos se unan al clúster después del reinicio. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Habilitar pacemaker comando puede completar con el error 'pacemaker inicio predeterminado contiene no hay niveles de ejecución, anulando'. Esto es inofensivo, puede continuar la configuración de clúster. 

## <a name="create-the-cluster"></a>Crear el clúster

1. Quite cualquier configuración de clúster existente de todos los nodos. 

   Ejecución 'sudo apt-get install PC' pcs, corosync y pacemaker instalan al mismo tiempo y empieza a ejecutarse todos los 3 de los servicios.  A partir de corosync genera una plantilla de ' / etc/cluster/corosync.conf' archivo.  Para que los pasos siguientes se realizan correctamente este archivo no debería existir: por lo que la solución consiste en Detener pacemaker y corosync y eliminar ' / etc/cluster/corosync.conf', y, a continuación, completaron correctamente los pasos siguientes. 'pcs cluster destroy' hace lo mismo, y puede usarlo como un paso de configuración inicial del clúster de tiempo.
   
   El comando siguiente quita los archivos de configuración de clúster existentes y detiene todos los servicios de cluster Server. Esto destruye el clúster de forma permanente. Ejecútelo como primer paso en un entorno de preproducción. Tenga en cuenta que "pcs cluster destroy' deshabilitado el servicio pacemaker y debe volver a habilitar. Ejecute el siguiente comando en todos los nodos.
   
   >[!WARNING]
   >El comando destruye cualquier recurso de clúster existente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Cree el clúster. 

   >[!WARNING]
   >Debido a un problema conocido que el proveedor de la agrupación en clústeres está investigando, comenzando en el clúster ("pcs cluster start") produce un error con el siguiente error. Esto es porque el archivo de registro configurado en /etc/corosync/corosync.conf que se crea cuando el comando de instalación de clúster se ejecute, es incorrecto. Para solucionar este problema, cambie el archivo de registro: /var/log/corosync/corosync.log. También puede crear el archivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
El siguiente comando crea un clúster de tres nodos. Antes de ejecutar el script, reemplace los valores entre `< ... >`. Ejecute el siguiente comando en el nodo principal. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Si ya ha configurado un clúster en los mismos nodos, debe usar la opción "--force" al ejecutar "pcs cluster setup". Tenga en cuenta que esto equivale a ejecutar "pcs cluster destroy" y que el servicio Pacemaker debe volver a habilitarse mediante "sudo systemctl enable pacemaker".


## <a name="configure-fencing-stonith"></a>Configurar vallado (STONITH)

Los proveedores de clúster de pacemaker requieren STONITH esté habilitado y un dispositivo de vallado configurado para una configuración de clúster compatibles. Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, vallado sirve para poner el clúster en un estado conocido de nuevo. Vallado de nivel de recurso principalmente garantiza que no hay ningún daño de datos en el caso de una interrupción del servicio mediante la configuración de un recurso. Puede usar la barrera de nivel de recurso, por ejemplo, con DRBD (distribuida replica bloque dispositivo) para marcar el disco en un nodo como obsoletos cuando el vínculo de comunicación deja de funcionar. Vallado de nivel de nodo, se garantiza que un nodo no ejecuta todos los recursos. Para ello, al restablecer el nodo y su implementación Pacemaker se denomina STONITH (que es el acrónimo "grabar el otro nodo en el encabezado"). Pacemaker es compatible con una gran variedad de dispositivos de vallado, por ejemplo, una fuente de alimentación ininterrumpida o administración de tarjetas de interfaz de servidores. Para obtener más información, consulte [clústeres de Pacemaker desde cero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/) y [vallado y Stonith](https://clusterlabs.org/doc/crm_fencing.html) 

Dado que el nivel del nodo Configuración de vallado depende en gran medida en su entorno, se deshabilita para este tutorial (se puede configurar en un momento posterior). Ejecute el siguiente script en el nodo principal: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar a Pacemaker en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y déjela habilitada. Tenga en cuenta que en este momento no hay ningún agente de barrera para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad para ejecutar clústeres de producción en estos entornos. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Establecer propiedad de clúster clúster-comprobar de nuevo-intervalo

`cluster-recheck-interval` indica el intervalo de sondeo en el que el clúster comprueba los cambios en los parámetros de recursos, las restricciones u otras opciones de clúster. Si una réplica deja de funcionar, el clúster intenta reiniciar la réplica en un intervalo que está limitado por el `failure-timeout` valor y el `cluster-recheck-interval` valor. Por ejemplo, si `failure-timeout` se establece en 60 segundos y `cluster-recheck-interval` se establece en 120 segundos, se prueba el reinicio en un intervalo que es mayor que 60 segundos, pero menos de 120 segundos. Se recomienda establecer tiempo de espera de un error en 60 y volver a comprobar-cluster-interval en un valor que es mayor que 60 segundos. No se recomienda establecer intervalo de volver a comprobar de clúster en un valor pequeño.

Para actualizar el valor de propiedad `2 minutes` ejecutar:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Si ya tiene un recurso de grupo de disponibilidad administrado por un clúster de Pacemaker, tenga en cuenta que todas las distribuciones que usan la última 1.1.18-11.el7 disponible del paquete Pacemaker introducen un cambio de comportamiento para el clúster de inicio-error-es-irrecuperable valor cuando su el valor es false. Este cambio afecta el flujo de trabajo de conmutación por error. Si una réplica principal sufre una interrupción, se espera el clúster de conmutación por error a una de las réplicas secundarias disponibles. En su lugar, los usuarios observarán que el clúster sigue intentando iniciar la réplica principal con errores. Si ese principal nunca se pone en línea (debido a una interrupción permanente), el clúster nunca conmuta por error a otra réplica secundaria disponible. Debido a este cambio, una configuración recomendada anteriormente para establecer inicio-error-es-irrecuperable ya no es válida y debe volver al valor predeterminado de la configuración `true`. Además, el recurso de grupo de disponibilidad debe actualizarse para incluir el `failover-timeout` propiedad. 
>
>Para actualizar el valor de propiedad `true` ejecutar:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Actualizar la propiedad de recurso de grupo de disponibilidad existente `failure-timeout` a `60s` ejecutar (reemplace `ag1` con el nombre del recurso de grupo de disponibilidad):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instale el agente de recursos de SQL Server para la integración con Pacemaker

Ejecute los siguientes comandos en todos los nodos. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crear recurso de grupo de disponibilidad

Para crear el recurso de grupo de disponibilidad, use `pcs resource create` comando y establezca las propiedades del recurso. Comando siguiente crea un `ocf:mssql:ag` maestro/subordinado el recurso de tipo para el grupo de disponibilidad con el nombre `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Crear recurso IP virtual

Para crear el recurso de dirección IP virtual, ejecute el siguiente comando en un nodo. Use una dirección IP estática disponible desde la red. Antes de ejecutar la secuencia de comandos, reemplace los valores comprendidos entre `< ... >` con una dirección IP válida.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

No hay ningún nombre de servidor virtual equivalente en Pacemaker. Para usar una cadena de conexión que apunta a un nombre de servidor de la cadena y no usar la dirección IP, registrar la dirección del recurso IP y el nombre de servidor virtual que desee en DNS. Para las configuraciones de recuperación ante desastres, registre el nombre del servidor virtual deseado y la dirección IP con los servidores DNS en principal y el sitio de recuperación ante desastres.

## <a name="add-colocation-constraint"></a>Agregar restricción de colocación

Prácticamente cualquier decisión en un clúster de Pacemaker, como elegir dónde se debe ejecutar un recurso, se realiza mediante la comparación de puntuaciones. Las puntuaciones se calculan por recurso y cluster resource manager elige el nodo con la puntuación más alta para un recurso determinado. (Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.) Use restricciones para configurar las decisiones del clúster. Las restricciones tienen una puntuación. Si una restricción tiene una puntuación menor que infinito, es sólo una recomendación. Una puntuación de infinito significa que es obligatorio. Para asegurarse de que la réplica principal y el recurso de dirección ip virtual están en el mismo host, definir una restricción de colocación con una puntuación de infinito. Para agregar la restricción de colocación, ejecute el siguiente comando en un nodo. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Agregar restricción de ordenación

La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que mueva el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos:

1. Problemas de usuarios `pcs resource move` al grupo de disponibilidad principal del Nodo1 al Nodo2.
1. El recurso IP virtual se detiene en el nodo 1.
1. El recurso IP virtual se inicia en el nodo 2.

   >[!NOTE]
   >En este momento, la dirección IP temporalmente puntos al Nodo2 mientras Nodo2 sigue siendo un pre-conmutación por error secundaria. 
   
1. El grupo de disponibilidad principal en el Nodo1 se degrada al secundario.
1. El grupo de disponibilidad secundario en el nodo 2 se promueve a principal. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior a la conmutación por error, agregue una restricción de ordenación. 

Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede utilizar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio de SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)

