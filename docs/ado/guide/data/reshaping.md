---
title: Cambiar la forma de | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58a09ecb5ad1828a94bdc5e5b82e59de61396be6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="reshaping"></a>Cambiar la forma
A **Recordset** creado por una cláusula de una forma de comando se puede asignar un *alias* nombre (normalmente con la palabra clave AS). El alias de una forma **Recordset** puede hacer referencia a un comando completamente diferente. Es decir, puede volver a usar, o *cambiar la forma de*, una forma anteriormente **Recordset** en un nuevo comando shape. Para admitir esta característica, ADO proporciona una propiedad, [cambiar la forma de nombre](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md).  
  
 Cambiar la forma tiene dos funciones principales. La primera consiste en asociar existente **Recordset** con un nuevo elemento primario **conjunto de registros**.  
  
## <a name="example"></a>Ejemplo  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 La segunda función consiste en habilitar el acceso no divididas en segmentos al elemento secundario existente **Recordset** objetos, mediante la sintaxis "forma \<cambiar la forma de conjunto de registros nombre >".  
  
> [!NOTE]
>  No se puede anexar columnas en una existente **conjunto de registros**, cambiar la forma de una con parámetros **Recordset** o **conjunto de registros** objetos en cualquier cláusula COMPUTE intermedia, o bien realizar agregar operaciones en ninguna **Recordset** descendientes desde el **Recordset** que se va a cambiar la forma. El **Recordset** que se va a cambiar la forma y la nueva forma de comandos deben utilizar ambos el mismo [conexión](../../../ado/reference/ado-api/connection-object-ado.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)
