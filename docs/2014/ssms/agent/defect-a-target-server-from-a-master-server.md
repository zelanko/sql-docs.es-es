---
title: Dar de baja un servidor de destino desde un servidor maestro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
ms.assetid: a6da262b-7b38-4ce4-bfd6-6a557c6e8a84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f51e8f62a6be442c123c5a1309293e204caf08f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783217"
---
# <a name="defect-a-target-server-from-a-master-server"></a>Dar de baja un servidor de destino desde un servidor maestro
  En este tema se describe cómo dar de baja un servidor de destino de un servidor maestro en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]u Objetos de administración de SQL Server (SMO). Ejecute este procedimiento en el servidor de destino.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para dar de baja un servidor de destino, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor `sysadmin`.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  En el **Explorador de objetos**, expanda un servidor que esté configurado como servidor de destino.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**, seleccione **Administración de multiservidor**y, luego, haga clic en **Dar de baja**.  
  
3.  Haga clic en **Sí** para confirmar que desea dar de baja este servidor de destino en un servidor maestro.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-defect-a-target-server-from-a-master-server"></a>Para dar de baja un servidor de destino desde un servidor maestro  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
```sql
sp_msx_defect ;  
```  
  
 Para obtener más información, vea [sp_msx_defect &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-msx-defect-transact-sql).  
  
##  <a name="PowerShellProcedure"></a>Usar Objetos de administración de SQL Server (SMO)  
 Use `MsxDefect Method`.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un entorno multiservidor](create-a-multiserver-environment.md)   
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)   
 [Defect Multiple Target Servers from a Master Server](defect-multiple-target-servers-from-a-master-server.md)  
