---
title: 'Operar la instancia de clúster de conmutación por error: SQL Server en Linux'
description: En este artículo se explica cómo trabajar con una instancia de clúster de conmutación por error (FCI) de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: cc0059f8e8dc43b2c65e432d7cdd56272218d36c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833150"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Operar la instancia de clúster de conmutación por error: SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo trabajar con una instancia de clúster de conmutación por error (FCI) de SQL Server en Linux. Si no ha creado una FCI de SQL Server en Linux, consulte [instancia de clúster de conmutación por error de configuración: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Conmutación por error

Conmutación por error para fci es similar a un clúster de conmutación por error de Windows Server (WSFC). Si el nodo de clúster que hospeda la FCI experimenta a algún tipo de error, la FCI debe conmutar por error automáticamente a otro nodo. A diferencia de un clúster de WSFC, no hay ninguna manera de establecer los propietarios preferidos, por lo que Pacemaker selecciona el nodo que será el nuevo host para la FCI.

Veces que desea manualmente producirá un error en la FCI a otro nodo. El proceso no es igual que con las fci en un WSFC. En un clúster de WSFC, conmuta por error recursos en el nivel de rol. En Pacemaker, elija un recurso para mover y, suponiendo que todas las restricciones son correctas, todo lo demás se moverá también. 

La forma de conmutación por error depende de la distribución de Linux. Siga las instrucciones para la distribución de linux.

- [RHEL o Ubuntu](#-manual-failover-rhel-or-ubuntu)
- [SLES](#-manual-failover-sles)

## <a name = "#-manual-failover-rhel-or-ubuntu"></a> Conmutación por error manual (RHEL o Ubuntu)

Para llevar a cabo una conmutación por error manual, onn Red Hat Enterprise Linux (RHEL) o los servidores Ubuntu que ejecutan los siguientes pasos.
1.  Emita el comando siguiente: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > es el nombre de recurso de Pacemaker para la FCI de SQL Server.

   \<NewHostNode > es el nombre del nodo de clúster que desea hospedar la FCI. 

   No obtendrá ninguna confirmación.

2.  Durante una conmutación por error manual, Pacemaker crea una restricción de ubicación en el recurso que se ha elegido para mover manualmente. Para ver esta restricción, ejecute `sudo pcs constraint`.

3.  Una vez completada la conmutación por error, quite la restricción mediante la emisión de `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName > es el nombre de recurso de Pacemaker para la FCI. 

## <a name = "#-manual-failover-sles"></a> Conmutación por error manual (SLES)


En Suse Linux Enterprise Server (SLES), use el `migrate` comando para conmutación por error manual de una FCI de SQL Server. Por ejemplo:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > es el nombre de recursos para la instancia de clúster de conmutación por error. 

\<NewHostNode > es el nombre del nuevo host de destino. 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>Pasos siguientes

- [Configurar la instancia de clúster de conmutación por error: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
