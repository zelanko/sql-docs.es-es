---
title: Deshabilitar restricciones CHECK para la replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: af98fc70-24dd-4bd3-a0a3-f701dfa67b2c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 557136026e518d54d81bda44b9694f9fe86e7c9d
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580659"
---
# <a name="disable-check-constraints-for-replication"></a>Deshabilitar restricciones CHECK para la replicación
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede deshabilitar las restricciones CHECK en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. También puede deshabilitar explícitamente las restricciones CHECK para la replicación, lo que puede resultar útil si se publican datos de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si una tabla se publica mediante replicación, se deshabilitan automáticamente las restricciones CHECK para las operaciones realizadas por los agentes de replicación. Cuando un agente de replicación realiza una inserción, actualización o eliminación en un suscriptor, no se comprueba la restricción. En cambio, sí se comprueba cuando lo hace un usuario. La restricción se deshabilitará para el agente de replicación porque ya se comprobó en el publicador cuando se insertaron, actualizaron o eliminaron los datos originalmente. Para obtener más información, vea [Especificar opciones de esquema](../../relational-databases/replication/publish/specify-schema-options.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-replication"></a>Para deshabilitar una restricción CHECK para la replicación  
  
1.  En el **Explorador de objetos**, expanda la tabla con la restricción CHECK que desee modificar y, a continuación, expanda la carpeta **Restricciones** .  
  
2.  Haga clic con el botón derecho en la restricción CHECK que quiera cambiar y, después, haga clic en **Modificar**.  
  
3.  En el cuadro de diálogo **Restricciones CHECK** , bajo **Diseñador de tablas**, seleccione el valor **No** para **Exigir para replicación**.  
  
4.  Haga clic en **Cerrar**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

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
## <a name="see-also"></a>Consulte también  
 [Especificar opciones de esquema](../../relational-databases/replication/publish/specify-schema-options.md)  
  
  
