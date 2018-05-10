---
title: Creación de claves principales | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- primary keys [SQL Server], creating
ms.assetid: 85c623ca-4656-4d70-a9db-ee4d897cd214
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 820dbb8998665eacef12417ada67222b967acd17
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-primary-keys"></a>Crear claves principales
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Crear claves principales](https://msdn.microsoft.com/en-US/library/ms189039(SQL.120).aspx).

  Puede definir una clave principal en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Al crear una clave principal, se crea automáticamente un índice agrupado único o bien un índice no agrupado si así se especifica.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Una tabla solo puede incluir una restricción PRIMARY KEY.  
  
-   Todas las columnas definidas en una restricción PRIMARY KEY se deben definir como NOT NULL. Si no se especifica nulabilidad, la nulabilidad de todas las columnas que participan en una restricción PRIMARY KEY se establece en NOT NULL.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 La creación de una tabla nueva con una clave principal requiere el permiso CREATE TABLE en la base de datos y el permiso ALTER en el esquema en el que se crea la tabla.  
  
 La creación de una clave principal de una tabla existente requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-create-a-primary-key"></a>Para crear una clave principal  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla a la que quiere agregar una restricción UNIQUE y haga clic en **Diseño**.  
  
2.  En el **Diseñador de tablas**, haga clic en el selector de filas de la columna de base de datos que desea definir como clave principal. Si desea seleccionar varias columnas, mantenga presionada la tecla CTRL mientras hace clic en los selectores de fila de las otras columnas.  
  
3.  Haga clic con el botón derecho en el selector de fila para la columna y seleccione **Establecer clave principal**.  
  
> [!CAUTION]  
>  Si desea volver a definir la clave principal, debe eliminar las relaciones establecidas con la clave principal existente antes de crear una nueva. Un mensaje le advertirá de que las relaciones existentes se eliminarán automáticamente durante este proceso.  
  
 Las columnas de clave principal se indican mediante un símbolo de clave principal en el selector de fila.  
  
 Si una clave principal consta de más de una columna, se admitirán valores duplicados en una columna, pero cada combinación de valores de todas las columnas de la clave principal debe ser única.  
  
 Si define una clave compuesta, el orden de las columnas de la clave principal coincide con el de las columnas mostradas en la tabla. Sin embargo, puede cambiar el orden de las columnas después de crear la clave principal. Para obtener más información, vea [Modificar claves principales](../../relational-databases/tables/modify-primary-keys.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  

### <a name="to-create-a-primary-key-in-an-existing-table"></a>Para crear una clave principal en una tabla existente  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una clave principal en la columna `TransactionID`.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Production.TransactionHistoryArchive   
    ADD CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID);  
    GO  
    ```  
  
### <a name="to-create-a-primary-key-in-a-new-table"></a>Para crear una clave principal en una nueva tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una tabla y define una clave principal en la columna `TransactionID`.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       TransactionID int IDENTITY (1,1) NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY CLUSTERED (TransactionID)  
    );  
    GO  
    ```  

### <a name="to-create-a-primary-key-with-nonclustered-index-in-a-new-table"></a>Crear una clave principal con un índice no agrupado en una tabla nueva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se crea una tabla y se define una clave principal en la columna `CustomerID` y un índice agrupado en `TransactionID`.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE Production.TransactionHistoryArchive1  
    (  
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,  
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)  
    );  
    GO  

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
    ```  

## <a name="see-also"></a>Ver también    
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)    
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)     
[table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)    
