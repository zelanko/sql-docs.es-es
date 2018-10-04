---
title: Comandos de forma General | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d35f549581e9ac0a12c37cef90f66969aff1659
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633441"
---
# <a name="shape-commands-in-general"></a>Comandos Shape en General
La forma de datos define las columnas de una forma **Recordset**, las relaciones entre las entidades representadas por las columnas y la forma en que el **Recordset** se rellena con datos.  
  
 Una forma **Recordset** puede constar de los siguientes tipos de columnas.  
  
|Tipo de columna|Descripción|  
|-----------------|-----------------|  
|datos|Campos de un **Recordset** devuelto por un comando de consulta a un proveedor de datos, tabla o en forma de anteriormente **Recordset**.|  
|Capítulo|Una referencia a otro **Recordset**, denominado un *capítulo*. Columnas de capítulo permiten definir una *elementos primarios y secundarios* relación donde la *primario* es el **Recordset** que contiene la columna de capítulo y el *secundarios* es el **Recordset** representado por el capítulo.|  
|agregado|El valor de la columna se deriva ejecutando una *función de agregado* en todas las filas o una columna de todas las filas de un elemento secundario **Recordset**. (Vea las funciones de agregado en el tema siguiente, [las funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|Expresión calculada|El valor de la columna se deriva calculando un Visual Basic para la expresión de aplicaciones en las columnas de la misma fila de la **Recordset**. La expresión es el argumento a la función CALC. (Vea expresión calculada en el tema siguiente, [las funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) y en [Visual Basic para aplicaciones de funciones](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|nuevo|Campos creados vacíos, que se pueden rellenar con datos en un momento posterior. La columna se define con la palabra clave NEW. (Vea la nueva palabra clave en el tema siguiente, [las funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Un comando shape puede contener una cláusula que especifica un comando de consulta a un proveedor de datos subyacente que devolverá un **Recordset** objeto. Sintaxis de la consulta depende de los requisitos del proveedor de datos subyacente. Suele ser SQL, aunque ADO no requiere el uso de cualquier lenguaje de consulta en particular.  
  
 Pueden emitir comandos de forma **Recordset** objetos o mediante la configuración de la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad de la [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto y, a continuación, llamar a la [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
 Podría usar una cláusula SQL JOIN para relacionar las dos tablas; Sin embargo, jerárquica **Recordset** puede representar la información de forma más eficaz. Cada fila de un **Recordset** creado mediante una información de repeticiones de combinación redundante desde una de las tablas. Jerárquica **Recordset** tiene solo un elemento primario **Recordset** para cada uno de varios secundarios **Recordset** objetos.  
  
 Comandos de forma que se pueden anidar. Es decir, el *comando primario* o *comando secundario* puede ser otro comando shape.  
  
 El proveedor de formas siempre devuelve un cursor de cliente, incluso cuando el usuario especifica una posición del cursor del **adUseServer**.  
  
 Puede tener acceso a la **Recordset** componentes de la forma **Recordset** mediante programación o a través de un control visual adecuado.  
  
 Microsoft proporciona una herramienta visual que genera comandos shape (vea la [diseñador del entorno de datos](http://go.microsoft.com/fwlink/?LinkId=5689) en la documentación de Visual Basic 6) y otra que muestra cursores jerárquicos (vea "usar el Microsoft jerárquica FlexGrid Control"en la documentación de Visual Basic 6).  
  
 Para obtener información sobre la navegación jerárquica **Recordset**, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Para obtener información exacta sobre los comandos de forma sintácticamente correcto, consulte [gramática Formal de forma](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Emitir comandos al proveedor de datos subyacente](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
