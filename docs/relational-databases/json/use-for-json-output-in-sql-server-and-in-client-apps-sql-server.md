---
title: "Uso de salidas FOR JSON en SQL Server y en aplicaciones cliente (SQL Server) | Microsoft Docs"
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
  - "FOR JSON, usar en aplicaciones cliente"
  - "FOR JSON, usar en SQL Server"
ms.assetid: 302e5397-b499-4ea3-9a7f-c24ccad698eb
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# Uso de salidas FOR JSON en SQL Server y en aplicaciones cliente (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Los siguientes ejemplos muestran algunas de las formas de usar la cláusula **FOR JSON** o su salida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en aplicaciones cliente.  
  
## Uso de salidas FOR JSON en variables de SQL Server  
 La salida de la cláusula FOR JSON es de tipo NVARCHAR(MAX), así que se puede asignar a cualquier variable, como se muestra en el ejemplo siguiente.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = (SELECT TOP 10 * FROM Sales.SalesOrderHeader FOR JSON AUTO)  
```  
  
## Uso de salidas FOR JSON en funciones definidas por el usuario de SQL Server  
 Puede crear funciones definidas por el usuario que formatean conjuntos de resultados como JSON y devuelven esta salida JSON. En el ejemplo siguiente se crea una función definida por el usuario que recupera algunas filas de detalle de pedido de ventas y las formatea como una matriz JSON.  
  
```tsql  
CREATE FUNCTION GetSalesOrderDetails(@salesOrderId int)  
RETURNS NVARCHAR(MAX)  
AS  
BEGIN  
  RETURN (SELECT UnitPrice, OrderQty  
          FROM Sales.SalesOrderDetail  
          WHERE SalesOrderID = @salesOrderId  
          FOR JSON AUTO)  
END  
```  
  
 Puede utilizar esta función en un lote o una consulta, como se muestra en el ejemplo siguiente.  
  
```tsql  
DECLARE @x NVARCHAR(MAX) = dbo.GetSalesOrderDetails(43659)  
PRINT dbo.GetSalesOrderDetails(43659)  
SELECT TOP 10 H.*, dbo.GetSalesOrderDetails(H.SalesOrderId) AS Details  
FROM Sales.SalesOrderHeader H  
```  
  
## Combinación de datos primarios y secundarios en una sola tabla  
 En el ejemplo siguiente, cada conjunto de filas secundarias se formatea como una matriz JSON y se convierte en el valor de la columna de detalles de la tabla primaria.  
  
```tsql  
select top 10 SalesOrderId, OrderDate,  
     (select top 3 UnitPrice, OrderQty  
        from Sales.SalesOrderDetail D  
        where H.SalesOrderId = D.SalesOrderID  
        for json auto) as Details  
into SalesOrder  
from Sales.SalesOrderHeader H  
```  
  
## Actualización de los datos en columnas JSON  
 En el ejemplo siguiente se muestra que se puede actualizar el valor de las columnas que contienen texto JSON.  
  
```tsql  
UPDATE SalesOrder  
SET Details =  
    (SELECT TOP 1 UnitPrice, OrderQty  
      FROM Sales.SalesOrderDetail D  
      WHERE D.SalesOrderId = SalesOrder.SalesOrderId  
     FOR JSON AUTO)  
```  
  
## Uso de salidas FOR JSON en una aplicación cliente de C#  
 En el ejemplo siguiente se muestra cómo recuperar la salida JSON de una consulta en un objeto StringBuilder en una aplicación cliente de C#. Supongamos que la variable queryWithForJson contiene el texto de una instrucción SELECT con una cláusula FOR JSON.  
  
```csharp  
var cmd = new SqlCommand(queryWithForJson, conn);  
conn.Open();  
var jsonResult = new StringBuilder();  
var reader = cmd.ExecuteReader();  
if (!reader.HasRows)  
{  
    jsonResult.Append("[]");  
}  
else  
{  
    while (reader.Read())  
    {  
        jsonResult.Append(reader.GetValue(0).ToString());  
    }  
}  
```  
  
## Vea también  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  