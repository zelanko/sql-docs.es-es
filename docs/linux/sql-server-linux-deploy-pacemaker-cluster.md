---
title: Implementar un clúster de Pacemaker para SQL Server en Linux
description: Este tutorial muestra cómo implementar un clúster de Pacemaker para SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/11/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ee3b4aac2e1bcdcc37de17a569f080d3b9bc87cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077475"
---
# <a name="deploy-a-pacemaker-cluster-for-sql-server-on-linux"></a>Implementar un clúster de Pacemaker para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial documentan las tareas necesarias para implementar un clúster de Linux Pacemaker para un [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] siempre en el grupo de disponibilidad (AG) o instancia de clúster de conmutación por error (FCI). A diferencia de Windows Server estrechamente acoplado / [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pila, la creación del clúster de Pacemaker, así como configuración de grupo (AG) de disponibilidad en Linux puede hacerse antes o después de la instalación de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. La integración y la configuración de recursos para la parte de Pacemaker de una implementación de grupo de disponibilidad o FCI se realiza una vez configurado el clúster.
> [!IMPORTANT]
> Un grupo de disponibilidad con un tipo de clúster ninguno *no* requiere un clúster de Pacemaker, ni puede administrarse mediante Pacemaker. 

> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad y Pacemaker.
> * Preparar los nodos para Pacemaker (solo Ubuntu y RHEL).
> * Cree el clúster de Pacemaker.
> * Instale los paquetes de SQL Server alta disponibilidad y del Agente SQL Server.
 
## <a name="prerequisite"></a>Requisito previo
[Instalar SQL Server 2017](sql-server-linux-setup.md).

## <a name="install-the-high-availability-add-on"></a>Instalar el complemento de alta disponibilidad
Use la sintaxis siguiente para instalar los paquetes que componen el complemento de alta disponibilidad (HA) para cada distribución de Linux. 

**Red Hat Enterprise Linux (RHEL)**
1.  Registre el servidor utilizando la sintaxis siguiente. Se solicitará un nombre de usuario válido y una contraseña.
    
    ```bash
    sudo subscription-manager register
    ```
    
2.  Lista de los grupos disponibles para el registro.
    
    ```bash
    sudo subscription-manager list --available
    ```

3.  Ejecute el siguiente comando para asociar la alta disponibilidad RHEL a la suscripción
    
    ```bash
    sudo subscription-manager attach --pool=<PoolID>
    ```
    
    donde *PoolId* es el identificador de grupo para la suscripción de alta disponibilidad en el paso anterior.
    
4.  Habilitación del repositorio poder usar el complemento de alta disponibilidad.
    
    ```bash
    sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
    ```
    
5.  Instale a Pacemaker.
    
    ```bash
    sudo yum install pacemaker pcs fence-agents-all resource-agents
    ```

**Ubuntu**

```bash
sudo apt-get install pacemaker pcs fence-agents resource-agents
```

**SUSE Linux Enterprise Server (SLES)**

Instalar el patrón de alta disponibilidad en YaST o hacerlo como parte de la instalación del servidor principal. La instalación puede realizarse con un DVD/ISO como origen o si lo busca en línea.
> [!NOTE]
> En SLES, el complemento de alta disponibilidad se inicializa cuando se crea el clúster.

## <a name="prepare-the-nodes-for-pacemaker-rhel-and-ubuntu-only"></a>Preparar los nodos para Pacemaker (solo Ubuntu y RHEL)
Propio pacemaker usa un usuario creado en la distribución denominada *hacluster coincida*. El usuario se crea cuando se instala el complemento de alta disponibilidad en Ubuntu y RHEL.
1. En cada servidor que actuará como un nodo del clúster de Pacemaker, cree la contraseña de un usuario que se usará el clúster. El nombre utilizado en los ejemplos es *hacluster coincida*, pero se puede utilizar cualquier nombre. El nombre y la contraseña deben ser la misma en todos los nodos que participan en el clúster de Pacemaker.
   
    ```bash
    sudo passwd hacluster
    ```
    
