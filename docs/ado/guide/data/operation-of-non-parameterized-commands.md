---
title: "Funcionamiento de los comandos sin parámetros | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1a025cf381bdf5a51cb825294bf5a5399fc033b2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="operation-of-non-parameterized-commands"></a>Funcionamiento de los comandos sin parámetros
Para los comandos sin parámetros, se ejecutan todos los comandos de proveedor y el **conjuntos de registros** se crean durante la ejecución del comando. Si el comando se ejecuta sincrónicamente, todos los **conjuntos de registros** se llenará totalmente. Si se ha seleccionado un modo de llenado asincrónico, el estado relleno de la **conjuntos de registros** dependerá del modo de llenado y el tamaño de la **conjuntos de registros**.  
  
 Por ejemplo, el *comando primario* podría devolver un **Recordset** de clientes para una compañía desde una tabla Customers y la *comando secundario* podría devolver un **Recordset** de pedidos para todos los clientes desde una tabla Orders.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Para las relaciones de elementos primarios y secundarios sin parámetros, cada primarios y secundarios **Recordset** objeto debe tener una columna en común para poder asociarlos. Las columnas se mencionen en la cláusula RELATE, *columna primaria* primero y, a continuación, *columna secundaria*. Las columnas pueden tener nombres distintos en sus respectivas **Recordset** objetos pero debe hacer referencia a la misma información con el fin de especificar una relación significativa. Por ejemplo, el **clientes** y **registros Orders** objetos podrían tener un campo customerID. Dado que la pertenencia del elemento secundario **Recordset** viene determinado por el comando de proveedor, el elemento secundario **Recordset** puede contener filas huérfanas. Estas filas huérfanas son inaccesibles sin reformular adicionales.  
  
 La forma de datos anexa una columna de capítulo al elemento primario **conjunto de registros**. Los valores de la columna de capítulo son referencias a las filas en el elemento secundario **Recordset**, que cumplen la cláusula RELATE. Es decir, el mismo valor en el *columna primaria* de una fila principal determinada en el *columna secundaria* de todas las filas del secundario del capítulo. Cuando se utilizan varias cláusulas TO en la misma cláusula RELATE, éstas se combinan implícitamente utilizando un operador AND. Si las columnas principales de la cláusula RELATE no constituyen una clave para el elemento primario **Recordset**, una fila secundaria única puede tener varias filas principales.  
  
 Cuando tiene acceso a la referencia de la columna de capítulo, ADO recupera automáticamente el **Recordset** representado por la referencia. Tenga en cuenta que en un comando sin parámetros, aunque todo el secundario **Recordset** ha sido recuperado, el capítulo sólo presenta un subconjunto de filas.  
  
 Si la columna anexada no tiene ningún *alias de capítulo*, se generará un nombre para ella automáticamente. A [campo](../../../ado/reference/ado-api/field-object.md) objeto para la columna se anexará a la **Recordset** del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) recopilación y su tipo de datos será **Dbtype_hchapter**.  
  
 Para obtener información sobre la navegación jerárquica **Recordset**, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
