---
title: Registro actual y el tamaño del conjunto de registros | Microsoft Docs
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
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bde55939e974c6c879dcd126fac863ef0a866487
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472608"
---
# <a name="current-record-and-size-of-recordset"></a>Registro actual y el tamaño del conjunto de registros
En esta sección se describe cómo buscar la posición actual del cursor en el ejemplo **Recordset** en [ejemplo de código JScript para devolver un conjunto de registros](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md).  
  
## <a name="current-record"></a>Registro actual  
 El registro actual en el conjunto de datos corresponde al que apunta a la posición del cursor de la **Recordset** objeto. Cuando un **Recordset** objeto se devuelve desde el origen de datos como resultado de llamar a **Recordset.Open**, **Command.Execute**, o **Connection.Execute**  (incluidos **Connection.NamedCommand** y **Connection.StoredProcedure**), el cursor se establece para que señale al primer registro. En el conjunto de datos de ejemplo, el registro inicial actual es la "de Bob tío secos orgánicos Peras" elemento.  
  
## <a name="size-of-recordset"></a>Tamaño del conjunto de registros  
 Para averiguar el tamaño de un **Recordset** de objeto, obtener el valor de la **Recordset.RecordCount** propiedad. Este valor es un entero largo que indica el número de registros en el **Recordset**. Si se devuelve el conjunto de datos desde el proveedor OLEDB de Microsoft SQL Server, este valor proporciona el número de filas devueltas. Leer el **RecordCount** propiedad en un cerrado **Recordset** produce un error.  
  
 Si no se puede determinar el número de registros, el valor de la propiedad es -1.  
  
 El valor de la **RecordCount** propiedad también depende de las capacidades del proveedor y el tipo de cursor que se utiliza. Para un cursor de solo avance, el valor es -1. Para un cursor estático o de conjunto de claves, el valor es el número real de los registros devueltos en la **Recordset** objeto. Para un cursor dinámico, el valor es -1 o el número real de registros, dependiendo del origen de datos.  
  
 Un cursor que admite **Recordcount** debe trabajo de más difícil y, por tanto, requiere más capacidad de proceso, que no se admite un cursor **Recordcount**. Si no necesita saber el número de registros, utilizando el tipo de cursor diferente podría ayudar a mejorar el rendimiento de la aplicación, especialmente si se debe tratar con un gran conjunto de datos.  
  
 En algunos casos, un proveedor o el cursor no puede determinar el **RecordCount** valor sin obtener primero todos los registros desde el origen de datos. Para garantizar un recuento preciso, llame a la **Recordset**. **MoveLast** método antes de llamar a **Recordset.RecordCount**.  
  
 El ejemplo **Recordset** objeto obtenido mediante la [ejemplo de código JScript](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md) utiliza un cursor de solo avance, por lo que una llamada a **RecordCount** en este objeto siempre da lugar a -1. Si cambia la línea de código que llama el **Recordset**. **Abra** método tal como se muestra en el ejemplo siguiente, la **RecordCount** propiedad devolverá el número real de registros recuperados.  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 Esto es estática porque los cursores con el [proveedor Microsoft OLE DB para SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) admite **RecordCount**. En este ejemplo, hay cinco registros y, por tanto, **RecordCount** debe obtener el valor de 5.  
  
 Esta sección contiene el siguiente tema.  
  
 [Límites de un conjunto de registros](../../../ado/guide/data/boundaries-of-a-recordset.md)
