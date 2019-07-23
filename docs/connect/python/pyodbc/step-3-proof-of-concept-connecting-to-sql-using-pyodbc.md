---
title: 'Paso 3: prueba de concepto de la conexión a SQL con pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87faa60456dd6d03f23d45346ab0dd103dc07c82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992507"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Paso 3: prueba de concepto de la conexión a SQL con pyodbc

Este ejemplo solo debe considerarse una prueba de concepto.  El código de ejemplo se simplifica para mayor claridad y no representa necesariamente las prácticas recomendadas recomendadas por Microsoft.  

**Ejecutar el script de ejemplo siguiente**  Cree un archivo denominado test.py y agregue cada fragmento de código a medida que vaya. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Paso 1: conexión  
  
```python

import pyodbc 
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'tcp:myserver.database.windows.net' 
database = 'mydb' 
username = 'myusername' 
password = 'mypassword' 
cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()

```  
  
  
## <a name="step-2--execute-query"></a>Paso 2: ejecutar la consulta  
  
El cursor. ExecuteFunction se puede usar para recuperar un conjunto de resultados de una consulta en SQL Database. Esta función acepta básicamente cualquier consulta y devuelve un conjunto de resultados que se puede recorrer en iteración con el uso de cursor. fetchone ()
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Paso 3: insertar una fila  
  
En este ejemplo verá cómo ejecutar una instrucción [Insert](../../../t-sql/statements/insert-transact-sql.md) de forma segura, pasar parámetros que protejan la aplicación del valor de [inyección de SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
  
```python

#Sample insert query
cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP )") 
row = cursor.fetchone()

while row: 
    print 'Inserted Product key is ' + str(row[0]) 
    row = cursor.fetchone()
```  
  `      
  ## <a name="next-steps"></a>Pasos siguientes  
  
Para obtener más información, vea el [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).
