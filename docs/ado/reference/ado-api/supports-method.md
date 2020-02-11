---
title: Admite el método | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936704"
---
# <a name="supports-method"></a>Método Supports
Determina si un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) especificado admite un tipo determinado de funcionalidad.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor **booleano** que indica si el proveedor admite todas las características identificadas por el argumento *CursorOptions* .  
  
#### <a name="parameters"></a>Parámetros  
 *CursorOptions*  
 Expresión **larga** que consta de uno o varios valores de [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 Use el método **Supports** para determinar los tipos de funcionalidad que admite un objeto de **conjunto de registros** . Si el objeto de **conjunto de registros** admite las características cuyas constantes correspondientes están en *CursorOptions*, el método **Supports** devuelve **true**. De lo contrario, devuelve **false**.  
  
> [!NOTE]
>  Aunque el método **Supports** puede devolver **true** para una funcionalidad determinada, no garantiza que el proveedor pueda hacer que la característica esté disponible en todas las circunstancias. El método **Supports** simplemente devuelve si el proveedor puede admitir la funcionalidad especificada, suponiendo que se cumplen ciertas condiciones. Por ejemplo, el método **Supports** puede indicar que un objeto de **conjunto de registros** admite actualizaciones aunque el cursor se base en una combinación de varias tablas, algunas columnas de las cuales no son actualizables.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Supports (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Ejemplo del método Supports (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propiedad CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
