---
title: Buscar (método) (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7e71776a43aa338246b4acb3b4d9f620c19234f0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748225"
---
# <a name="find-method-ado"></a>Find (método) (ADO)
Busca un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para la fila que cumple los criterios especificados. Opcionalmente, se puede especificar la dirección de la búsqueda, la fila inicial y el desplazamiento desde la fila inicial. Si se cumplen los criterios, la posición de fila actual se establece en el registro se encuentra; en caso contrario, se establece la posición al final (o inicio) de la **Recordset**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Criterios*  
 Un **cadena** valor que contiene una instrucción que especifica el nombre de columna, el operador de comparación y el valor para usar en la búsqueda.  
  
 *Skiprows al*  
 Opcional *.* Un **largo** valor, cuyo valor predeterminado es cero, que especifica el desplazamiento de fila de la fila actual o *iniciar* marcador para iniciar la búsqueda. De forma predeterminada, se iniciará la búsqueda en la fila actual.  
  
 *SearchDirection*  
 Opcional *.* Un [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) valor que especifica si debe comenzar la búsqueda en la fila actual o la próxima fila disponible en la dirección de la búsqueda. Una búsqueda se detiene al final de la **Recordset** si el valor es **adSearchForward**. Una búsqueda se detiene al comienzo de la **Recordset** si el valor es **adSearchBackward**.  
  
 *Inicio*  
 Opcional. Un **Variant** marcador que funciona como la posición inicial de la búsqueda.  
  
## <a name="remarks"></a>Comentarios  
 Se puede especificar solo un nombre de columna única en *criterios*. Este método no admite búsquedas en varias columnas.  
  
 El operador de comparación *criterios* puede ser "**>**"(mayor que),"**\<**" (menor que), "=" (igual), "> =" (mayor o igual que), "< =" (menor o igual que), "<>" (no es igual a) o "like" (coincidencia).  
  
 El valor de *criterios* puede ser una cadena, número de punto flotante o fecha. Los valores de cadena están delimitados con comillas simples o marcas "#" (signo de número) (por ejemplo, "estado = 'WA'" o "estado = WA #"). Los valores de fecha se delimitan con marcas de "#" (signo de número) (por ejemplo, "start_date > #7/22/97 #"). Estos valores pueden contener horas, minutos y segundos para indicar las marcas de tiempo, pero no deben contener milisegundos o se producirán errores.  
  
 Si el operador de comparación es "like", el valor de cadena puede contener un asterisco (*) para buscar una o más apariciones de cualquier carácter o subcadena. Por ejemplo, "state like'm\*'" encuentra Maine y Massachusetts. También puede utilizar asteriscos iniciales y finales para buscar una subcadena dentro de los valores. Por ejemplo, "estado como '\*como\*'" coincide con Alaska, Arkansas y Massachusetts.  
  
 Asteriscos pueden usarse solo al final de una cadena de criterios, o al principio y al final de una cadena de criterios, como se indicó anteriormente. No se puede usar el asterisco como comodín inicial ('* str'), o como un indicado incrustado anteriormente\*r'). Esto provocará un error.  
  
> [!NOTE]
>  Se producirá un error si no se establece una posición de fila actual antes de llamar a **encontrar**. Cualquier método que establece la posición de fila, tales como [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), debe llamarse antes de llamar a **encontrar**.  
  
> [!NOTE]
>  Si se llama a la **buscar** método en un conjunto de registros y la posición actual en el conjunto de registros no está en el último registro o el final del archivo (EOF), no encontrará nada. Se debe llamar a la **MoveFirst** método para establecer el cursor o la posición actual hasta el principio del conjunto de registros.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Buscar el ejemplo del método (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Propiedad Index](../../../ado/reference/ado-api/index-property.md)   
 [Optimizar la propiedad dinámica (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [El método de búsqueda](../../../ado/reference/ado-api/seek-method.md)
