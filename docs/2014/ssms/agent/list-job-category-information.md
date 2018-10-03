---
title: Mostrar información de categorías de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 69abea91334f53993fec78e2204cee1573afd780
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181585"
---
# <a name="list-job-category-information"></a>Mostrar información de categorías de trabajo
  Cómo mostrar información de categoría de trabajo en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)] u objetos de administración de SQL Server.  

  
##  <a name="Security"></a> Seguridad  
 Para obtener información detallada, vea [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  

  
##  <a name="TSQL"></a> Usar Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>Para mostrar información de categorías de trabajo  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 Para obtener más información, consulte [sp_help_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql).  
  
  
##  <a name="SMO"></a> Usar objetos de administración de SQL Server  
 **Para mostrar información de categorías de trabajo**  
  
 Use la `JobCategory` clase mediante el uso de un lenguaje de programación que desee, como Visual Basic, Visual C# o PowerShell... Para obtener más información, consulte [SQL Server Management Objects &#40;SMO&#41; Programming Guide](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md).  
  
  
  
