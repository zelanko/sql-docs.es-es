---
title: Dar de baja un servidor de destino desde un servidor maestro | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 660fbd83ba89ceb38ca240fe2c8c7d2d6d6b8dcd
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="defect-a-target-server-from-a-master-server"></a>Defect a Target Server from a Master Server
En este tema se describe cómo dar de baja un servidor de destino de un servidor maestro en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] u Objetos de administración de SQL Server (SMO). Ejecute este procedimiento en el servidor de destino.  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Seguridad](#Security)  
  
-   **Para dar de baja un servidor de destino, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SMO](#PowerShellProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor de destino.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, haga clic en **Dar de baja**.  
  
3.  Haga clic en **Sí** para confirmar que desea dar de baja este servidor de destino en un servidor maestro.  
  
## <a name="TsqlProcedure"></a>Usar Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
```  
sp_msx_defect ;  
```  
  
Para más información, consulte [sp_msx_defect (Transact-SQL)](http://msdn.microsoft.com/en-us/0dfd963a-3bc5-4b58-94f7-aec976da2883).  
  
## <a name="PowerShellProcedure"></a>Usar Objetos de administración de SQL Server (SMO)  
Utilice el método **MsxDefect**.  
  
## <a name="see-also"></a>Vea también  
[Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)  
[Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Dar de baja varios servidores de destino desde un servidor maestro](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)  
  

