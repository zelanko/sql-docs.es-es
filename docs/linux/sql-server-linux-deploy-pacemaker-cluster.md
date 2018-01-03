---
title: "Implementar un clúster marcapasos para SQL Server en Linux | Documentos de Microsoft"
description: "Este tutorial muestra cómo implementar un clúster marcapasos para SQL Server en Linux."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 4a014c0b7eedb96375f027674d9eb2374f38c85e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implementar un clúster marcapasos para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tutorial documentan las tareas necesarias para implementar un clúster de Linux marcapasos para un [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] grupo de disponibilidad AlwaysOn (AG) o instancia de clúster de conmutación por error (FCI). A diferencia del servidor de Windows estrechamente acoplado /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pila, la creación del clúster marcapasos, así como configuración de grupo (AG) de disponibilidad en Linux puede hacerse antes o después de la instalación de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. La integración y la configuración de los recursos de la parte marcapasos de una implementación de AG o FCI se realiza después de que el clúster está configurado.
> [!IMPORTANT]
> Un AG con un tipo de clúster de None *no* requiere un clúster marcapasos, ni puede administrarse mediante marcapasos. 

> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad y marcapasos.
> * Preparar los nodos para marcapasos (RHEL y Ubuntu solo).
> * Cree el clúster marcapasos.
> * Instalar los paquetes de HA de SQL Server y Agente SQL Server.
 
