---
title: Propiedad ActiveConnection (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae0b32385b98ac1b48688a7f89bbd7c91842a106
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67911597"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection (propiedad, ADO MD)
Indica a qué objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) ADO pertenece actualmente el objeto Cellset o el catálogo actual.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **valor de tipo Variant** que contiene una cadena que define una conexión o un objeto de **conexión** . El valor predeterminado es vacío.  
  
## <a name="remarks"></a>Observaciones  
 Puede establecer esta propiedad en un objeto de **conexión** ADO válido o en una cadena de conexión válida. Cuando esta propiedad se establece en una cadena de conexión, el proveedor crea un nuevo objeto de **conexión** con esta definición y abre la conexión.  
  
 Si usa el argumento *ActiveConnection* del método [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) para abrir un objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) , la propiedad **ActiveConnection** heredará el valor del argumento.  
  
 Al establecer la propiedad **ActiveConnection** de un objeto de [Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) en **Nothing** , se liberan los datos asociados, incluidos los datos de la colección [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) y los objetos de [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md)y [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) relacionados. Cerrar un objeto de **conexión** que se usó para abrir un **Catálogo** tiene el mismo efecto que establecer la propiedad **ActiveConnection** en **Nothing**.  
  
 Al cambiar la base de datos predeterminada de la conexión a la que hace referencia la propiedad **ActiveConnection** de un objeto de **Catálogo** , se invalida el contenido del **Catálogo**.  
  
 Se producirá un error si intenta cambiar la propiedad **ActiveConnection** para un objeto **Cellset** abierto.  
  
> [!NOTE]
>  En Visual Basic, recuerde usar la palabra clave **set** al establecer la propiedad **ActiveConnection** en un objeto **Connection** . Si se omite la palabra clave **set** , se establecerá realmente la propiedad **ActiveConnection** en la propiedad predeterminada del objeto de **conexión** , **ConnectionString**. El código funcionará; sin embargo, creará una conexión adicional con el origen de datos, que puede tener implicaciones de rendimiento negativas.  
  
 Al usar el proveedor de datos MSOLAP, establezca el origen de datos de una cadena de conexión en un nombre de servidor y establezca el catálogo inicial en el nombre de un catálogo desde el origen de datos. Para conectarse a un archivo de cubo que está desconectado de un servidor, establezca la ubicación en la ruta de acceso completa a. Archivo CUB. En cualquier caso, establezca el proveedor en el nombre del proveedor. Por ejemplo, la cadena siguiente usa el proveedor MSOLAP para conectarse a un catálogo denominado bobs Video Store en un servidor denominado **ServerName**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 La cadena siguiente se conecta a un archivo de cubo local en la ubicación C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
```  
"Location=C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub;Provider=msolap"  
```  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Connection (objeto) (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open (método) (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
