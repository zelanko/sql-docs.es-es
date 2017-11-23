---
title: "Funcionan de la instancia de clúster de conmutación por error: SQL Server en Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 8af38fffc17a1b5198dbc85eff5c66a7c2acbb1f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Funcionan de la instancia de clúster de conmutación por error: SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este artículo explica cómo utilizar una instancia de clúster de conmutación por error (FCI) de SQL Server en Linux. Si no ha creado una FCI de SQL Server en Linux, consulte [instancia de clúster de conmutación por error de configuración: SQL Server en Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Conmutación por error

Conmutación por error de fci es similar a un clúster de conmutación por error de Windows Server (WSFC). Si el nodo de clúster que aloja la FCI experimenta a algún tipo de error, la FCI debe conmutar por error automáticamente a otro nodo. A diferencia de un WSFC, no hay ninguna manera de establecer los propietarios preferidos, modo marcapasos elija el nodo que será el nuevo host para la FCI.

Hay ocasiones puede que desee por error manualmente de la FCI a otro nodo. El proceso no es igual que con las fci en un WSFC. En un WSFC, conmutar los recursos en el nivel de rol. En marcapasos, elija un recurso para mover y, suponiendo que todas las restricciones son correctas, todo lo demás se moverá también. 

La forma de conmutación por error depende de la distribución de Linux. Siga las instrucciones para su distribución de linux.

- [RHEL o Ubuntu](#rhelFailover)
- [SLES GRANDE](#slesFailover)

## <a name = "#rhelFailover"></a>Conmutación por error manual (RHEL o Ubuntu)

Para llevar a cabo una conmutación por error manual, onn Red Hat Enterprise Linux (RHEL) o servidores Ubuntu, ejecute los siguientes pasos.
1.  Emita el comando siguiente: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > es el nombre de recurso marcapasos para la FCI de SQL Server.

   \<NewHostNode > es el nombre del nodo de clúster que desea hospedar la FCI. 

   No se obtendrá ninguna confirmación.

2.  Durante una conmutación por error manual, marcapasos crea una restricción de ubicación en el recurso que se ha elegido para mover manualmente. Para ver esta restricción, ejecute `sudo pcs constraint`.

3.  Una vez completada la conmutación por error, quite la restricción mediante la emisión de `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName > es el nombre de recurso marcapasos para la FCI. 

## <a name = "#slesFailover"></a>Conmutación por error manual (SLES)


En Suse Linux Enterprise Server (SLES), use el `migrate` de comandos para la conmutación por error manualmente una FCI de SQL Server. Por ejemplo:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > es el nombre de recurso para la instancia de clúster de conmutación por error. 

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
