---
title: Implementación de un clúster de Pacemaker para SQL Server en Linux
description: En este tutorial se muestra cómo implementar un clúster de Pacemaker para SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ee3b4aac2e1bcdcc37de17a569f080d3b9bc87cc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68077475"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implementación de un clúster de Pacemaker para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se documentan las tareas necesarias para implementar un clúster de Pacemaker de Linux para un grupo de disponibilidad Always On (AG) de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] o una instancia de clúster de conmutación por error (FCI). A diferencia de la pila ligada estrechamente de Windows Server/[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], la creación de clústeres de Pacemaker, así como la configuración de grupos de disponibilidad (AG) en Linux, se pueden realizar antes o después de la instalación de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. La integración y configuración de los recursos para la parte de Pacemaker de una implementación de AG o FCI se realiza una vez configurado el clúster.
> [!IMPORTANT]
> Un AG con un tipo de clúster de Ninguno *no* requiere un clúster de Pacemaker, ni se puede administrar mediante Pacemaker. 

> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad e instalar Pacemaker.
> * Preparar los nodos para Pacemaker (solo RHEL y Ubuntu).
> * Implementar un clúster de Pacemaker.
> * Instalar los paquetes de SQL Server HA y Agente SQL Server.
 
## <a name="prerequisite"></a>Requisito previo
[Instalar SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instale el complemento de alta disponibilidad
Use la siguiente sintaxis para instalar los paquetes que componen el complemento de alta disponibilidad (HA) para cada distribución de Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registre el servidor con la siguiente sintaxis. Se le pedirá un nombre de usuario y una contraseña válidos.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Enumere los grupos disponibles para el registro.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Ejecute el siguiente comando para asociar la alta disponibilidad de RHEL con la suscripción
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    donde *PoolId* es el identificador de grupo para la suscripción de alta disponibilidad del paso anterior.
    
4.  Habilite el repositorio para poder usar el complemento de alta disponibilidad.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instale Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instale el patrón de alta disponibilidad en YaST o hágalo como parte de la instalación principal del servidor. La instalación se puede realizar con una ISO/DVD como origen u obteniéndola en línea.
> [!NOTE]
> En SLES, el complemento de alta disponibilidad se inicializa cuando se crea el clúster.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparar los nodos para Pacemaker (solo RHEL y Ubuntu)
Pacemaker utiliza un usuario creado en la distribución denominada *hacluster*. El usuario se crea cuando se instala el complemento de alta disponibilidad en RHEL y Ubuntu.
1. En cada servidor que sirva como nodo del clúster de Pacemaker, cree la contraseña para un usuario que vaya a usar el clúster. El nombre que se usa en los ejemplos es *hacluster*, pero se puede usar cualquier nombre. El nombre y la contraseña deben ser los mismos en todos los nodos que participan en el clúster de Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. En cada nodo que va a formar parte del clúster de Pacemaker, habilite e inicie el servicio `pcsd` con los siguientes comandos (RHEL y Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   Después, ejecute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para asegurarse que `pcsd` se inicia.
3. Habilite el servicio Pacemaker en cada nodo posible del clúster de Pacemaker.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   En Ubuntu, verá un error:
   
   *Inicio predeterminado de Pacemaker no contiene niveles de ejecución, anulando.*
   
   Este error es un problema conocido. A pesar del error, la habilitación del servicio Pacemaker se realiza correctamente y este error se solucionará en algún momento en el futuro.
   
4. A continuación, cree e inicie el clúster de Pacemaker. Hay una diferencia entre RHEL y Ubuntu en este paso. En ambas distribuciones, la instalación de `pcs` configura un archivo de configuración predeterminado para el clúster de Pacemaker; en RHEL, al ejecutar este comando, se destruye cualquier configuración existente y se crea un nuevo clúster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Implementar un clúster de Pacemaker 
En esta sección se documenta cómo crear y configurar el clúster para cada distribución de Linux.

**RHEL**

1. Autorice los nodos
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   donde *NodeX* es el nombre del nodo.
2. Creación del clúster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   donde *PMClusterName* es el nombre asignado al clúster de Pacemaker y *nodeList* es la lista de nombres de los nodos separados por un espacio.

**Ubuntu**

La configuración de Ubuntu es similar a la de RHEL. Con todo, hay una diferencia importante: la instalación de los paquetes de Pacemaker crea una configuración base para el clúster y habilita e inicia `pcsd`. Si intenta configurar el clúster de Pacemaker siguiendo exactamente las instrucciones de RHEL, obtendrá un error. Para corregir este problema, siga los pasos que se indican a continuación: 
1. Quite la configuración predeterminada de Pacemaker de cada nodo.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga los pasos de la sección RHEL para crear el clúster de Pacemaker.

**SLES**

El proceso para crear un clúster de Pacemaker es completamente diferente en SLES que en RHEL y Ubuntu. En los pasos siguientes se documenta cómo crear un clúster con SLES.
1. Inicie el proceso de configuración del clúster mediante la ejecución de 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   en uno de los nodos. Es posible que se le pida que NTP no esté configurado y que no se encuentre ningún dispositivo guardián. De esta manera, podrá poner en marcha el proceso. El guardián está relacionado con STONITH si usa barreras integradas de SLES que se basan en el almacenamiento. NTP y el guardián se pueden configurar más adelante.
   
2. Se le pedirá que configure Corosync. Se le pedirá la dirección de red a la que se va a enlazar, así como la dirección y el puerto de multidifusión. La dirección de red es la subred que está usando; por ejemplo, 192.191.190.0. Puede aceptar los valores predeterminados en cada solicitud o cambiarlos si es necesario.
   
3. A continuación, se le preguntará si desea configurar SBD, que es la barrera basada en disco. Esta configuración se puede realizar más adelante si lo desea. Si SBD no está configurado, a diferencia de RHEL y Ubuntu, `stonith-enabled` se establecerá de forma predeterminada en false.
   
4. Por último, se le preguntará si desea configurar una dirección IP para la administración. Esta dirección IP es opcional, pero funciona de forma similar a la dirección IP de un clúster de conmutación por error de Windows Server (WSFC) ya que crea una dirección IP en el clúster que se va a usar para conectarse a la misma a través de HA Web Konsole (HAWK). Esta configuración también es opcional.
   
5. Para asegurarse de que el clúster está en funcionamiento 
   ```bash
   sudo crm status
   ```
   
6. Cambie la contraseña de *hacluster* con 
   ```bash
   sudo passwd hacluster
   ```
   
7. Si ha configurado una dirección IP para la administración, puede probarla en un explorador, que también prueba el cambio de contraseña de *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. En otro servidor SLES que será un nodo del clúster, ejecute 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Cuando se le pida, escriba el nombre o la dirección IP del servidor que se ha configurado como primer nodo del clúster en los pasos anteriores. El servidor se agrega como un nodo al clúster existente.
   
10. Compruebe que el nodo se ha agregado; para ello, envíe 
   ```bash
   sudo crm status
   ```
   
11. Cambie la contraseña de *hacluster* con 
   ```bash
   sudo passwd hacluster
   ```
   
12. Repita los pasos del 8 al 11 para el resto de los servidores que se van a agregar al clúster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Instalación de los paquetes de SQL Server HA y Agente SQL Server
Use los siguientes comandos para instalar el paquete de SQL Server HA y el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], si aún no están instalados. La instalación del paquete HA después de la instalación de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requiere reiniciar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para que pueda utilizarse. En estas instrucciones se da por supuesto que los repositorios de los paquetes de Microsoft ya se han configurado, ya que debe instalarse [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en este momento.
> [!NOTE]
> - Si no va a usar el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para el trasvase de registros o cualquier otro uso, no es necesario instalarlo, por lo que se puede omitir el paquete *mssql-server-agent*.
> - Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, la búsqueda de texto completo de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*) no se requieren para la alta disponibilidad, ya sea para una FCI o un AG.

**RHEL**

```bash
sudo yum install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**Ubuntu**

```bash
sudo apt-get install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

**SLES**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a implementar un clúster de Pacemaker para SQL Server en Linux. Ha aprendido a:
> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad e instalar Pacemaker.
> * Preparar los nodos para Pacemaker (solo RHEL y Ubuntu).
> * Implementar un clúster de Pacemaker.
> * Instalar los paquetes de SQL Server HA y Agente SQL Server.

Para crear y configurar un grupo de disponibilidad para SQL Server en Linux, consulte:

> [!div class="nextstepaction"]
> [Creación y configuración de un grupo de disponibilidad para SQL Server en Linux](sql-server-linux-create-availability-group.md).

