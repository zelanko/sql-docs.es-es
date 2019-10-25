---
title: Mostrar información de categorías de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dae8f1d98fb1758e9a9802883def1574bda68a78
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798210"
---
# <a name="list-job-category-information"></a>Mostrar información de categorías de trabajo
  Cómo Mostrar información de categorías de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] o Objetos de administración de SQL Server.  

  
##  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  

  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>Para mostrar información de categorías de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 Para obtener más información, [vea &#40;SP_HELP_CATEGORY Transact-&#41;SQL](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql).  
  
  
##  <a name="SMO"></a>Usar Objetos de administración de SQL Server  
 **Para mostrar información de categorías de trabajo**  
  
 Utilice la clase `JobCategory` mediante un lenguaje de programación que elija, como Visual Basic, Visual C# o PowerShell. Para obtener más información, [vea &#40;objetos de administración de SQL Server&#41; guía de programación de SMO](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md).  
