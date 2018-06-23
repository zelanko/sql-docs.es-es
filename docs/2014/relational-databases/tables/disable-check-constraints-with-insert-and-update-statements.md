---
title: Deshabilitar restricciones CHECK con instrucciones INSERT y UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 16baf05c5beba900d853da3e655b7742d18a7ac4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103760"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>Deshabilitar restricciones CHECK con instrucciones INSERT y UPDATE
  Puede deshabilitar una restricción CHECK para las transacciones INSERT y UPDATE de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Después de deshabilitar las restricciones CHECK, las posteriores inserciones o actualizaciones de la columna no se validan con las condiciones de la restricción. Use esta opción si sabe que los nuevos datos infringirán la restricción existente o si la restricción solo se aplica a los datos que ya están en la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para deshabilitar una restricción CHECK para las instrucciones INSERT y UPDATE con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Para deshabilitar una restricción CHECK para las instrucciones INSERT y UPDATE  
  
1.  En el **Explorador de objetos**, expanda la tabla que contiene la restricción y, a continuación, expanda la carpeta **Restricciones** .  
  
2.  Haga clic con el botón derecho en la restricción y seleccione **Modificar**.  
  
3.  En la cuadrícula situada debajo de **Diseñador de tablas**, haga clic en **Exigir para comandos INSERTs y UPDATEs** y seleccione **No** en el menú desplegable.  
  
4.  Haga clic en **Cerrar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Para deshabilitar una restricción CHECK para las instrucciones INSERT y UPDATE  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  
