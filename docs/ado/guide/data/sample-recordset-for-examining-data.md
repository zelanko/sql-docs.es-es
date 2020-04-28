---
title: Conjunto de registros de ejemplo para examinar datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1882c5298d92e17a7ddaa165288fddfab7fdb02b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924304"
---
# <a name="sample-recordset-for-examining-data"></a>Conjunto de registros de ejemplo para examinar datos
En primer lugar, echemos un vistazo al objeto de **conjunto de registros** tal y como se devuelve mediante la siguiente consulta SQL, que se ejecuta en la base de datos de ejemplo Northwind en Microsoft SQL Server.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 El objeto de **conjunto de registros** resultante contiene todas las generaciones en la base de datos que se muestra en la tabla siguiente.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Peras secas orgánicas|30,0000|  
|14|Tofu|23,2500|  
|28|Rssle Sauerkraut|45,6000|  
|51|Manzanas secas Manjimup|53,0000|  
|74|Longlife Tofu|10,0000|  
  
 Si le interesa obtener estos resultados usted mismo, pruebe el siguiente ejemplo de JScript:  
  
-   [Ejemplo de JScript para devolver un conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
