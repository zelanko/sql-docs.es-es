---
title: Modificación de un índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], modifying
- modifying indexes
- index changes [SQL Server]
ms.assetid: 97e3110d-fde7-4f5d-9309-dc1697960aeb
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: dfd7171832c37ee4e269e70aaf40251c6e0adecd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112914"
---
# <a name="modify-an-index"></a>Modificar un índice
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
  
     [!code-sql[IndexDDL#CreateIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/createindex.sql#createindex4)]  
  
     En el ejemplo siguiente se usa ALTER INDEX para establecer varias opciones del índice `AK_SalesOrderHeader_SalesOrderNumber`.  
  
     [!code-sql[IndexDDL#AlterIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/alterindex.sql#alterindex4)]  
  
#### <a name="to-modify-index-columns"></a>Para modificar columnas de índices  
  
1.  Para agregar, quitar o cambiar la posición de una columna de índice, debe quitar y volver a crear el índice.  
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/indexproperty-transact-sql)   
 [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)   
 [sys.index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-index-columns-transact-sql)   
 [Establecer opciones de índice](set-index-options.md)   
 [Cambiar el nombre a los índices](indexes.md)  
  
  
