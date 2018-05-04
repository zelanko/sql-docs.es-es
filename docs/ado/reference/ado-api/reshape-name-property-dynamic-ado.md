---
title: Cambiar la forma de nombre de propiedad dinámica (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Reshape Name property [ADO]
ms.assetid: 690229d1-46cc-42e6-a57d-4438251fe248
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3e4509aa15755839c9b199427a9026d86dbf8d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="reshape-name-property-dynamic-ado"></a>Cambiar la forma de nombre de propiedad dinámica (ADO)
Especifica un nombre para el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **cadena** valor que es el nombre de la **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 Los nombres se conservan para la duración de la conexión o hasta que el **Recordset** está cerrado.  
  
 El **cambiar la forma de nombre** propiedad sirve principalmente para su uso con la característica de volver a catalogar el [servicio de forma de datos de Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) proveedor de servicios. Nombres deben ser únicos para participar en volver a dar forma.  
  
 Esta propiedad es de solo lectura, pero se puede establecer indirectamente cuando un **Recordset** se crea. Por ejemplo, si una cláusula de un comando Shape crea un **Recordset** y le da un nombre de alias mediante el uso de la **AS** palabra clave, el alias se asigna a la **cambiar la forma de nombre** propiedad. Si no se declara ningún alias, la **cambiar la forma de nombre** propiedad se asigna un nombre único generado por el servicio de forma de datos. Si el nombre de alias es el mismo que el nombre de un miembro de **Recordset**, ni **Recordset** puede cambiarse hasta que uno de ellos se libera. El comportamiento predeterminado se puede cambiar estableciendo un nombre único el [cambiar la forma de nombre](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md) propiedad en la conexión de ADO para **True**. Establecer esta propiedad proporciona el permiso de servicio para cambiar el nombre de usuario asignado, si es necesario, para garantizar la unicidad de la forma de datos. Para obtener más información acerca de cómo cambiar la forma de, consulte [servicio de forma de datos de Microsoft para OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md).  
  
 Use la **cambiar la forma de nombre** propiedad cuando desea hacer referencia a un **Recordset** en un comando Shape o cuando no conozca el nombre debido a fue generado por el servicio de forma de datos. En ese caso, es posible generar un comando SHAPE al concatenar el comando con la cadena devuelta por la **cambiar la forma de nombre** propiedad.  
  
 **Cambiar la forma de nombre** es una propiedad dinámica que se anexa a la **Recordset** del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección cuando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Datos de Microsoft para dar forma al servicio para OLE DB (proveedor de servicios ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
