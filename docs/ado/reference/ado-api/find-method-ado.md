---
title: "Find (método) (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ee7c7feb630040fce10311335f414213bba4ada
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="find-method-ado"></a>Find (método) (ADO)
Busca un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) para la fila que cumple los criterios especificados. Si lo desea, se puede especificar la dirección de la búsqueda, la fila inicial y el desplazamiento desde la fila inicial. Si se cumplen los criterios, la posición de fila actual se establece en el registro encontrado; en caso contrario, se establece la posición al final (o inicio) de la **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Criterios*  
 A **cadena** valor que contiene una instrucción que especifica el nombre de columna, el operador de comparación y el valor para usar en la búsqueda.  
  
 *SkipRows*  
 Opcional*.* A **largo** valor, cuyo valor predeterminado es cero, que especifica el desplazamiento de fila de la fila actual o *iniciar* marcador que se va a comenzar la búsqueda. De forma predeterminada, se iniciará la búsqueda en la fila actual.  
  
 *SearchDirection*  
 Opcional*.* A [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) valor que especifica si la búsqueda debe iniciar en la fila actual o la siguiente fila disponible en la dirección de la búsqueda. Detiene una búsqueda al final de la **Recordset** si el valor es **adSearchForward**. Se detiene una búsqueda en el inicio de la **Recordset** si el valor es **adSearchBackward**.  
  
 *Inicio*  
 Opcional. A **Variant** marcador que funciona como la posición inicial de la búsqueda.  
  
## <a name="remarks"></a>Comentarios  
 Se puede especificar sólo un nombre de columna única en *criterios*. Este método no admite búsquedas en varias columnas.  
  
 El operador de comparación *criterios* puede ser "**>**"(mayor que),"**\<**" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), "<>" (no es igual a) o "like" (coincidencia de modelos).  
  
 El valor de *criterios* puede ser una cadena, un número de punto flotante o una fecha. Valores de cadena se delimitan con comillas simples o marcas "#" (signo de número) (por ejemplo, "estado = 'WA'" o "estado = WA #"). Los valores de fecha se delimitan con marcas de "#" (signo de número) (por ejemplo, "fecha_inicial > #7/22/&#97;"). Estos valores pueden contener horas, minutos y segundos para indicar las marcas de tiempo, pero no deben contener milisegundos o se producirán errores.  
  
 Si el operador de comparación es "like", el valor de cadena puede contener un asterisco (*) para buscar una o más apariciones de cualquier carácter o una subcadena. Por ejemplo, "state like'm\*'" encuentra Maine y Massachusetts. También puede utilizar asteriscos iniciales y finales para buscar una subcadena dentro de los valores. Por ejemplo, "estado como '\*como\*'" encuentra Alaska, Arkansas y Massachusetts.  
  
 Pueden utilizar asteriscos de solo al final de una cadena de criterios, o al principio y al final de una cadena de criterios, como se indicó anteriormente. No se puede usar el asterisco como carácter comodín inicial ('* str'), o como un incrustado indicado anteriormente\*r'). Esto producirá un error.  
  
> [!NOTE]
>  Se producirá un error si no se establece una posición de fila actual antes de llamar a **buscar**. Cualquier método que establece la posición de la fila, tales como [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), debe llamarse antes de llamar a **buscar**.  
  
> [!NOTE]
>  Si se llama a la **buscar** método en un conjunto de registros y la posición actual en el conjunto de registros está en el último registro o al final del archivo (EOF), no encontrará nada. Debe llamar a la **MoveFirst** método para establecer el cursor o la posición actual hasta el principio del conjunto de registros.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo (VB) del método Find](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Propiedad Index](../../../ado/reference/ado-api/index-property.md)   
 [Optimizar la propiedad dinámica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)

