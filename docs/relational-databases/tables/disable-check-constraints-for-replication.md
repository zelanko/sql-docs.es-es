---
title: "Deshabilitar restricciones CHECK para la replicación | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2f8ff552993defe940576ea5cf0a35943a417b1b
ms.lasthandoff: 04/11/2017

---
# <a name="disable-check-constraints-for-replication"></a>Deshabilitar restricciones CHECK para la replicación
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede deshabilitar las restricciones CHECK en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. También puede deshabilitar explícitamente las restricciones CHECK para la replicación, lo que puede resultar útil si se publican datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si una tabla se publica mediante replicación, se deshabilitan automáticamente las restricciones CHECK para las operaciones realizadas por los agentes de replicación. Cuando un agente de replicación realiza una inserción, actualización o eliminación en un suscriptor, no se comprueba la restricción. En cambio, sí se comprueba cuando lo hace un usuario. La restricción se deshabilitará para el agente de replicación porque ya se comprobó en el publicador cuando se insertaron, actualizaron o eliminaron los datos originalmente. Para obtener más información, vea [Especificar opciones de esquema](../../relational-databases/replication/publish/specify-schema-options.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>Para deshabilitar una restricción CHECK para la replicación  
  
1.  En el **Explorador de objetos**, expanda la tabla con la restricción CHECK que desee modificar y, a continuación, expanda la carpeta **Restricciones** .  
  
2.  Haga clic con el botón derecho en la restricción CHECK que quiera cambiar y, después, haga clic en **Modificar**.  
  
3.  En el cuadro de diálogo **Restricciones CHECK** , bajo **Diseñador de tablas**, seleccione el valor **No** para **Exigir para replicación**.  
  
4.  Haga clic en **Cerrar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>Para deshabilitar una restricción CHECK para la replicación  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se crea una tabla con una columna IDENTITY y una restricción CHECK. Después, se quita la restricción y se vuelve a crear especificando la cláusula NOT FOR REPLICATION.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.doc_exd (column_a int IDENTITY (1,1)   
    CONSTRAINT exd_check CHECK (column_a > 1))   
  
    ALTER TABLE dbo.doc_exd   
    DROP CONSTRAINT exd_check;   
    GO  
    ALTER TABLE dbo.doc_exd    
    ADD CONSTRAINT exd_check CHECK NOT FOR REPLICATION (column_a > 1);  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>   
## <a name="see-also"></a>Vea también  
 [Especificar opciones de esquema](../../relational-databases/replication/publish/specify-schema-options.md)  
  
  
