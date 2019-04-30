---
title: ActiveConnection (propiedad, ADO MD) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9a9ece5a7774ca2b718af90fe041c070fcc99bdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155901"
---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection (propiedad, ADO MD)
Indica a qué ADO [conexión](../../../ado/reference/ado-api/connection-object-ado.md) el conjunto de celdas de objeto o el catálogo al que pertenece actualmente.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** que contiene una cadena que define una conexión o **conexión** objeto. El valor predeterminado está vacío.  
  
## <a name="remarks"></a>Comentarios  
 Puede establecer esta propiedad para un ADO válido **conexión** objeto o en una cadena de conexión válida. Cuando esta propiedad se establece en una cadena de conexión, el proveedor crea un nuevo **conexión** utilizando esta definición de objeto y se abre la conexión.  
  
 Si usas el *ActiveConnection* argumento de la [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para abrir un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto, el **ActiveConnection** propiedad heredar el valor del argumento.  
  
 Establecer el **ActiveConnection** propiedad de un [catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) objeto **nada** libera los datos asociados, incluidos los datos en el [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) colección y los relacionados con [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md), y [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Cerrar un **conexión** objeto que se usó para abrir un **catálogo** tiene el mismo efecto que establecer el **ActiveConnection** propiedad **nada**.  
  
 Cambiar la base de datos predeterminada de la conexión al que hace referencia el **ActiveConnection** propiedad de un **catálogo** objeto invalida el contenido de la **catálogo**.  
  
 Se producirá un error si intenta cambiar el **ActiveConnection** propiedad para que uno abierto **Cellset** objeto.  
  
> [!NOTE]
>  En Visual Basic, recuerde que debe usar el **establecer** palabra clave al establecer el **ActiveConnection** propiedad a un **conexión** objeto. Si se omite el **establecer** palabra clave, en realidad se estableciendo el **ActiveConnection** propiedad igual a la **conexión** propiedad predeterminada del objeto,  **ConnectionString**. El código funcionará; Sin embargo, se creará una conexión adicional al origen de datos, lo que podría tener implicaciones de rendimiento negativo.  
  
 Cuando se usa el proveedor de datos MSOLAP, establezca el origen de datos en una cadena de conexión a un nombre de servidor y el catálogo inicial en el nombre de un catálogo desde el origen de datos. Para conectarse a un archivo de cubo que se desconecta un servidor, establezca la ubicación en la ruta de acceso completa a la. Archivos CUB. En cualquier caso, establezca el proveedor en el nombre del proveedor. Por ejemplo, la siguiente cadena usa el proveedor MSOLAP para conectarse a un catálogo denominado Bobs Video Store en un servidor denominado **Servername**:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de conjunto de celdas (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open (método) (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
