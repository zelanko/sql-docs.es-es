---
title: Propiedad AbsolutePage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0da08a0c51c8d4d89329bbe9c36cacd7979c1e71
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747546"
---
# <a name="absolutepage-property-ado"></a>Propiedad AbsolutePage (ADO)
Indica en qué página reside el registro actual.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Para el código de 32 bits, establece o devuelve un valor **Long** de 1 al número de páginas del objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)) o devuelve uno de los valores de [PositionEnum](../../../ado/reference/ado-api/positionenum.md) .  
  
 Para el código de 64 bits, use un tipo de datos que proporcione para el almacenamiento de un valor de 64 bits. Por ejemplo, puede usar un valor **Long** u otro que puede tener una longitud de 64 bits como DBORDINAL. No use valores **PositionEnum** porque están limitados a una longitud de 32 bits.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se puede utilizar para identificar el número de página en el que se encuentra el registro actual. Usa la propiedad [pageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) para dividir lógicamente el número total de conjuntos de filas del objeto de **conjunto de registros** en una serie de páginas, cada una de las cuales tiene el número de registros igual a **pageSize** (excepto en la última página, que puede tener menos registros). El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
-   Al obtener o establecer la propiedad **AbsolutePage** , ADO utiliza la propiedad [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) y la propiedad [pageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) conjuntamente de la siguiente manera:  
  
-   Para obtener el **AbsolutePage**, ADO primero recupera el **AbsolutePosition**y, a continuación, lo divide por el **pageSize**.  
  
-   Para establecer el valor de **AbsolutePage**, ADO mueve el valor de **AbsolutePosition** de la manera siguiente: multiplica el valor de **pageSize** por el nuevo valor de **AbsolutePage** y, a continuación, agrega 1 al valor. Como resultado, la posición actual del conjunto de **registros** después de establecer correctamente **AbsolutePage** es el primer registro de la página.  
  
 Al igual que la propiedad **AbsolutePosition** , **AbsolutePage** es de base 1 y es igual a 1 cuando el registro actual es el primer registro del **conjunto de registros**. Establezca esta propiedad para pasar al primer registro de una página determinada. Obtenga el número total de páginas de la propiedad **PageCount** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedades AbsolutePage, PageCount y PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Ejemplo de propiedades AbsolutePage, PageCount y PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition (propiedad, ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount (propiedad, ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Propiedad PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
