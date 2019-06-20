---
title: Propiedad AbsolutePosition (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 467834d2cfd5e56c14d9c7565d6749fa6848251e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718346"
---
# <a name="absoluteposition-property-ado"></a>Propiedad AbsolutePosition (ADO)
Indica la posición ordinal de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) registro actual del objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Para el código de 32 bits, Establece o devuelve un **largo** valor entre 1 y el número de registros en el **Recordset** objeto ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), o devuelve uno de los [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para el código de 64 bits, utilice un tipo de datos que proporciona para el almacenamiento de un valor de 64 bits. Por ejemplo, podría utilizar prolongada u otro valor que es la longitud de 64 bits como DBORDINAL. No use **PositionEnum** valores desde que se limitan a la longitud de 32 bits.  
  
## <a name="remarks"></a>Comentarios  
 Para establecer el **AbsolutePosition** propiedad, ADO requiere que implemente el proveedor OLE DB que usa el [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) interfaz.  
  
 Obtener acceso a la **AbsolutePosition** propiedad de un **Recordset** que se abrió con cualquiera de solo avance o un cursor dinámico genera el error **adErrFeatureNotAvailable**. Con otros tipos de cursor, se devolverá la posición correcta siempre que el proveedor OLE DB admite la **IRowsetScroll:IRowsetLocate** interfaz. Si el proveedor no admite la **IRowsetScroll** interfaz, la propiedad se establece en **adPosUnknown**. Consulte la documentación de su proveedor para determinar si éste admite **IRowsetScroll**.  
  
 Use la **AbsolutePosition** propiedad que se va a mover a un registro según su posición ordinal en la **Recordset** objeto, o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para esta propiedad esté disponible.  
  
 Al igual que el [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedad, **AbsolutePosition** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro en el **Recordset**. Puede obtener el número total de registros en el **Recordset** objeto desde el [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad.  
  
 Al establecer el **AbsolutePosition** propiedad, incluso si se van a un registro en la memoria caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros empezando por el registro especificado. El [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad determina el tamaño de este grupo.  
  
> [!NOTE]
>  No se debe usar el **AbsolutePosition** propiedad como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. También no hay ninguna garantía de que un registro determinado tendrá el mismo **AbsolutePosition** si el **Recordset** objeto se vuelve a consultar o se vuelve a abrir. Los marcadores siguen siendo la forma recomendada de retener y volver a una posición determinada y son la única manera de posicionamiento en todos los tipos de **Recordset** objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo AbsolutePosition y CursorLocation propiedades (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Ejemplo AbsolutePosition y CursorLocation propiedades (VC ++)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
