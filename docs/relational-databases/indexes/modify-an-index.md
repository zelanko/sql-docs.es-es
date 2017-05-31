---
title: "Modificación de un índice | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: baab89e891a068e358727fd2a8c739ef1b37b400
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="modify-an-index"></a>Modificar un índice
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo modificar un índice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Los índices creados como resultado de una restricción PRIMARY KEY o UNIQUE no se pueden modificar con este método. En su lugar, se debe modificar la restricción.  
  
 **En este tema**  
  
-   **Para modificar un índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-an-index"></a>Para modificar un índice  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, a continuación, la base de datos a la que pertenece la tabla y, por último, **Tablas**.  
  
3.  Expanda la tabla a la que pertenece el índice y, a continuación, **Índices**.  
  
4.  Haga clic con el botón derecho en el índice que quiera modificar y, después, haga clic en **Propiedades**.  
  
5.  En el cuadro de diálogo **Propiedades del índice** , realice los cambios deseados. Por ejemplo, puede agregar o quitar una columna de la clave de índice, o cambiar el valor de una opción de índice.  
  
#### <a name="to-modify-index-columns"></a>Para modificar columnas de índices  
  
1.  Para agregar, quitar o cambiar la posición de una columna de índice, seleccione la página **General** del cuadro de diálogo **Propiedades del índice** .  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-modify-an-index"></a>Para modificar un índice  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se quita y vuelve a crear un índice existente en la columna `ProductID` de la tabla `Production.WorkOrder` usando la opción `DROP_EXISTING` . También se establecen las opciones `FILLFACTOR` y `PAD_INDEX` .  
  
     [!code-sql[IndexDDL#CreateIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_1.sql)]  
  
     En el ejemplo siguiente se usa ALTER INDEX para establecer varias opciones del índice `AK_SalesOrderHeader_SalesOrderNumber`.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_2.sql)]  
  
#### <a name="to-modify-index-columns"></a>Para modificar columnas de índices  
  
1.  Para agregar, quitar o cambiar la posición de una columna de índice, debe quitar y volver a crear el índice.  
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)   
 [Cambiar el nombre a los índices](../../relational-databases/indexes/rename-indexes.md)  
  
  

