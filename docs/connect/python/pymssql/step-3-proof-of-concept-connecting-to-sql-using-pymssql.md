---
title: 'Paso 3: Prueba de concepto que se conecta a SQL con pymssql | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e744d2e472e082cacb48a3e4f8c3a07a1f87bb03
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35309934"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Paso 3: Prueba de concepto que se conecta a SQL con pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

En este ejemplo debe considerarse una prueba de concepto solo.  El código de ejemplo se ha simplificado para mayor claridad y no representa necesariamente mejores prácticas recomendadas por Microsoft.  
  
## <a name="step-1--connect"></a>Paso 1: conectar  
  
El [pymssql.connect](http://pymssql.org/en/latest/ref/pymssql.html) función se utiliza para conectarse a la base de datos SQL.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Paso 2: Ejecutar consulta  
  
El [cursor.execute](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) función puede utilizarse para recuperar un conjunto de resultados de una consulta en base de datos de SQL. Esta función básicamente acepta cualquier consulta y devuelve un conjunto de resultados que puede ser recorre en iteración mediante el uso de [cursor.fetchone()](http://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>Paso 3: Insertar una fila  
  
En este ejemplo se muestra cómo ejecutar un [insertar](../../../t-sql/statements/insert-transact-sql.md) instrucción de forma segura, pasar parámetros que protección la aplicación de [inyección de código SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>Paso 4: Revertir una transacción  
  
Este ejemplo de código muestra el uso de transacciones en el que es:  
  
* Iniciar una transacción  
* Insertar una fila de datos  
* Revertir la transacción para deshacer la inserción  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>Pasos siguientes  
  
Para obtener más información, consulte el [Centro para desarrolladores de Python](https://azure.microsoft.com/en-us/develop/python/).
