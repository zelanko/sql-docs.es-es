---
title: Dar de baja un servidor de destino desde un servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 07433af48c259d0f2654f01b3a6bc3a43c808c0a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106255"
---
# <a name="defect-a-target-server-from-a-master-server"></a>Dar de baja un servidor de destino desde un servidor maestro
  En este tema se describe cómo dar de baja un servidor de destino de un servidor maestro en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] u Objetos de administración de SQL Server (SMO). Ejecute este procedimiento en el servidor de destino.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para dar de baja un servidor de destino, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor `sysadmin`.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor de destino.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, haga clic en **Dar de baja**.  
  
3.  Haga clic en **Sí** para confirmar que desea dar de baja este servidor de destino en un servidor maestro.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
```  
sp_msx_defect ;  
```  
  
 Para obtener más información, consulte [sp_msx_defect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-defect-transact-sql).  
  
##  <a name="PowerShellProcedure"></a> Usar objetos de administración de SQL Server (SMO)  
 Use `MsxDefect Method`.  
  
## <a name="see-also"></a>Vea también  
 [Crear un entorno multiservidor](create-a-multiserver-environment.md)   
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)   
 [Dar de baja varios servidores de destino desde un servidor maestro](defect-multiple-target-servers-from-a-master-server.md)  
  
  
