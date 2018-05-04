---
title: Ejemplo de conjunto de registros para examinar los datos | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca05161aad6aaaf79f1e1af85d7e83d55e6997ad
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sample-recordset-for-examining-data"></a>Conjunto de registros de ejemplo para examinar datos
En primer lugar, echemos un vistazo a la **Recordset** objeto devuelto al utilizar la siguiente consulta SQL, que se ejecuta en los datos de ejemplo Northwind base en Microsoft SQL Server.  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 El resultante **Recordset** objeto contiene todos lo genera la base de datos se muestra en la tabla siguiente.  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|Peras secas orgánicas de tío Bob|30.0000|  
|14|Tofu|23.2500|  
|28|Rssle chucrut|45.6000|  
|51|Manzanas secas Manjimup|53.0000|  
|74|Longlife Tofu|10.0000|  
  
 Si está interesado en obtener estos resultados usted mismo, pruebe el siguiente ejemplo de JScript:  
  
-   [Ejemplo de JScript para devolver un conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
