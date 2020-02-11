---
title: Find (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f394d5e3b3021ca240675d6979152c63b903190
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918625"
---
# <a name="find-method-ado"></a>Find (método) (ADO)
Busca en un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) la fila que cumple los criterios especificados. Opcionalmente, se puede especificar la dirección de la búsqueda, la fila inicial y el desplazamiento de la fila inicial. Si se cumplen los criterios, la posición de la fila actual se establece en el registro encontrado; de lo contrario, la posición se establece en el final (o en el inicio) del **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Criterios*  
 Valor de **cadena** que contiene una instrucción que especifica el nombre de columna, el operador de comparación y el valor que se van a usar en la búsqueda.  
  
 *SkipRows*  
 Opcional. Un valor **Long** , cuyo valor predeterminado es cero, que especifica el desplazamiento de fila desde la fila actual o el marcador de *Inicio* para comenzar la búsqueda. De forma predeterminada, la búsqueda se iniciará en la fila actual.  
  
 *SearchDirection*  
 Opcional. Valor [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) que especifica si la búsqueda debe comenzar en la fila actual o en la siguiente fila disponible en la dirección de la búsqueda. Una búsqueda incorrecta se detiene al final del **conjunto de registros** si el valor es **adSearchForward**. Una búsqueda incorrecta se detiene al principio del **conjunto de registros** si el valor es **adSearchBackward**.  
  
 *Iniciar*  
 Opcional. Marcador de **variante** que funciona como la posición inicial de la búsqueda.  
  
## <a name="remarks"></a>Observaciones  
 En los *criterios*solo se puede especificar un nombre de una sola columna. Este método no admite búsquedas en varias columnas.  
  
 El operador de comparación en *criterios* puede ser**>**"" (mayor que),**\<**"" (menor que), "=" (igual), ">=" (mayor o igual que), "<=" (menor o igual que), "<>" (no es igual a) o "like" (coincidencia de patrones).  
  
 El valor de *criterios* puede ser una cadena, un número de punto flotante o una fecha. Los valores de cadena se delimitan entre comillas simples o "#" (signo de número) (por ejemplo, "State = ' WA '" o "State = #WA #"). Los valores de fecha se delimitan con marcas "#" (signo de número) (por ejemplo, "start_date > #7/22/97 #"). Estos valores pueden contener horas, minutos y segundos para indicar las marcas de tiempo, pero no deben contener milisegundos o se producirán errores.  
  
 Si el operador de comparación es "like", el valor de cadena puede contener un asterisco (*) para buscar una o más apariciones de cualquier carácter o subcadena. Por ejemplo, "State like\*'" coincide con Maine y Massachusetts. También puede usar asteriscos iniciales y finales para buscar una subcadena incluida dentro de los valores. Por ejemplo, "State like '\*as\*'" coincide con Alaska, Arkansas y Massachusetts.  
  
 Los asteriscos solo se pueden usar al final de una cadena de criterios, o al principio y al final de una cadena de criterios, como se mostró anteriormente. No se puede usar el asterisco como carácter comodín inicial (' * str ') o como carácter comodín incrustado (\*r '). Esto producirá un error.  
  
> [!NOTE]
>  Se producirá un error si no se establece una posición de fila actual antes de llamar a **Find**. Se debe llamar a cualquier método que establezca la posición de la fila, como [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), antes de llamar a **Find**.  
  
> [!NOTE]
>  Si llama al método **Find** en un conjunto de registros y la posición actual en el conjunto de registros está en el último registro o final de archivo (EOF), no encontrará nada. Debe llamar al método **MoveFirst** para establecer la posición o el cursor actual al principio del conjunto de registros.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Find (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index (propiedad)](../../../ado/reference/ado-api/index-property.md)   
 [Optimize (propiedad dinámica) (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)