2. En cada nodo que va a formar parte del clúster de Pacemaker, habilitar e iniciar el `pcsd` servicio con los siguientes comandos (RHEL y Ubuntu):

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   ```
   
   A continuación, ejecute
   
   ```bash
   sudo systemctl status pcsd
   ```
   
   para asegurarse de que `pcsd` se inicia.
3. Habilite el servicio Pacemaker en cada nodo del clúster de Pacemaker posible.
   
   ```bash
   sudo systemctl start pacemaker
   ```

   En Ubuntu, verá un error:
   
   *pacemaker inicio predeterminado contiene no hay niveles de ejecución, anulando.*
   
   Este error es un problema conocido. A pesar del error, habilitar el servicio Pacemaker es correcta, y este error se corregirá en algún momento en el futuro.
   
4. A continuación, cree e inicie el clúster de Pacemaker. Hay una diferencia entre Ubuntu y RHEL en este paso. Mientras se encuentra en las distribuciones de ambos, instalar `pcs` configura un archivo de configuración predeterminado para el clúster de Pacemaker en RHEL, al ejecutar este comando destruye cualquier configuración existente y crea un nuevo clúster.

<a id="create"></a>
## <a name="create-the-pacemaker-cluster"></a>Crear el clúster de Pacemaker 
Esta sección describe cómo crear y configurar el clúster para cada distribución de Linux.

**RHEL**

1. Autorizar a los nodos
   
   ```bash
   sudo pcs cluster auth <Node1 Node2 ... NodeN> -u hacluster
   ```
   
   donde *NodeX* es el nombre del nodo.
2. Crear el clúster
   
   ```bash
   sudo pcs cluster setup --name <PMClusterName Nodelist> --start --all --enable
   ```
   
   donde *PMClusterName* es el nombre asignado al clúster de Pacemaker y *Nodelist* es la lista de nombres de los nodos separados por un espacio.

**Ubuntu**

Configuración de Ubuntu es similar a RHEL. Sin embargo, hay una diferencia importante: instalar los paquetes de Pacemaker crea una configuración básica para el clúster y habilita y se inicia `pcsd`. Si intenta configurar el clúster de Pacemaker siguiendo las instrucciones de RHEL exactamente, obtendrá un error. Para corregir este problema, realice los pasos siguientes: 
1. Quitar la configuración de Pacemaker predeterminada de cada nodo.
   
   ```bash
   sudo pcs cluster destroy
   ```
   
2. Siga los pasos descritos en la sección RHEL para crear el clúster de Pacemaker.

**SLES**

El proceso de creación de un clúster de Pacemaker es completamente diferente en SLES en Ubuntu y RHEL. Los pasos siguientes describen cómo crear un clúster con SLES.
1. Inicie el proceso de configuración de clúster mediante la ejecución 
   ```bash
   sudo ha-cluster-init
   ``` 
   
   en uno de los nodos. Se le pedirá que NTP no está configurado y que no se encuentra ningún dispositivo guardián. Eso está bien para las cosas entre en funcionamiento. Guardián está relacionado con STONITH si usas barrera integrada de SLES que se basa en el almacenamiento. NTP y guardián se pueden configurar más adelante.
   
2. Le pedirá que configure Corosync. Se le pedirán la dirección de red que desea enlazar, así como la dirección de multidifusión y puerto. La dirección de red es la subred que está usando; Por ejemplo, 192.191.190.0. Puede aceptar los valores predeterminados en cada símbolo del sistema, o si es necesario cambiar.
   
3. A continuación, le pregunta si desea configurar SBD, que es la barrera basadas en disco. Esta configuración se puede realizar más adelante si lo desea. Si SBD no está configurado, a diferencia de en RHEL y Ubuntu, `stonith-enabled` de forma predeterminada se establecerá en false.
   
4. Por último, le pregunta si desea configurar una dirección IP para la administración. Esta dirección IP es opcional, pero las funciones similar a la dirección IP para un clúster de conmutación por error de Windows Server (WSFC) en el sentido de que crea una dirección IP del clúster que se usará para conectarse a ella a través de alta disponibilidad Web Konsole (HAWK). Esta configuración, también es opcional.
   
5. Asegúrese de que el clúster está en marcha mediante la emisión 
   ```bash
   sudo crm status
   ```
   
6. Cambiar el *hacluster coincida* contraseña con 
   ```bash
   sudo passwd hacluster
   ```
   
7. Si ha configurado una dirección IP para la administración, puede probarlo en un explorador, que también comprueba el cambio de contraseña para *hacluster coincida*.
   ![](./media/sql-server-linux-deploy-pacemaker-cluster/image2.png)
   
8. En otro servidor SLES que será un nodo del clúster, ejecute 
   ```bash
   sudo ha-cluster-join
   ```
   
9. Cuando se le solicite, escriba el nombre o dirección IP del servidor que se ha configurado como el primer nodo del clúster en los pasos anteriores. El servidor se agrega como un nodo al clúster existente.
   
10. Comprobar que el nodo se ha agregado mediante la emisión 
   ```bash
   sudo crm status
   ```
   
11. Cambiar el *hacluster coincida* contraseña con 
   ```bash
   sudo passwd hacluster
   ```
   
12. Repita los pasos del 8 al 11 para todos los demás servidores a agregarse al clúster.

## <a name="install-the-sql-server-ha-and-sql-server-agent-packages"></a>Instalar los paquetes de SQL Server alta disponibilidad y del Agente SQL Server
Use los siguientes comandos para instalar el paquete de SQL Server alta disponibilidad y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Agent, si no están ya instalados. Instalar el paquete de alta disponibilidad después de instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requiere un reinicio de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para que pueda usarse. Estas instrucciones se supone que los repositorios para los paquetes de Microsoft ya se han configurado, ya que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] debe estar instalado en este momento.
> [!NOTE]
> - Si no va a usar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente para el trasvase de registros o cualquier otro uso, no tiene que instalar, por lo que empaquetar *mssql-server-agent* puede omitirse.
> - Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Full-Text Search (*mssql-server-fts*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-es*), no son se requiere para alta disponibilidad, ya sea por una FCI o un grupo de disponibilidad.

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

En este tutorial, ha aprendido cómo implementar un clúster de Pacemaker para SQL Server en Linux. Ha aprendido a:
> [!div class="checklist"]
> * Instalar el complemento de alta disponibilidad y Pacemaker.
> * Preparar los nodos para Pacemaker (solo Ubuntu y RHEL).
> * Cree el clúster de Pacemaker.
> * Instale los paquetes de SQL Server alta disponibilidad y del Agente SQL Server.

Para crear y configurar un grupo de disponibilidad para SQL Server en Linux, consulte:

> [!div class="nextstepaction"]
> [Crear y configurar un grupo de disponibilidad para SQL Server en Linux](sql-server-linux-create-availability-group.md).

