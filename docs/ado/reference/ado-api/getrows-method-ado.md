---
title: Ejemplo del método GetRows (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetRows
- Recordset15::raw_GetRows
helpviewer_keywords:
- Getrows method [ADO]
ms.assetid: 14b92860-4171-47d9-a413-dd60dd6a8880
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65d346cb9394613a92f95f7466e429b10c54b1a8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616973"
---
# <a name="getrows-method-ado"></a>Método GetRows (ADO)
Recupera varios registros de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto en una matriz.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
array = recordset.GetRows(Rows, Start, Fields )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **Variant** cuyo valor es una matriz bidimensional.  
  
#### <a name="parameters"></a>Parámetros  
 *Filas*  
 Opcional. Un [GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md) valor que indica el número de registros para recuperar. El valor predeterminado es **adGetRowsRest**.  
  
 *Inicio*  
 Opcional. Un **cadena** valor o **Variant** que se evalúa como el marcador para el registro desde el que el **GetRows** debe comenzar la operación. También puede usar un [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valor.  
  
 *Fields*  
 Opcional. Un **Variant** que representa un nombre de campo único o la posición ordinal o una matriz de nombres de campo o números de posición ordinal. ADO devuelve sólo los datos en estos campos.  
  
## <a name="remarks"></a>Comentarios  
 Use la **GetRows** método para copiar registros de un **Recordset** en una matriz bidimensional. El primer subíndice identifica el campo y el segundo el número de registro. El *matriz* variable se ajusta automáticamente para el valor correcto de tamaño cuando el **GetRows** método devuelve los datos.  
  
 Si no especifica un valor para el *filas* argumento, el **GetRows** método recupera automáticamente todos los registros de la **Recordset** objeto. Si se solicita más registros que están disponibles, **GetRows** devuelve solo el número de registros disponibles.  
  
 Si el **Recordset** objeto admite marcadores, puede especificar en qué registro el **GetRows** método debería empezar a recuperar datos pasando el valor de ese registro [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md)propiedad en el *iniciar* argumento.  
  
 Si desea restringir los campos que el **GetRows** devuelve la llamada, puede pasar un nombre o número de campo único o una matriz de números y nombres de campo en el *campos* argumento.  
  
 Después de llamar a **GetRows**, el siguiente registro sin leer se convierte en el registro actual, o la [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedad está establecida en **True** si no hay más registros.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método GetRows (VB)](../../../ado/reference/ado-api/getrows-method-example-vb.md)   
 [Ejemplo del método GetRows (VC ++)](../../../ado/reference/ado-api/getrows-method-example-vc.md)   
