---
title: "Admite el método | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5b78cb1325b720207f6a18201971ef627314bfee
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="supports-method"></a>Método Supports
Determina si un determinado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto admite un tipo determinado de funcionalidad.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **booleano** valor que indica si todas las características de identifican por la *CursorOptions* argumento son compatibles con el proveedor.  
  
#### <a name="parameters"></a>Parámetros  
 *CursorOptions*  
 A **largo** expresión formada por uno o varios [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valores.  
  
## <a name="remarks"></a>Comentarios  
 Use la **admite** método para determinar qué tipos de funcionalidad de un **Recordset** objeto admite. Si el **Recordset** objeto admite las funcionalidades cuyas constantes correspondientes están en *CursorOptions*, el **admite** método **True**. De lo contrario, devuelve **False**.  
  
> [!NOTE]
>  Aunque la **admite** método puede devolver **True** para una funcionalidad determinada, no garantiza que el proveedor puede ofrecer la funcionalidad en todas las circunstancias. El **admite** método simplemente devuelve si el proveedor puede admitir la funcionalidad especificada, suponiendo que se cumplen ciertas condiciones. Por ejemplo, el **admite** método puede indicar que un **Recordset** objeto admita actualizaciones, aun cuando el cursor se basa en una combinación de varias tablas, algunas de las columnas no son actualizables.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Supports (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Ejemplo del método Supports (VC ++)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Propiedad CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
