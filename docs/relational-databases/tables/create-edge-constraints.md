---
title: Crear restricciones perimetrales | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97ad249695c4fbe0fd79a23a5493d998fbaf5191
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67582308"
---
# <a name="create-edge-constraints"></a>Crear restricciones perimetrales
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

   Puede definir una restricción perimetral en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. 
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las restricciones perimetrales solo se pueden definir en tablas perimetrales de gráficos. 
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  

### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>Para crear una restricción perimetral en una nueva tabla perimetral
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se crea una restricción perimetral en la tabla perimetral **bought**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO
 ```  

### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>Para agregar una restricción perimetral a una tabla perimetral existente 
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se usa ALTER TABLE para agregar una restricción perimetral a la tabla perimetral **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product)
 GO
 ```  

### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>Crear una restricción perimetral en una tabla perimetral existente con cláusulas de restricción perimetral adicionales
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se usa ALTER TABLE para agregar una nueva restricción perimetral con cláusulas de restricción perimetral adicionales a la tabla perimetral **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Supplier
    (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO

 -- User ALTER TABLE to create a new edge constraint.
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  
 Tenga en cuenta que hay dos cláusulas de restricción perimetral en la restricción *EC_BOUGHT1*, una que conecta **Customer** (Cliente) con **Product** (Producto) y otra que conecta **Supplier** (Proveedor) con **Product** (Producto). Estas dos cláusulas se aplican como disyunción; es decir, un perímetro determinado tiene que cumplir cualquiera de estas dos cláusulas para poder estar permitido en la tabla perimetral. 



### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>Crear una restricción perimetral en una tabla perimetral existente con una cláusula de restricción perimetral nueva
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se usa ALTER TABLE para agregar una nueva restricción perimetral con una cláusula de restricción perimetral nueva a la tabla perimetral **bought**.
  
 ```sql
 USE TEMPDB
 GO
 -- CREATE node and edge tables
 CREATE TABLE Customer
    (
        ID INTEGER PRIMARY KEY, 
        CustomerName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Supplier
    (
        ID INTEGER PRIMARY KEY, 
        SupplierName VARCHAR(100)
    )
 AS NODE
 GO

 CREATE TABLE Product 
  (
        ID INTEGER PRIMARY KEY, 
        ProductName VARCHAR(100)
  ) AS NODE
 GO

 CREATE TABLE bought
    (
        PurchaseCount INT,
        CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
 AS EDGE
 GO

 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product)
 GO
 ```  

 En este ejemplo hemos creado dos restricciones perimetrales independientes en la tabla perimetral **bought**: *EC_BOUGHT* y *EC_BOUGHT1*. Ambas restricciones perimetrales tienen cláusulas de restricción perimetral diferentes. Si una tabla perimetral contiene más de una restricción perimetral, un perímetro concreto tendrá que cumplir **TODAS** las restricciones perimetrales para poder estar permitido en la tabla perimetral. Puesto que en este caso ningún perímetro podrá cumplir *EC_BOUGHT* y *EC_BOUGHT1*, la tabla perimetral **bought** deberá permanecer vacía. 

 Para que las inserciones se efectúen correctamente en esta tabla perimetral, se debe quitar una de las restricciones perimetrales o bien las dos y crear una restricción perimetral que contenga ambas cláusulas de restricción perimetral. 

 ```sql
 USE TEMPDB
 GO
 -- Drop the existing edge constraint first and then create a new one.
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT
 GO
 
 ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1
 GO
 
 ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product)
 GO
 ```  

 Ahora, para que se permita un perímetro concreto en la tabla perimetral **bought**, tiene que cumplir cualquiera de las cláusulas de restricción perimetral de la restricción *EC_BOUGHT_NEW*. Por lo tanto, se permitirá cualquier perímetro que esté intentando unos nodos **Customer**-**Product** (Cliente-Producto) o **Supplier**-**Product** (Proveedor-Producto) válidos. 
