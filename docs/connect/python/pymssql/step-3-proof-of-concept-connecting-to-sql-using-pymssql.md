---
title: 'Paso 3: Prueba de concepto de la conexión a SQL con pymssql | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea474658e57c3f61df7eb95866ea4688c942a750
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80913115"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>Paso 3: Prueba de concepto de la conexión a SQL con pymssql
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

Este ejemplo solo debe considerarse una prueba de concepto.  El código de ejemplo se simplifica para mayor claridad y no representa necesariamente los procedimientos recomendados por Microsoft.  
  
## <a name="step-1--connect"></a>Paso 1:  Conectar  
  
La función [pymssql.connect](https://pypi.org/project/pymssql/) se usa para conectarse a SQL Database.  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>Paso 2:  Ejecutar consulta  
  
La función [cursor.execute](https://pypi.org/project/pymssql/) puede usarse para recuperar un conjunto de resultados de una consulta realizada a SQL Database. Esta función acepta cualquier consulta y devuelve un conjunto de resultados que se puede iterar mediante el uso de [cursor.fetchone()](https://pypi.org/project/pymssql/).  
  
  
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
  
## <a name="step-3--insert-a-row"></a>Paso 3:  Inserción de una fila  
  
En este ejemplo se muestra cómo ejecutar la instrucción [INSERT](../../../t-sql/statements/insert-transact-sql.md) de forma segura y pasar parámetros que protejan la aplicación ante el valor de [inyección de código SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
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
  
## <a name="step-4--rollback-a-transaction"></a>Paso 4:  Reversión de una transacción  
  
Este ejemplo de código muestra el uso de transacciones con las que podrá realizar lo siguiente:  
  
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
  
Para más información, vea el [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).
