---
title: Grabar (objeto) (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26840ff89f61bc3c37cee2fd88c1f53e393528bf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="record-object-ado"></a>Objeto de registro (ADO)
Representa una fila de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o el proveedor de datos o un objeto devuelto por un proveedor de datos semiestructurados, como un archivo o directorio.  
  
## <a name="remarks"></a>Comentarios  
 A **registro** objeto representa una fila de datos y tiene algunas semejanzas conceptuales con una fila **conjunto de registros**. Dependiendo de las capacidades del proveedor, **registro** objetos pueden devolverse directamente desde dicho proveedor en lugar de una fila **Recordset**, por ejemplo, cuando una consulta SQL que selecciona solo una fila es ejecutar. O, una **registro** se puede obtener el objeto directamente desde un **Recordset** objeto. O, una **registro** puede devolverse directamente desde un proveedor de datos semiestructurados, como el proveedor OLE DB de Microsoft Exchange.  
  
 Puede ver los campos asociados a la **registro** objeto por medio de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección en la **registro** objeto. ADO permite columnas con valores de objeto como **Recordset**, **SafeArray**y valores escalares en el **campos** colección de **registro** objetos.  
  
 Si el **registro** objeto representa una fila en un **Recordset**, es posible volver a ese original **conjunto de registros** con el [origen](../../../ado/reference/ado-api/source-property-ado-record.md) propiedad.  
  
 El **registro** objeto también puede ser utilizado por los proveedores de datos semiestructurados como el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)para espacios de nombres con estructura de árbol del modelo. Cada nodo en el árbol es un **registro** objeto con las columnas asociadas. Las columnas pueden representar los atributos de ese nodo y otra información relevante. El **registro** objeto puede representar tanto un nodo hoja como un nodo en la estructura de árbol. Los nodos no hoja tienen otros nodos como su contenido, pero los nodos hoja no tienen dicho contenido. Los nodos hoja contienen normalmente secuencias binarias de datos y los nodos no hoja también pueden tener una secuencia binaria predeterminada asociada a ellos. Propiedades de la **registro** objeto de identificar el tipo del nodo.  
  
 El **registro** objeto también representa un medio alternativo para desplazarse jerárquicamente datos organizados. A **registro** objeto puede ser creado para representar la raíz de un subárbol específico en una estructura de árbol de gran tamaño y nuevos **registro** objetos se pueden abrir para representar nodos secundarios.  
  
 Un recurso (por ejemplo, un archivo o directorio) puede identificarse de forma exclusiva por una dirección URL absoluta. A [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto se crea implícitamente y se establece en el **registro** objeto cuando la **registro** se abre mediante una dirección URL absoluta. A **conexión** objeto puede establecerse explícitamente en el **registro** objeto a través de la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad. Los archivos y directorios que se pueden tener acceso mediante el uso de la **conexión** objeto definir la *contexto* en el que **registro** pueden producirse operaciones.  
  
 Métodos de navegación y modificación de datos en el **registro** objeto también acepta una dirección URL relativa, que localiza un recurso mediante una dirección URL absoluta o **conexión** contexto del objeto como punto de partida.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 A **conexión** está asociado a cada objeto **registro** objeto. Por lo tanto, **registro** las operaciones de objeto pueden formar parte de una transacción mediante la invocación de **conexión** métodos de transacción del objeto.  
  
 El **registro** objeto no admite eventos de ADO y, por tanto, no responderá a las notificaciones.  
  
 Con los métodos y propiedades de un **registro** objeto, puede hacer lo siguiente:  
  
-   Establecer o devolver asociado **conexión** objeto con el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
-   Indicar permisos de acceso con el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad.  
  
-   Devolver la dirección URL del directorio, si procede, que contiene el recurso representado por la **registro** con el [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propiedad.  
  
-   Indicar la dirección URL absoluta, la dirección URL relativa, o **Recordset** desde el que el **registro** procede con la [origen](../../../ado/reference/ado-api/source-property-ado-record.md) propiedad.  
  
-   Indicar el estado actual de la **registro** con el [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad.  
  
-   Indicar el tipo de **registro** : *simple*, *colección*, o *documentos estructurados* : con la [Tiporegistro](../../../ado/reference/ado-api/recordtype-property-ado.md)propiedad.  
  
-   Detener la ejecución de una operación asincrónica con el [cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Desasociar la **registro** desde un origen de datos con la [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Copie el archivo o directorio representado por un **registro** a otra ubicación con el [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
-   Eliminar el archivo o directorio y subdirectorios, representado por un **registro** con el [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) método.  
  
-   Abrir un **Recordset** que contiene las filas que representen los subdirectorios y archivos de la entidad representada por la **registro** con el [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) método.  
  
-   Mover (cambiar el nombre) el archivo o directorio y subdirectorios, representados por un **registro** a otra ubicación con el [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
-   Asociar el **registro** con los datos existentes de origen, o crear un nuevo archivo o directorio con el [abiertos](../../../ado/reference/ado-api/open-method-ado-record.md) método.  
  
 El **registro** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades de objeto de registro](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Registros y secuencias](../../../ado/guide/data/records-and-streams.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

