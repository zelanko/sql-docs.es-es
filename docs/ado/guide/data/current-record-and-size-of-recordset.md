---
title: Registro actual y el tamaño del conjunto de registros | Documentos de Microsoft
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
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47039bdba7fe5d5a867df4ac7ca8700a7a835b13
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="current-record-and-size-of-recordset"></a>Registro actual y el tamaño del conjunto de registros
Esta sección describe cómo buscar la posición actual del cursor en el ejemplo **Recordset** en [ejemplo de código de JScript para devolver un conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Registro actual  
 El registro actual en el conjunto de datos corresponde al que apunta la posición del cursor de la **Recordset** objeto. Cuando un **Recordset** objeto se devuelve desde el origen de datos como resultado de llamar al método **Recordset.Open**, **Command.Execute**, o **Connection.Execute**  (incluidos **Connection.NamedCommand** y **Connection.StoredProcedure**), el cursor se establece para que apunten a la primera entrada. En el conjunto de datos de ejemplo, el registro actual es el "Peras de secas orgánicas del tío Bob" elemento.  
  
## <a name="size-of-recordset"></a>Tamaño del conjunto de registros  
 Para averiguar el tamaño de un **Recordset** de objetos, obtener el valor de la **Recordset.RecordCount** propiedad. Este valor es un entero largo que indica el número de registros en la **conjunto de registros**. Si el conjunto de datos se devuelve desde el proveedor OLEDB de Microsoft SQL Server, este valor proporciona el número de filas devueltas. Leer la **RecordCount** propiedad en un cerrado **Recordset** produce un error.  
  
 Si no se puede determinar el número de registros, el valor de la propiedad es -1.  
  
 El valor de la **RecordCount** propiedad también depende de las capacidades del proveedor y el tipo de cursor que se utiliza. Para un cursor de solo avance, el valor es -1. Para un cursor estático o de conjunto de claves, el valor es el número real de registros devueltos en la **Recordset** objeto. Para un cursor dinámico, el valor es -1 o el número real de registros, dependiendo del origen de datos.  
  
 Un cursor que admite **Recordcount** debe trabajo de más difícil y, por tanto, requiere más capacidad informática, de un cursor no admite **Recordcount**. Si no necesita conocer el número de registros, utilizar otro tipo de cursor puede ayudar a mejorar el rendimiento de la aplicación, especialmente si es necesario administrar un gran conjunto de datos.  
  
 En algunos casos, un proveedor o el cursor es no se puede determinar la **RecordCount** valor sin obtener primero todos los registros desde el origen de datos. Para garantizar un recuento preciso, llame a la **Recordset**. **MoveLast** método antes de llamar a **Recordset.RecordCount**.  
  
 El ejemplo **Recordset** objeto obtenido mediante la [ejemplo de código JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) utiliza un cursor de solo avance, por lo que una llamada a **RecordCount** en este objeto siempre da lugar a -1. Si cambia la línea de código que llama la **Recordset**. **Abra** método tal como se muestra en el ejemplo siguiente, la **RecordCount** propiedad devolverá el número real de los registros obtenidos.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Esto es estático porque los cursores con el [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) admite **RecordCount**. En este ejemplo, hay cinco registros, por lo que **RecordCount** debe proporcionar el valor de 5.  
  
 Esta sección contiene el siguiente tema.  
  
 [Límites de un conjunto de registros](../../../ado/guide/data/boundaries-of-a-recordset.md)
