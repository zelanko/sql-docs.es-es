---
title: 'Paso 3: Prueba de concepto de la conexión a SQL con Ruby | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992487"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>Paso 3: Prueba de concepto que se conecta a SQL con Ruby

Este ejemplo solo debe considerarse una prueba de concepto.  El código de ejemplo se simplifica para mayor claridad y no representa necesariamente las prácticas recomendadas recomendadas por Microsoft.  
  
## <a name="step-1--connect"></a>Paso 1: conexión  
  
La función [función tinytds:: Client](https://github.com/rails-sqlserver/tiny_tds) se usa para conectarse a SQL Database.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>Paso 2: Ejecutar una consulta  
  
Copie y pegue el código siguiente en un archivo vacío. Llámelo test. RB. Después, ejecútelo escribiendo el siguiente comando desde el símbolo del sistema:  
  
    ruby test.rb  
  
En el ejemplo de código, la función [función tinytds:: result](https://github.com/rails-sqlserver/tiny_tds) se usa para recuperar un conjunto de resultados de una consulta en SQL Database. Esta función acepta una consulta y devuelve un conjunto de resultados. El conjunto de resultados se recorre en iteración mediante el [resultado. cada do | Row |](https://github.com/rails-sqlserver/tiny_tds).  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>Paso 3: insertar una fila  
  
En este ejemplo verá cómo ejecutar una instrucción [Insert](../../t-sql/statements/insert-transact-sql.md) de forma segura, pasar parámetros que protejan la aplicación del valor de [inyección de SQL](../../relational-databases/tables/primary-and-foreign-key-constraints.md) .    
  
Para usar función tinytds con Azure, se recomienda ejecutar varias `SET` instrucciones para cambiar el modo en que la sesión actual controla la información específica. Las `SET` instrucciones recomendadas se proporcionan en el ejemplo de código. Por ejemplo, `SET ANSI_NULL_DFLT_ON` permitirá que se creen nuevas columnas para permitir valores NULL incluso si el estado de nulabilidad de la columna no se indica explícitamente.  
  
Para alinear con el formato de [fecha y hora](../../t-sql/data-types/datetime-transact-sql.md) Microsoft SQL Server, utilice la función [strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) para convertir al formato de fecha y hora correspondiente.  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
