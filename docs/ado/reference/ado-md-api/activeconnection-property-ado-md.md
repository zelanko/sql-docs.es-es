---
title: ActiveConnection (propiedad, ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ActiveConnection
- Cellset::ActiveConnection
- Catalog::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO MD]
ms.assetid: 2509b32c-a995-4364-9152-d8c83129bdd8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae0ad910a0535599d7e134d3314030537068ab25
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="activeconnection-property-ado-md"></a>ActiveConnection (propiedad, ADO MD)
Indica a qué ADO [conexión](../../../ado/reference/ado-api/connection-object-ado.md) el conjunto de celdas actual de un objeto o catálogo al que pertenece actualmente.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **Variant** que contiene una cadena que define una conexión o **conexión** objeto. El valor predeterminado está vacío.  
  
## <a name="remarks"></a>Comentarios  
 Puede establecer esta propiedad en un ADO válido **conexión** objeto o en una cadena de conexión válida. Cuando esta propiedad se establece en una cadena de conexión, el proveedor crea un nuevo **conexión** objeto mediante esta definición y abre la conexión.  
  
 Si usas el *ActiveConnection* argumento de la [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para abrir un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto, el **ActiveConnection** propiedad heredar el valor del argumento.  
  
 Establecer el **ActiveConnection** propiedad de un [catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md) el objeto a **nada** libera los datos asociados, incluidos los datos en el [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) colección y los relacionados con [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md), [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md), [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md), y [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Cerrar un **conexión** objeto que se usó para abrir un **catálogo** tiene el mismo efecto que establecer la **ActiveConnection** propiedad **nada**.  
  
 Cambiar la base de datos predeterminada de la conexión al que hace referencia el **ActiveConnection** propiedad de un **catálogo** objeto invalida el contenido de la **catálogo**.  
  
 Se producirá un error si intenta cambiar el **ActiveConnection** propiedad abierto **Cellset** objeto.  
  
> [!NOTE]
>  En Visual Basic, recuerde que debe usar el **establecer** palabra clave al establecer el **ActiveConnection** propiedad a una **conexión** objeto. Si se omite la **establecer** palabra clave, en realidad estará estableciendo la **ActiveConnection** propiedad igual a la **conexión** propiedad predeterminada del objeto, ** ConnectionString**. El código funcionará; Sin embargo, se creará una conexión adicional al origen de datos, lo que puede tener implicaciones de rendimiento negativo.  
  
 Cuando se utiliza el proveedor de datos MSOLAP, establezca el origen de datos en una cadena de conexión a un nombre de servidor y el catálogo inicial para el nombre de un catálogo de desde el origen de datos. Para conectarse a un archivo de cubo que esté desconectado de un servidor, establezca la ubicación en la ruta de acceso completa a la. Archivos CUB. En cualquier caso, establezca el proveedor en el nombre del proveedor. Por ejemplo, la cadena siguiente usa el proveedor MSOLAP para conectarse a un catálogo denominado almacén de vídeo del equipo en un servidor denominado **Servername**:  
  
```  
"Data Source=Servername;Initial Catalog=Bobs Video Store;Provider=msolap"  
```  
  
 La siguiente cadena se conecta a un archivo de cubo local en la ubicación C:\MSDASDK\samples\oledb\olap\data\bobsvid.cub:  
  
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
