---
title: Cláusula APPEND de forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7b51e2cbfb298493e7001937f7b0f274044478a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801595"
---
# <a name="shape-append-clause"></a>Cláusula APPEND Shape
La cláusula APPEND de comando de forma que anexa una o varias columnas a un **Recordset**. Con frecuencia, estas columnas son columnas de capítulo, que hacen referencia a un elemento secundario **Recordset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Descripción  
 Las partes de esta cláusula son los siguientes:  
  
 *comando primario*  
 Cero o uno de los siguientes (se puede omitir el *comando primario* completamente):  
  
-   Un comando de proveedor entre llaves ("{}") que devuelve un **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, aunque ADO no requiere ningún lenguaje de consulta determinada.  
  
-   Otro comando shape incrustado entre paréntesis.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *alias del primario*  
 Un alias opcional que hace referencia al elemento primario **Recordset**.  
  
 *lista de columnas*  
 Uno o varios de los siguientes:  
  
-   Una columna agregada.  
  
-   Una columna calculada.  
  
-   Una nueva columna creada mediante la cláusula nuevo.  
  
-   Una columna de capítulo. Una definición de columna de capítulo se encierra entre paréntesis ((")"). Consulte la siguiente sintaxis.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Comentarios  
 *child-recordset*  
 -   Un comando de proveedor entre llaves ("{}") que devuelve un **Recordset** objeto. El comando se emite al proveedor de datos subyacente, y su sintaxis depende de los requisitos de ese proveedor. Normalmente será el lenguaje SQL, aunque ADO no requiere ningún lenguaje de consulta determinada.  
  
-   Otro comando shape incrustado entre paréntesis.  
  
-   El nombre de una existente en forma de **Recordset**.  
  
-   La tabla (palabra clave), seguido del nombre de una tabla en el proveedor de datos.  
  
 *alias de elemento secundario*  
 Un alias que hace referencia al elemento secundario **Recordset**.  
  
 *columna primaria*  
 Una columna en la **Recordset** devuelto por la *comando primario.*  
  
 *columna secundaria*  
 Una columna en la **Recordset** devuelto por la *comando secundario*.  
  
 *número de parámetros*  
 Consulte [funcionamiento de los comandos con parámetros](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *alias de capítulo*  
 Un alias que hace referencia a la columna de capítulo anexada al elemento primario.  
  
> [!NOTE]
>  El *"columna primaria* TO *columna secundaria"* cláusula es realmente una lista, donde cada relación definida está separado por una coma  
  
> [!NOTE]
>  La cláusula después de la palabra clave APPEND es realmente una lista, donde cada cláusula separado por una coma y define otra columna que se debe anexar al elemento primario.  
  
## <a name="remarks"></a>Comentarios  
 Al construir los comandos de proveedor de entrada del usuario como parte de un comando SHAPE, SHAPE tratará proporcionado por el usuario un comando de proveedor como una cadena opaca y pasarlos fielmente al proveedor. Por ejemplo, en el siguiente comando de forma  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE ejecutará dos comandos: `select * from t1` y (`select * from t2 RELATE k1 TO k2)`. Si el usuario proporciona un comando compuesto que consta de varios comandos de proveedor separados por punto y coma, SHAPE no es capaz de distinguir la diferencia. Así que en el siguiente comando de forma  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Ejecuta de forma `select * from t1; drop table t1` y (`select * from t2 RELATE k1 TO k2),` sin darse cuenta que `drop table t1` es un independiente y en este comando de proveedor de caso, peligroso. Las aplicaciones siempre deben validar la entrada del usuario para evitar estos posibles ataques de piratas informáticos que se produzca.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Funcionamiento de los comandos sin parámetros](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Funcionamiento de los comandos con parámetros](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandos híbridos](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Cláusulas COMPUTE de forma que intervengan](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
