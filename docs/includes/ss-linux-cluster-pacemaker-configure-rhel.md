---
ms.openlocfilehash: 6cf3dd279f33ea0c157743d4b4c11248267a0a62
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215626"
---
3. En todos los nodos de clúster, abra los puertos de firewall de Pacemaker. Para abrir estos puertos con `firewalld`, ejecute el comando siguiente:

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > Si el firewall no tiene una configuración de alta disponibilidad integrada, abra los puertos siguientes para Pacemaker.
   >
   > * TCP: puertos 2224, 3121, 21064
   > * UDP: puerto 5405

1. Instale paquetes de Pacemaker en todos los nodos.

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. Establezca la contraseña para el usuario predeterminado que se crea al instalar paquetes de Pacemaker y Corosync. Use la misma contraseña en todos los nodos. 

   ```bash
   sudo passwd hacluster
   ```

3. Para permitir que los nodos vuelvan a unirse al clúster después del reinicio, habilite e inicie el servicio `pcsd` y Pacemaker. Ejecute el siguiente comando en todos los nodos.

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. Cree el clúster. Para crear el clúster, ejecute el comando siguiente:

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Si ya ha configurado un clúster en los mismos nodos, necesita usar la opción `--force` al ejecutar `pcs cluster setup`. Esta opción es equivalente a ejecutar `pcs cluster destroy`. Para volver a habilitar Pacemaker, ejecute `sudo systemctl enable pacemaker`.

5. Instale el agente de recursos de SQL Server para SQL Server. Ejecute los siguientes comandos en todos los nodos. 

   ```bash
   sudo yum install mssql-server-ha
   ```