## <a name="prerequisite"></a>Requisito previo
[Instalar SQL Server de 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instalar el complemento de alta disponibilidad
Use la sintaxis siguiente para instalar los paquetes que componen el complemento de alta disponibilidad (HA) para cada distribución de Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registrar el servidor utilizando la sintaxis siguiente. Se le pida un nombre de usuario válido y una contraseña.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Lista de los grupos disponibles para el registro.
    
    ```bash
    sudo subscription-manager list --available
3.  Run the following command to associate RHEL high availability with the subscription
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    donde *PoolId* es el identificador de grupo para la suscripción de alta disponibilidad en el paso anterior.
    
4.  Habilitar el repositorio para poder usar el complemento de alta disponibilidad.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instalar a marcapasos.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instale el patrón de alta disponibilidad en YaST o hacerlo como parte de la instalación del servidor principal. La instalación puede hacerse con un DVD/ISO como origen o si lo busca en línea.
> [!NOTE]
> En SLES, el complemento de alta disponibilidad se inicializa cuando se crea el clúster.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparar los nodos para marcapasos (RHEL y Ubuntu solo)
Marcapasos propio usa un usuario creado en la distribución denominada *hacluster*. El usuario se crea cuando se instala el complemento de alta disponibilidad en RHEL y Ubuntu.
1. En cada servidor que actúa como un nodo del clúster marcapasos, cree la contraseña de un usuario que va a usar el clúster. El nombre utilizado en los ejemplos es *hacluster*, pero se puede utilizar cualquier nombre. El nombre y la contraseña deben ser el mismo en todos los nodos que participan en el clúster marcapasos.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. En cada nodo que va a formar parte del clúster marcapasos, habilitar e iniciar el `pcsd` servicio con los siguientes comandos (RHEL y Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   A continuación, ejecute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para asegurarse de que `pcsd` se inicia.
3. Habilitar el servicio marcapasos en cada nodo del clúster marcapasos posibles.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   En Ubuntu, verá un error:
   
   *marcapasos inicio predeterminado no contiene niveles de ejecución, anulando.*
   
   Este error es un problema conocido. A pesar del error, habilitar el servicio marcapasos es correcta, y este error se corregirá en algún momento en el futuro.
   
4. A continuación, cree e inicie el clúster marcapasos. Hay una diferencia entre RHEL y Ubuntu en este paso. Mientras que en las distribuciones, instalar `pcs` configura un archivo de configuración predeterminado para el clúster marcapasos, en RHEL, al ejecutar este comando destruye cualquier configuración existente y crea un nuevo clúster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Crear el clúster marcapasos 
Esta sección describe cómo crear y configurar el clúster para cada distribución de Linux.

**RHEL**

1. Autorizar a los nodos
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 … NodeN> -u hacluster
   ```
   
   donde *NodeX* es el nombre del nodo.
2. Crear el clúster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   donde *PMClusterName* es el nombre asignado al clúster marcapasos y *Nodelist* es la lista de nombres de los nodos separados por un espacio.

**Ubuntu**

Configuración Ubuntu es similar a RHEL. Sin embargo, hay una diferencia importante: instalar los paquetes de marcapasos, crea una configuración básica para el clúster y habilita e inicia `pcsd`. Si intenta configurar el clúster marcapasos siguiendo las instrucciones de RHEL exactamente, obtendrá un error. Para solucionar este problema, realice los pasos siguientes: 
1. Quitar la configuración de marcapasos predeterminado de cada nodo.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga los pasos descritos en la sección RHEL para crear el clúster marcapasos.

**SLES GRANDE**

El proceso para crear un clúster marcapasos es completamente diferente en SLES en RHEL y Ubuntu. Cómo crear un clúster con SLES de documentos de los pasos siguientes.
1. Inicie el proceso de configuración de clúster mediante la ejecución 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   en uno de los nodos. Se le pedirá que NTP no está configurado y que no hay ningún dispositivo de guardián se encuentra. Esto está bien para poner cosas en ejecución. Guardián está relacionado con STONITH si usas barrera integrada del SLES que esté basado en almacenamiento. NTP y guardián se pueden configurar más adelante.
   
2. Deberá configurar Corosync. Se le pedirán la dirección de red enlazar, así como la dirección de multidifusión y el puerto. La dirección de red es la subred que esté utilizando; Por ejemplo, 192.191.190.0. Puede aceptar los valores predeterminados en cada símbolo del sistema, o si es necesario cambiar.
   
3. A continuación, se le preguntará si desea configurar el mismo día Laborable, que es la barrera basadas en disco. Esta configuración puede realizarse más adelante si lo desea. Si no es el mismo día Laborable se ha configurado, a diferencia de en RHEL y Ubuntu, `stonith-enabled` de forma predeterminada se establecerá en false.
   
4. Por último, se le preguntará si desea configurar una dirección IP para la administración. Esta dirección IP es opcional, pero las funciones similar a la dirección IP de un clúster de conmutación por error de Windows Server (WSFC) en el sentido de que crea una dirección IP del clúster que se usará para conectarse a ella a través de alta disponibilidad Web Konsole (HAWK). Esta configuración, también es opcional.
   
5. Asegúrese de que el clúster está en funcionamiento mediante la emisión 
   ```bash
   sudo crm status
   ```
   
6. Cambiar el *hacluster* contraseña con 
   ```bash
   sudo passwd hacluster
   ```
   
7. Si ha configurado una dirección IP para la administración, puede probarlo en un explorador, que también comprueba el cambio de contraseña para *hacluster*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. En otro servidor SLES que será un nodo del clúster, ejecute 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Cuando se le solicite, escriba el nombre o dirección IP del servidor que se haya configurado como el primer nodo del clúster en los pasos anteriores. El servidor se agrega como un nodo al clúster existente.
   
10. Compruebe que el nodo se agrega mediante la emisión 
   ```bash
   sudo crm status
   ```
   
11. Cambiar el *hacluster* contraseña con 
   ```bash
   sudo passwd hacluster
   ```
   
12. Repita los pasos del 8 al 11 para todos los demás servidores va a agregar al clúster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Instalar los paquetes de HA de SQL Server y Agente SQL Server
Utilice los siguientes comandos para instalar el paquete HA de SQL Server y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent, si no están ya instalados. Instalar el paquete de alta disponibilidad después de instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requiere un reinicio de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para que se pueda usar. Estas instrucciones se supone que los repositorios de los paquetes de Microsoft se haya configurado, ya que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] debe estar instalado en este momento.
> [!NOTE]
> - Si no va a usar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de trasvase de registros o cualquier otro uso, no tiene que instalarse, por lo que empaqueta *agente de server mssql* puede omitirse.
> - Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Full-Text Search (*mssql-server-FT*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql servidor es*), no son es necesario para lograr alta disponibilidad, para ver si una FCI o un AG.

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

**SLES GRANDE**

```bash
sudo zypper install mssql-server-ha mssql-server-agent
sudo systemctl restart mssql-server
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprendió a implementar un clúster marcapasos para SQL Server en Linux. También habrá aprendido cómo para:
> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad y marcapasos.
> * Preparar los nodos para marcapasos (RHEL y Ubuntu solo).
> * Cree el clúster marcapasos.
> * Instalar los paquetes de HA de SQL Server y Agente SQL Server.

Para crear y configurar un grupo de disponibilidad para SQL Server en Linux, consulte:

> [!div class="nextstepaction"]
> [Crear y configurar un grupo de disponibilidad para SQL Server en Linux](sql-server-linux-create-availability-group.md).

