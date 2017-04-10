---
title: "Uso de OPENJSON con el esquema predeterminado (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON, con el esquema predeterminado"
ms.assetid: 8e28a8f8-71a8-4c25-96b8-0bbedc6f41c4
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Uso de OPENJSON con el esquema predeterminado (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Use **OPENJSON** con el esquema predeterminado para devolver una tabla con una fila por cada propiedad del objeto o por cada elemento de la matriz.  
  
 Estos son algunos ejemplos que utilizan **OPENJSON** con el esquema predeterminado. Para obtener más información y más ejemplos, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## Ejemplo: Devolución de cada propiedad de un objeto  
 **Query**  
  
```tsql  
SELECT * FROM OPENJSON('{"name":"John","surname":"Doe","age":45}')  
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|name|John|  
|surname|Doe|  
|age|45|  
  
## Ejemplo: Devolución de cada elemento de una matriz  
 **Query**  
  
```tsql  
SELECT [key], value FROM OPENJSON('["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]')  
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
  
## Ejemplo: Convertir JSON a una tabla temporal  
 La siguiente consulta devuelve todas las propiedades del objeto **info** .  
  
```tsql  
SET @json = N'{  
    "info":{    
      "type":1,  
      "address":{    
        "town":"Bristol",  
        "county":"Avon",  
        "country":"England"  
      },  
      "tags":["Sport", "Water polo"]  
   },  
   "type":"Basic"  
}'  
  
SELECT * FROM OPENJSON(@json, N'lax $.info')  
```  
  
 **Resultado**  
  
|Key|Valor|Tipo|  
|---------|-----------|----------|  
|tipo|1|0|  
|address|{ "town":"Bristol", "county":"Avon", "country":"England" }|5|  
|etiquetas|[ "Sport", "Water polo" ]|4|  
  
## Ejemplo: Combinar datos relacionales y datos JSON  
 En el ejemplo siguiente, la tabla SalesOrderHeader tiene una columna de texto SalesReason que contiene una matriz de SalesOrderReasons en formato JSON. Los objetos de SalesOrderReasons contienen propiedades como "Manufacturer" y "Quality". En el ejemplo se crea un informe que combina todas las filas de pedidos de ventas y las razones de venta relacionadas expandiendo la matriz JSON de razones de venta como si las razones se almacenaran en una tabla secundaria independiente.  
  
```tsql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
    CROSS APPLY OPENJSON (SalesReasons)  
  
```  
  
 En este ejemplo, OPENJSON devuelve una tabla de razones de venta en la que las razones aparecen como la columna de valor. El operador CROSS APPLY combina cada fila de pedido de ventas con las filas devueltas por la función con valores de tabla OPENJSON.  
  
## Vea también  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  