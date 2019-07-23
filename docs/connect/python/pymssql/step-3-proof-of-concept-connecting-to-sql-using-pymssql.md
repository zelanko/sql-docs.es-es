---
title: 'Paso 3: prueba de concepto de la conexión a SQL con pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935776"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Paso 3: prueba de concepto de la conexión a SQL con pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Este ejemplo solo debe considerarse una prueba de concepto.  El código de ejemplo se simplifica para mayor claridad y no representa necesariamente las prácticas recomendadas recomendadas por Microsoft.  
  
## <a name="step-1--connect"></a>Paso 1: conexión  
  
La función [pymssql. Connect](https://pymssql.org/en/latest/ref/pymssql.html) se usa para conectarse a SQL Database.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Paso 2: ejecutar la consulta  
  
La función [cursor. Execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute) se puede usar para recuperar un conjunto de resultados de una consulta en SQL Database. Básicamente, esta función acepta cualquier consulta y devuelve un conjunto de resultados que se puede recorrer en iteración con el uso de [cursor. fetchone ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone).  
  
  
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
  
## <a name="step-3--insert-a-row"></a>Paso 3: insertar una fila  
  
En este ejemplo verá cómo ejecutar una instrucción [Insert](../../../t-sql/statements/insert-transact-sql.md) de forma segura, pasar parámetros que protejan la aplicación del valor de [inyección de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>Paso 4: reversión de una transacción  
  
En este ejemplo de código se muestra el uso de transacciones en las que:  
  
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
  
Para obtener más información, vea el [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).
