---
title: Cambiar la forma de nombre de propiedad dinámica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a07ec878b1198fbf23bfb251460d83869313c83
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696834"
---
# <a name="reshape-name-property-dynamic-ado"></a>Propiedad dinámica Reshape Name (ADO)
Especifica un nombre para el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **cadena** valor que es el nombre de la **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Los nombres se conservan para la duración de la conexión o hasta que el **Recordset** está cerrado.  
  
 El **Reshape Name** propiedad sirve principalmente para su uso con la característica de cambio de forma de la [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) proveedor de servicios. Los nombres deben ser únicos para participar en volver a dar forma a.  
  
 Esta propiedad es de solo lectura, pero se puede establecer indirectamente cuando un **Recordset** se crea. Por ejemplo, si una cláusula de un comando Shape crea un **Recordset** y le da un nombre de alias mediante el uso de la **AS** palabra clave, el alias se asigna a la **Reshape Name** propiedad. Si no se declara ningún alias, el **Reshape Name** propiedad se asigna un nombre único generado por el servicio de la forma de datos. Si el nombre de alias es el mismo que el nombre de un miembro de **Recordset**, ni **Recordset** puede cambiarse hasta que se libere una de ellas. El comportamiento predeterminado se puede cambiar estableciendo un nombre único la [Reshape Name](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) propiedad en la conexión de ADO a **True**. Al establecer esta propiedad proporciona el permiso de servicio para cambiar el nombre de usuario asignado, si es necesario, para garantizar la unicidad de la forma de datos. Para obtener más información acerca de nuevas formas, consulte [servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios de ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Use la **Reshape Name** propiedad cuando desea hacer referencia a un **Recordset** en un comando de forma, o cuando no conoce el nombre debido a que se ha generado por el servicio de datos de forma. En ese caso, es posible generar un comando de forma al concatenar el comando con la cadena devuelta por la **Reshape Name** propiedad.  
  
 **Cambiar la forma de nombre** se anexa una propiedad dinámica a la **Recordset** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Servicio de OLE DB (proveedor de servicios de ADO) de la forma de datos de Microsoft](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
