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
manager: craigg
ms.openlocfilehash: cd861c50523e218bc1cf0ed6e538e66eeb3671f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756318"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Paso 3: prueba de concepto de la conexión a SQL con pyodbc

En este ejemplo debe considerarse como una prueba de concepto solo.  El código de ejemplo se ha simplificado para mayor claridad y no representa necesariamente las mejores prácticas recomendadas por Microsoft.  

**Ejecute el siguiente script de ejemplo** cree un archivo llamado test.py y agregue cada fragmento de código a medida que avanza. 

```
> python test.py
```
  
## <a name="step-1--connect"></a>Paso 1: conectar  
  
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
  
  
## <a name="step-2--execute-query"></a>Paso 2: Ejecutar consulta  
  
El cursor.executefunction puede usarse para recuperar un conjunto de resultados de una consulta en SQL Database. Esta función acepta cualquier consulta básicamente y devuelve un conjunto de resultados que se puede iterar mediante el uso de cursor.fetchone)
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print row[0] 
    row = cursor.fetchone()

```  
  
## <a name="step-3--insert-a-row"></a>Paso 3: Insertar una fila  
  
En este ejemplo se muestra cómo ejecutar un [insertar](../../../t-sql/statements/insert-transact-sql.md) instrucción de forma segura, pasar parámetros que protejan la aplicación de [inyección de código SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md) valor.    
  
  
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
  
Para obtener más información, consulte el [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).
