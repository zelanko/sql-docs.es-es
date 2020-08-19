---
description: Método CompareBookmarks (ADO)
title: CompareBookmarks (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: rothja
ms.author: jroth
ms.openlocfilehash: 4729574b92b841da48f7cf6de6f1dcabc369b4a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450807"
---
# <a name="comparebookmarks-method-ado"></a>Método CompareBookmarks (ADO)
Compara dos marcadores y devuelve una indicación de sus valores relativos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de [CompareEnum](../../../ado/reference/ado-api/compareenum.md) que indica la posición de fila relativa de dos registros representados por sus marcadores.  
  
#### <a name="parameters"></a>Parámetros  
 *Bookmark1*  
 Marcador de la primera fila.  
  
 *Bookmark2*  
 Marcador de la segunda fila.  
  
## <a name="remarks"></a>Observaciones  
 Los marcadores se deben aplicar al mismo objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) , a un objeto de conjunto de **registros** y a su [clonación](../../../ado/reference/ado-api/clone-method-ado.md). No puede comparar de forma confiable los marcadores de distintos objetos de **conjunto de registros** , aunque se hayan creado a partir del mismo origen o comando. Ni puede comparar marcadores para un objeto de **conjunto de registros** cuyo proveedor subyacente no admita comparaciones.  
  
 Un marcador identifica de forma única una fila en un objeto de **conjunto de registros** . Use la propiedad [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md) de la fila actual para obtener su marcador.  
  
 Dado que el tipo de datos de un marcador es específico de cada proveedor, ADO lo expone como **variante**. Por ejemplo, SQL Server marcadores son del tipo DBTYPE_R8 (**Double**). ADO expondría este tipo como una **variante** con un subtipo de **Double**.  
  
 Al comparar marcadores, ADO no intenta ningún tipo de coerción. Los valores simplemente se pasan al proveedor donde se produce la comparación. Si los marcadores pasados al método **CompareBookmarks** se almacenan en variables de tipos diferentes, puede generar el siguiente error de coincidencia de tipos: "los argumentos son del tipo incorrecto, están fuera del intervalo aceptable o están en conflicto entre sí".  
  
 Un marcador que no sea válido o que tenga un formato incorrecto producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método CompareBookmarks (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [Ejemplo del método CompareBookmarks (VC + +)](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark (propiedad) (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
