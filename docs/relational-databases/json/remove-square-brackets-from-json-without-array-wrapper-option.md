---
title: "Eliminación de corchetes de JSON: opción WITHOUT_ARRAY_WRAPPER | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 36e612b6c3759d968687d8ba35286c399de02a74
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="remove-square-brackets-from-json---withoutarraywrapper-option"></a>Eliminación de corchetes de JSON: opción WITHOUT_ARRAY_WRAPPER
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Para quitar los corchetes que rodean la salida JSON de la cláusula **FOR JSON** de manera predeterminada, especifique la opción **WITHOUT_ARRAY_WRAPPER** . Utilice esta opción con un sola fila de resultados para generar un objeto JSON único como salida en lugar de una matriz con un único elemento.

Si utiliza esta opción con un resultado de varias filas, el resultado no es un valor JSON válido debido a varios elementos y los corchetes que faltan.  
  
## <a name="example-single-row-result"></a>Ejemplo (resultados de fila única)  
En el ejemplo siguiente se muestra la salida de la cláusula **FOR JSON** con y sin la opción **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Resultado** con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Resultado** (predeterminado) sin el **WITHOUT_ARRAY_WRAPPER** opción  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>Ejemplo (resultados de varias filas)
Este es otro ejemplo de una cláusula **FOR JSON** con y sin la opción **WITHOUT_ARRAY_WRAPPER** . Este ejemplo genera un resultado de varias filas. El resultado no es un valor JSON válido debido a varios elementos y los corchetes que faltan.
  
 **Consulta**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Resultado** con la opción **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Resultado** (predeterminado) sin el **WITHOUT_ARRAY_WRAPPER** opción  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  

