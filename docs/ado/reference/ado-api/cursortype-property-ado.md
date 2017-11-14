---
title: Propiedad CursorType (ADO) | Documentos de Microsoft
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
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7031dc9b7acd89eea8491837ec4a550f34dc1ef
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cursortype-property-ado"></a>Propiedad CursorType (ADO)
Indica el tipo de cursor que se utiliza en una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor. El valor predeterminado es **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CursorType** propiedad para especificar el tipo de cursor que se debe usar al abrir el **Recordset** objeto.  
  
 Solo un valor de **adOpenStatic** se admite si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**. Si se establece un valor no admitido, no se producirá ningún error; admite la más parecida **CursorType** se utilizará en su lugar.  
  
 Si un proveedor no admite el tipo de cursor solicitado, puede devolver otro tipo de cursor. El **CursorType** propiedad cambiarán para coincidir con el tipo de cursor real en uso cuando el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto está abierto. Para comprobar la funcionalidad específica del cursor devuelto, utilice el [admite](../../../ado/reference/ado-api/supports-method.md) método. Después de cerrar la **Recordset**, **CursorType** propiedad revierte a su valor original.  
  
 El gráfico siguiente muestra la funcionalidad de proveedor (identificada por **admite** constantes del método) necesaria para cada tipo de cursor.  
  
|Para un conjunto de registros de este CursorType|El método Supports debe devolver True para todas estas constantes|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Aunque **admite**(**adUpdateBatch**) puede ser true para los cursores dinámicos y de solo avance, acerca de las actualizaciones por lotes se debe utilizar un conjunto de claves o un cursor estático. Establecer el [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) propiedad a **adLockBatchOptimistic** y **CursorLocation** propiedad **adUseClient** para habilitar el Cursor Servicio de OLE DB, que es necesario para las actualizaciones por lotes.  
  
 El **CursorType** propiedad es de lectura y escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **Recordset** objeto, el **CursorType** propiedad se puede establecer solo en **adOpenStatic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)

