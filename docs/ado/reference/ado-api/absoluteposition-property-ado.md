---
title: AbsolutePosition (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b9795f962d0ead59a8d4f993e799a0ae4e2b750
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921694"
---
# <a name="absoluteposition-property-ado"></a>Propiedad AbsolutePosition (ADO)
Indica la posición ordinal del registro actual de un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Para el código de 32 bits, establece o devuelve un valor **Long** de 1 al número de registros en el objeto de **conjunto de registros** ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)) o devuelve uno de los valores de [PositionEnum](../../../ado/reference/ado-api/positionenum.md) .  
  
 Para el código de 64 bits, use un tipo de datos que proporcione para el almacenamiento de un valor de 64 bits. Por ejemplo, puede usar un valor Long u otro que tenga una longitud de 64 bits como DBORDINAL. No use valores **PositionEnum** , ya que están limitados a una longitud de 32 bits.  
  
## <a name="remarks"></a>Observaciones  
 Para establecer la propiedad **AbsolutePosition** , ADO requiere que el OLE DB proveedor que está usando implemente la interfaz [IRowsetLocate: IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) .  
  
 El acceso a la propiedad **AbsolutePosition** de un **conjunto de registros** que se abrió con un cursor de solo avance o dinámico genera el error **adErrFeatureNotAvailable**. Con otros tipos de cursor, se devolverá la posición correcta siempre que el proveedor de OLE DB admita la interfaz **IRowsetScroll: IRowsetLocate** . Si el proveedor no admite la interfaz **IRowsetScroll** , la propiedad se establece en **adPosUnknown**. Consulte la documentación del proveedor para determinar si admite **IRowsetScroll**.  
  
 Use la propiedad **AbsolutePosition** para desplace un registro basándose en su posición ordinal en el objeto de **conjunto de registros** o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 Al igual que la propiedad [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) , **AbsolutePosition** es de base 1 y es igual a 1 cuando el registro actual es el primer registro del **conjunto de registros**. Puede obtener el número total de registros en el objeto de **conjunto de registros** de la propiedad [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) .  
  
 Cuando se establece la propiedad **AbsolutePosition** , incluso si se trata de un registro en la caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros a partir del registro especificado. La propiedad [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) determina el tamaño de este grupo.  
  
> [!NOTE]
>  No debe utilizar la propiedad **AbsolutePosition** como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. Tampoco existe la garantía de que un registro determinado tendrá el mismo **AbsolutePosition** si el objeto de **conjunto de registros** se reconsulta o se vuelve a abrir. Los marcadores siguen siendo la forma recomendada de conservar y volver a una posición determinada y son la única forma de colocar en todos los tipos de objetos de **conjunto de registros** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades AbsolutePosition y CursorLocation (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Ejemplo de las propiedades AbsolutePosition y CursorLocation (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
