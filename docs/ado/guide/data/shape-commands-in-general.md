---
title: Forma comandos en General | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 245f842883ec0be1ac92ad58ea75b4cdef7d9cb3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="shape-commands-in-general"></a>Comandos Shape en General
Dar forma a datos define las columnas de una forma **Recordset**, las relaciones entre las entidades representadas por las columnas y la forma en que la **Recordset** se rellena con datos.  
  
 Una forma **Recordset** puede constar de los siguientes tipos de columnas.  
  
|Tipo de columna|Description|  
|-----------------|-----------------|  
|data|Campos de un **Recordset** devuelto por un comando de consulta a un proveedor de datos, tabla o en forma de anteriormente **conjunto de registros**.|  
|capítulo|Una referencia a otro **Recordset**, denominado un *capítulo*. Columnas de capítulo permiten definir una *elementos primarios y secundarios* relación donde la *primario* es el **Recordset** que contiene la columna de capítulo y el *secundarios* es el **Recordset** representado por el capítulo.|  
|agregado|El valor de la columna se deriva ejecutando una *función de agregado* en todas las filas o una columna de todas las filas de un elemento secundario **conjunto de registros**. (Vea funciones de agregado en el tema siguiente, [funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|expresión calculada|El valor de la columna se deriva calculando un ejemplo de Visual Basic para la expresión de aplicaciones en las columnas de la misma fila de la **conjunto de registros**. La expresión es el argumento a la función CALC. (Vea expresión calculada en el tema siguiente, [funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) y en [de Visual Basic para aplicaciones de funciones](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|nuevo|Campos creados vacíos, que se pueden rellenar con datos en un momento posterior. La columna se define con la palabra clave NEW. (Vea la nueva palabra clave en el tema siguiente, [funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Un comando shape puede contener una cláusula que especifica un comando de consulta a un proveedor de datos subyacente que va a devolver un **Recordset** objeto. Sintaxis de la consulta depende de los requisitos del proveedor de datos subyacente. Normalmente será SQL, aunque ADO no requiere el uso de cualquier lenguaje de consulta en particular.  
  
 Puede emitir comandos de forma **Recordset** objetos o al establecer la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad de la [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto y, a continuación, llamar a la [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) (método).  
  
 Puede usar una cláusula JOIN de SQL para relacionar dos tablas; Sin embargo, jerárquica **Recordset** puede representar la información de forma más eficaz. Cada fila de un **Recordset** creado por una información de repeticiones de combinación repetidamente desde una de las tablas. Jerárquica **Recordset** tiene solo un primario **Recordset** para cada uno de varios secundarios **Recordset** objetos.  
  
 Comandos de forma que se pueden anidar. Es decir, el *comando primario* o *comando secundario* puede ser otro comando shape.  
  
 El proveedor de formas siempre devuelve un cursor de cliente, incluso cuando el usuario especifica una ubicación del cursor de **adUseServer**.  
  
 Puede tener acceso a la **Recordset** componentes de la forma **Recordset** mediante programación o a través de un control visual apropiado.  
  
 Microsoft ofrece una herramienta visual que genera comandos shape (vea la [diseñador del entorno de datos](http://go.microsoft.com/fwlink/?LinkId=5689) en la documentación de Visual Basic 6) y otra que muestra cursores jerárquicos (vea "usar el Microsoft jerárquica FlexGrid Control"en la documentación de Visual Basic 6).  
  
 Para obtener información sobre la navegación jerárquica **Recordset**, consulte [obtener acceso a filas en un conjunto de registros jerárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Para obtener información precisa sobre los comandos shape sintácticamente correcto, consulte [gramática Formal del comando Shape](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Las funciones de agregado, la función CALC y la palabra clave NEW](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Emitir comandos al proveedor de datos subyacente](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)

