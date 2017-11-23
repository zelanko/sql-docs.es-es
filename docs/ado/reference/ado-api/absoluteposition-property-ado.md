---
title: Propiedad AbsolutePosition (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::AbsolutePosition
helpviewer_keywords: AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 491ed39340dd066955db2fd73ed986614744cff4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="absoluteposition-property-ado"></a>Propiedad AbsolutePosition (ADO)
Indica la posición ordinal de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) registro actual del objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Para código de 32 bits, Establece o devuelve un **largo** valor entre 1 y el número de registros en el **Recordset** objeto ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), o devuelve uno de los [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) valores.  
  
 Para código de 64 bits, use un tipo de datos que proporciona para el almacenamiento de un valor de 64 bits. Por ejemplo, podría utilizar larga u otro valor que es la longitud de 64 bits como DBORDINAL. No utilice **PositionEnum** valores desde que se limitan a la longitud de 32 bits.  
  
## <a name="remarks"></a>Comentarios  
 Para establecer el **AbsolutePosition** propiedad, ADO requiere que implementen el proveedor OLE DB que usa el [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) interfaz.  
  
 Obtener acceso a la **AbsolutePosition** propiedad de un **Recordset** que se abrió con cualquiera de solo avance o cursor dinámico genera el error **adErrFeatureNotAvailable**. Con otros tipos de cursor, se devolverá la posición correcta siempre que el proveedor OLE DB admite la **IRowsetScroll:IRowsetLocate** interfaz. Si el proveedor no admite la **IRowsetScroll** interfaz, la propiedad se establece en **adPosUnknown**. Consulte la documentación de su proveedor para determinar si éste admite **IRowsetScroll**.  
  
 Use la **AbsolutePosition** propiedad que se va a mover a un registro basándose en su posición ordinal en la **Recordset** objeto, o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 Al igual que el [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) propiedad, **AbsolutePosition** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro de la **conjunto de registros**. Puede obtener el número total de registros en la **Recordset** objeto desde el [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) propiedad.  
  
 Al establecer el **AbsolutePosition** propiedad, incluso si es a un registro en la memoria caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros empezando por el registro especificado. El [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad determina el tamaño de este grupo.  
  
> [!NOTE]
>  No debe utilizar el **AbsolutePosition** propiedad como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. También no hay ninguna garantía de que un registro determinado tenga el mismo **AbsolutePosition** si la **Recordset** objeto se realiza una nueva consulta o se vuelve a abrir. Los marcadores siguen siendo la forma recomendada de conservar y volver a una posición determinada y son la única manera de ubicarse a través de todos los tipos de **Recordset** objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo AbsolutePosition y CursorLocation propiedades (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Ejemplo AbsolutePosition y CursorLocation propiedades (VC ++)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Propiedad AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Propiedad RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
