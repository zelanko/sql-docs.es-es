---
title: 'Paso 3: prueba de concepto de la conexión a SQL con pyodbc | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4bfd6e52-817d-4f0a-a33d-11466e3f0484
author: arob98
ms.author: angrobe
ms.openlocfilehash: c5d8adfa33541402fb50017c3790d38f0396d73d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78256905"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pyodbc"></a>Paso 3: prueba de concepto de la conexión a SQL con pyodbc

Este ejemplo es una prueba de concepto. El código de ejemplo se simplifica por claridad y no representa necesariamente los procedimientos recomendados que sugiere Microsoft.  

Para empezar, ejecute el siguiente script de ejemplo. Cree un archivo denominado test.py y agregue cada fragmento de código conforme avance. 

```
> python test.py
```
  
## <a name="connect"></a>Conectar  
  
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
  
  
## <a name="run-query"></a>Ejecutar consulta  
  
La función cursor.execute puede usarse para recuperar un conjunto de resultados de una consulta realizada a SQL Database. Esta función acepta una consulta y devuelve un conjunto de resultados que se puede iterar mediante el uso de cursor.fetchone().
  
  
```python
#Sample select query
cursor.execute("SELECT @@version;") 
row = cursor.fetchone() 
while row: 
    print(row[0])
    row = cursor.fetchone()

```  
  
## <a name="insert-a-row"></a>Insertar una fila  
  
En este ejemplo se muestra cómo ejecutar una instrucción [INSERT](../../../t-sql/statements/insert-transact-sql.md) de forma segura y pasar parámetros que protejan la aplicación de la [inyección de código SQL](../../../relational-databases/tables/primary-and-foreign-key-constraints.md).    
  
  
```python
#Sample insert query
cursor.execute("""
INSERT INTO SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) 
VALUES (?,?,?,?,?)""",
'SQL Server Express New 20', 'SQLEXPRESS New 20', 0, 0, CURRENT_TIMESTAMP) 
cnxn.commit()
row = cursor.fetchone()

while row: 
    print('Inserted Product key is ' + str(row[0]))
    row = cursor.fetchone()
```  

## <a name="azure-active-directory-and-the-connection-string"></a>Azure Active Directory y la cadena de conexión

pyODBC usa el controlador ODBC de Microsoft para SQL Server.
Si su versión del controlador ODBC es 17.1 o posterior, puede usar el modo interactivo de Azure Active Directory del controlador ODBC a través de pyODBC.
Esta opción interactiva funciona si Python y pyODBC permiten que el controlador ODBC muestre el cuadro de diálogo. La opción solo está disponible en los sistemas operativos Windows. 

### <a name="example-connection-string-for-azure-active-directory-interactive-authentication"></a>Ejemplo de cadena de conexión para la autenticación interactiva de Azure Active Directory

En el ejemplo siguiente se proporciona una cadena de conexión ODBC que especifica la autenticación interactiva de Azure Active Directory:

`server=Server;database=Database;UID=UserName;Authentication=ActiveDirectoryInteractive;`

Para más información sobre las opciones de autenticación del controlador ODBC, consulte [Uso de Azure Active Directory con el controlador ODBC](../../odbc/using-azure-active-directory.md#new-andor-modified-dsn-and-connection-string-keywords).

## <a name="next-steps"></a>Pasos siguientes
  
Para más información, vea el [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/).
