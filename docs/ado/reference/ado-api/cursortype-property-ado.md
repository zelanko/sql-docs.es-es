---
title: Propiedad CursorType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fb037216c851a869cb19013a37fccd48145f284
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789683"
---
# <a name="cursortype-property-ado"></a>Propiedad CursorType (ADO)
Indica el tipo de cursor utilizado en un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) valor. El valor predeterminado es **adOpenForwardOnly**.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CursorType** propiedad para especificar el tipo de cursor que se debe usar al abrir el **Recordset** objeto.  
  
 Solo un valor de **adOpenStatic** se admite si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**. Si se establece un valor no admitido, se producirá ningún error; admite la más cercana **CursorType** se usará en su lugar.  
  
 Si un proveedor no admite el tipo de cursor solicitado, puede devolver otro tipo de cursor. El **CursorType** propiedad cambiará para coincidir con el tipo de cursor actual en uso cuando la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto está abierto. Para comprobar la funcionalidad específica del cursor devuelto, use el [admite](../../../ado/reference/ado-api/supports-method.md) método. Después de cerrar el **Recordset**, **CursorType** propiedad revierte a su valor original.  
  
 El gráfico siguiente muestra la funcionalidad de proveedor (identificado por **admite** constantes del método) necesarios para cada tipo de cursor.  
  
|Para un conjunto de registros de este CursorType|El método Supports debe devolver True para todas estas constantes|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**, **adHoldRecords**, **adMovePrevious**, **adResync**|  
  
> [!NOTE]
>  Aunque **admite**(**adUpdateBatch**) puede ser true para los cursores dinámicos y de solo avance, para las actualizaciones por lotes se debe usar un conjunto de claves o un cursor estático. Establecer el [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) propiedad **adLockBatchOptimistic** y el **CursorLocation** propiedad **adUseClient** para habilitar el Cursor Servicio de OLE DB, que es necesario para las actualizaciones por lotes.  
  
 El **CursorType** propiedad es de lectura/escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **Recordset** objeto, el **CursorType** propiedad se puede establecer solo en **adOpenStatic**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [CursorType, LockType y ejemplo de las propiedades EditMode (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType, LockType y ejemplo de las propiedades EditMode (VC ++)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Método Supports](../../../ado/reference/ado-api/supports-method.md)
