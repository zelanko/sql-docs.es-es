---
title: Funcionamiento de los comandos sin parámetros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884ef4e72b975de0eb9dd92e80ec3ce0d513546b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187791"
---
# <a name="operation-of-non-parameterized-commands"></a>Funcionamiento de los comandos sin parámetros
Para los comandos sin parámetros, se ejecutan todos los comandos de proveedor y el **conjuntos de registros** se crean durante la ejecución del comando. Si el comando se ejecuta sincrónicamente, todas las **conjuntos de registros** se llenará totalmente. Si se ha seleccionado un modo de llenado asincrónico, el estado relleno de la **conjuntos de registros** dependerá del modo de llenado y el tamaño de la **conjuntos de registros**.  
  
 Por ejemplo, el *comando primario* podría devolver un **Recordset** de clientes para una compañía de una tabla de clientes y el *comando secundario* podría devolver un **Recordset** de pedidos de todos los clientes de una tabla de pedidos.  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 Para las relaciones de elementos primarios y secundarios sin parámetros, cada elemento primario y secundario **Recordset** objeto debe tener una columna en común para asociarlos. Las columnas se mencionen en la cláusula RELATE, *columna principal* primero y, a continuación, *columna secundaria*. Las columnas pueden tener nombres distintos en sus respectivos **Recordset** objetos pero debe hacer referencia a la misma información con el fin de especificar una relación significativa. Por ejemplo, el **clientes** y **registros Orders** objetos podrían tener un campo customerID. Dado que la pertenencia del elemento secundario **Recordset** viene determinada por el comando de proveedor, el elemento secundario **Recordset** puede contener filas huérfanas. Estas filas huérfanas son inaccesibles sin cambiar de forma adicional.  
  
 La forma de datos anexa una columna de capítulo con el elemento primario **Recordset**. Los valores de la columna de capítulo son referencias a las filas en el elemento secundario **Recordset**, que cumplen la cláusula RELATE. Es decir, el mismo valor en el *columna principal* de una fila principal determinada en el *columna secundaria* de todas las filas del secundario del capítulo. Cuando se usan varias cláusulas TO en la misma cláusula RELATE, implícitamente se combinan mediante un operador AND. Si las columnas primarias de la cláusula RELATE no constituyen una clave con el elemento primario **Recordset**, una fila secundaria única puede tener varias filas principales.  
  
 Cuando tenga acceso a la referencia de la columna de capítulo, ADO recupera automáticamente el **Recordset** representado por la referencia. Tenga en cuenta que en un comando sin parámetros, aunque todo el secundario **Recordset** ha sido recuperado, el capítulo sólo presenta un subconjunto de filas.  
  
 Si la columna anexada no tiene ningún *alias de capítulo*, se generará un nombre para ella automáticamente. Un [campo](../../../ado/reference/ado-api/field-object.md) objeto para la columna se anexará a la **Recordset** del objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección y su tipo de datos será **adChapter**.  
  
 Para obtener información sobre la navegación jerárquica **Recordset**, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
