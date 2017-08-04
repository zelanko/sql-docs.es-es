---
title: "Configurar grupo de disponibilidad de SQL Server del clúster Ubuntu | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7aa90eb3fd0a0ea66ea4b4fa09bd17d3e6887d7e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---

# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar clúster Ubuntu y grupo de disponibilidad de recursos

Este documento explica cómo crear un clúster de tres nodos en Ubuntu y agregar un grupo de disponibilidad creado anteriormente como un recurso en el clúster. Para lograr alta disponibilidad, un grupo de disponibilidad en Linux requiere tres nodos: vea [alta disponibilidad y protección de datos para las configuraciones de grupo de disponibilidad](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> En este momento, la integración de SQL Server con marcapasos en Linux no es como acoplamiento como con WSFC en Windows. Desde dentro de SQL, no hay ningún conocimiento sobre la presencia del clúster, todas las orquestaciones está fuera de y marcapasos controla el servicio como una instancia independiente. Además, el nombre de red virtual es específico de WSFC, no hay ningún equivalente de la misma en marcapasos. Siempre en vistas de administración dinámica que consultar la información de clúster devolverá filas vacías. Puede crear un agente de escucha para usarlo para la reconexión transparente después de la conmutación por error, pero tendrá que registrar manualmente el nombre de agente de escucha en el servidor DNS con la dirección IP utilizada para crear el recurso IP virtual (tal y como se explica más adelante).

En las siguientes secciones abordan los pasos necesarios para configurar una solución de clúster de conmutación por error. 

## <a name="roadmap"></a>Guía básica

Los pasos para crear un grupo de disponibilidad en servidores Linux para lograr alta disponibilidad son diferentes de los pasos en un clúster de conmutación por error de Windows Server. En la lista siguiente se describe los pasos de alto niveles: 

1. [Configurar SQL Server en los nodos del clúster](sql-server-linux-setup.md).

2. [Crear el grupo de disponibilidad](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar un administrador de recursos de clúster, como marcapasos. Estas instrucciones se encuentran en este documento.
   
   La manera de configurar un administrador de recursos de clúster depende de la distribución de Linux específica. 

   >[!IMPORTANT]
   >Los entornos de producción requieren a un agente de barrera, como STONITH para lograr alta disponibilidad. Las demostraciones en esta documentación no utiliza a agentes de barrera. Las demostraciones son para pruebas y la validación solo. 
   
   >Un clúster de Linux usa barrera para devolver el clúster a un estado conocido. La manera de configurar la barrera depende de la distribución y el entorno. En este momento, no está disponible en algunos entornos de nube barrera. Vea [directivas de soporte técnico para alta disponibilidad RHEL clústeres: plataformas de virtualización](https://access.redhat.com/articles/29440) para obtener más información.

5.  [Agregar el grupo de disponibilidad como un recurso en el clúster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar y configurar a marcapasos en cada nodo del clúster

1. En todos los nodos abrir los puertos de firewall. Abra el puerto para el servicio de alta disponibilidad marcapasos, instancia de SQL Server y el punto de conexión del grupo de disponibilidad. El puerto TCP predeterminado para el servidor que ejecuta SQL Server es 1433.  

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

1. Instalar paquetes de marcapasos. En todos los nodos, ejecute los siguientes comandos:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Usar la misma contraseña en todos los nodos. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Habilitar e iniciar el servicio de pcsd y marcapasos

El siguiente comando habilita e inicia marcapasos y el servicio de pcsd. Ejecutar en todos los nodos. Esto permite que los nodos que se va a volver a unirse al clúster después de reiniciar el equipo. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Habilitar marcapasos comando completará con el error "marcapasos inicio predeterminado no contiene niveles de ejecución, anulando". Esto es inofensivo, pueda continuar la configuración de clúster. Le estamos seguimiento una con los proveedores de clúster para corregir este problema.

## <a name="create-the-cluster"></a>Crear el clúster

1. Quite cualquier configuración de clústeres existentes de todos los nodos. 

   'Sudo instalación apt get PC en ejecución' marcapasos, corosync y equipos instala al mismo tiempo y empieza a ejecutarse todos los 3 de los servicios.  A partir de corosync genera una plantilla de ' / etc/cluster/corosync.conf' archivo.  Tener pasos correctamente este archivo no deben existir: por lo que la solución consiste en Detener marcapasos / corosync y eliminar ' / etc/cluster/corosync.conf', y, a continuación, los pasos siguientes se completaron correctamente. 'destruir el clúster de equipos' hace lo mismo, y se puede usar como un paso de la configuración de tiempo inicial del clúster.
   
   El comando siguiente quita los archivos de configuración de clúster existentes y detiene todos los servicios de cluster Server. Esto destruye el clúster de forma permanente. Ejecútelo como primer paso en un entorno de preproducción. Tenga en cuenta que 'equipos clúster destruir' deshabilitado el servicio marcapasos y necesita volver a habilitar. Ejecute el siguiente comando en todos los nodos.
   
   >[!WARNING]
   >El comando destruirá cualquier recurso de clúster existente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Crear el clúster. 

   >[!WARNING]
   >Debido a un problema conocido que el proveedor de la agrupación en clústeres está investigando el problema, a partir de generará un error con el clúster ('inicio de clúster de equipos') debajo de error. Esto es porque el archivo de registro configurado en /etc/corosync/corosync.conf es incorrecto. Para solucionar este problema, cambie el archivo de registro: /var/log/corosync/corosync.log. También puede crear el archivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
El comando siguiente crea un clúster de tres nodos. Antes de ejecutar la secuencia de comandos, reemplace los valores entre `**< ... >**`. Ejecute el siguiente comando en el nodo principal. 

   ```bash
   sudo pcs cluster auth **<node1>** **<node2>** **<node3>** -u hacluster -p **<password for hacluster>**
   sudo pcs cluster setup --name **<clusterName>** **<node1>** **<node2…>** **<node3>**
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Si ya ha configurado un clúster en los mismos nodos, debe usar la opción "--force" al ejecutar "pcs cluster setup". Tenga en cuenta que esto equivale a ejecutar "pcs cluster destroy" y que el servicio Pacemaker debe volver a habilitarse mediante "sudo systemctl enable pacemaker".


## <a name="configure-fencing-stonith"></a>Configurar la barrera (STONITH)

Los proveedores de clúster marcapasos requieren STONITH esté habilitado y un dispositivo de barrera configurado para una instalación de clúster compatibles. Cuando el Administrador de recursos de clúster no puede determinar el estado de un nodo o de un recurso en un nodo, barrera se utiliza para poner el clúster en un estado conocido de nuevo. Barrera de nivel de recurso principalmente garantiza que no hay ningún daños en los datos en el caso de una interrupción del sistema mediante la configuración de un recurso. Puede usar la barrera de nivel de recurso, por ejemplo, con DRBD (Distributed replican bloque dispositivo) para marcar el disco en un nodo como obsoleto cuando el vínculo de comunicación deja de funcionar. Barrera de nivel de nodo se asegura de que un nodo no ejecuta todos los recursos. Para ello, restablecer el nodo y la implementación de marcapasos del mismo se denomina STONITH (que es el acrónimo "grabar el otro nodo en el encabezado"). Marcapasos admite una gran variedad de dispositivos de la barrera, por ejemplo, una fuente de alimentación ininterrumpida o administración de tarjetas de interfaz de para los servidores. Para obtener más información, consulte [marcapasos clústeres desde el principio](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) y [barrera y Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Dado que el nivel del nodo Configuración de barrera depende en gran medida en su entorno, se deshabilitará para este tutorial (se puede configurar en un momento posterior). Ejecute el siguiente script en el nodo principal: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Deshabilitar STONITH es solo para fines de prueba. Si tiene previsto usar marcapasos en un entorno de producción, debe planear una implementación de STONITH dependiendo de su entorno y manténgala habilitada. Tenga en cuenta que en este momento no hay ningún agente de barrera para Hyper-V ni entornos de nube (incluido Azure). Por consiguiente, el proveedor de clúster no ofrece compatibilidad con la ejecución de clústeres de producción en estos entornos. Estamos trabajando en una solución para este vacío que estará disponible en futuras versiones.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Establecer propiedades de clúster inicio error-es-grave en false

`start-failure-is-fatal`indica si un error al iniciar un recurso en un nodo impide más intentos de inicio en ese nodo. Cuando se establece en `false`, el clúster decidirá si se intente iniciar en el mismo nodo nuevo, en función actual error recuento y migración el umbral del recurso. Por lo tanto, después de producirse la conmutación por error, marcapasos volverá a intentar iniciar el recurso de grupo de disponibilidad en la primera estructura principal una vez que la instancia de SQL está disponible. Marcapasos degradará la réplica secundaria y vuelve a unir automáticamente el grupo de disponibilidad. 

Para actualizar el valor de propiedad para `false` ejecute el siguiente script:

```bash
sudo pcs property set start-failure-is-fatal=false
```


>[!WARNING]
>Después de una conmutación por error automática, cuando `start-failure-is-fatal = true` el Administrador de recursos intentará iniciar el recurso. Si se produce un error en el primer intento tendrá que ejecutar manualmente `pcs resource cleanup <resourceName>` Liberador de espacio en el recuento de errores de recursos y restablecer la configuración.

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instalar a agente de recursos de SQL Server para la integración con marcapasos

Ejecute los siguientes comandos en todos los nodos. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crear un inicio de sesión de SQL Server para marcapasos

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Crear el recurso de grupo de disponibilidad

Para crear el recurso de grupo de disponibilidad, utilice `pcs resource create` comando y establezca las propiedades del recurso. Comando siguiente crea un `ocf:mssql:ag` maestro/esclavo el recurso de tipo para el grupo de disponibilidad con el nombre `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Crear el recurso de IP virtual

Para crear el recurso de dirección IP virtual, ejecute el siguiente comando en un nodo. Use una dirección IP estática disponible desde la red. Antes de ejecutar la secuencia de comandos, reemplace los valores entre `**< ... >**` con una dirección IP válida.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

No hay ningún nombre de servidor virtual equivalente en marcapasos. Para usar una cadena de conexión que apunta a un nombre de servidor de cadena y no usar la dirección IP, registrar la dirección del recurso IP y el nombre de servidor virtual que desee en DNS. Las configuraciones de recuperación ante desastres, registre el nombre del servidor virtual deseado y la dirección IP con los servidores DNS principal y el sitio de recuperación ante desastres.

## <a name="add-colocation-constraint"></a>Agregar restricción de colocación

Casi cada decisión en un clúster marcapasos, como elegir dónde se debe ejecutar un recurso, se realiza comparando las puntuaciones. Las puntuaciones se calculan por recurso y el Administrador de recursos de clúster elige el nodo con la máxima puntuación de un recurso concreto. (Si un nodo tiene una puntuación negativa para un recurso, el recurso no se puede ejecutar en ese nodo.) Se pueden manipular las decisiones del clúster con restricciones. Las restricciones tienen una puntuación. Si una restricción que tiene una puntuación menor que infinito, es sólo una recomendación. Una puntuación de infinito significa que es un requisito indispensable. Es deseable para asegurarse de que principal del grupo de disponibilidad y el virtual recurso de ip se ejecutan en el mismo host, por lo que se define una restricción de colocación con una puntuación de infinito. Para agregar la restricción de colocación, ejecute el siguiente comando en un nodo. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Agregar restricción de ordenación

La restricción de colocación tiene una restricción de ordenación implícita. Mueve el recurso IP virtual antes de que pase el recurso de grupo de disponibilidad. De forma predeterminada es la secuencia de eventos:

1. Problemas de los usuarios `pcs resource move` al grupo de disponibilidad principal del Nodo1 al Nodo2.
1. El recurso IP virtual se detiene en el nodo 1.
1. El recurso IP virtual se inicia en el nodo 2.

   >[!NOTE]
   >En este punto, la dirección IP temporalmente puntos al Nodo2 mientras Nodo2 sigue siendo una pre-conmutación por error secundario. 
   
1. El grupo de disponibilidad principal en el nodo 1 se degrada a la secundaria.
1. El grupo de disponibilidad secundario en Nodo2 se promueve a principal. 

Para evitar que la dirección IP temporalmente que apunta al nodo con la base de datos secundaria anterior la conmutación por error, agregue una restricción de ordenación. 

Para agregar una restricción de ordenación, ejecute el siguiente comando en un nodo:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Después de configurar el clúster y agregar el grupo de disponibilidad como un recurso de clúster, no puede usar Transact-SQL para conmutar los recursos del grupo de disponibilidad. Recursos de clúster de SQL Server en Linux no se acoplan estrechamente como con el sistema operativo tal como están en un clúster de conmutación por error de Windows Server (WSFC). Servicio SQL Server no es consciente de la presencia del clúster. Todas las orquestaciones se realiza a través de las herramientas de administración de clúster. En RHEL o Ubuntu usar `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Pasos siguientes

[Operar el grupo de disponibilidad de alta disponibilidad](sql-server-linux-availability-group-failover-ha.md)


