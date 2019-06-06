---
title: Registrar el objeto (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 859bf3f53051a500e86742cb681885b8067f6a0c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712217"
---
# <a name="record-object-ado"></a>Objeto Record (ADO)
Representa una fila de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o el proveedor de datos o un objeto devuelto por un proveedor de datos semiestructurados, como un archivo o directorio.  
  
## <a name="remarks"></a>Comentarios  
 Un **registro** objeto representa una fila de datos y presenta algunas similitudes con una fila conceptuales **Recordset**. Dependiendo de las capacidades del proveedor, **registro** objetos pueden devolverse directamente desde el proveedor en lugar de una fila **Recordset**, por ejemplo, cuando una consulta SQL que selecciona una única fila es ejecuta. O, un **registro** puede obtenerse un objeto directamente desde un **Recordset** objeto. O, un **registro** pueden devolverse directamente desde un proveedor de datos semiestructurados, como el proveedor OLE DB de Microsoft Exchange.  
  
 Puede ver los campos asociados con el **registro** objeto por medio de la [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección en el **registro** objeto. ADO permite columnas con valores de objeto como **Recordset**, **SafeArray**y valores escalares en el **campos** colección de **registro** objetos.  
  
 Si el **registro** objeto representa una fila en un **Recordset**, es posible volver a ese original **Recordset** con el [origen](../../../ado/reference/ado-api/source-property-ado-record.md) propiedad.  
  
 El **registro** objeto también se puede usar proveedores de datos semiestructurados, como el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), para modelar la estructura de árbol de espacios de nombres. Cada nodo del árbol es un **registro** objeto con las columnas asociadas. Las columnas pueden representar los atributos de ese nodo y otra información relevante. El **registro** objeto puede representar un nodo hoja y un nodo de la estructura de árbol. No hoja tienen otros nodos como su contenido, pero los nodos hoja no tienen dicho contenido. Normalmente, los nodos hoja contienen secuencias binarias de datos y los nodos no hoja también pueden tener una secuencia binaria predeterminada asociada con ellos. Las propiedades de la **registro** objeto de identificar el tipo de nodo.  
  
 El **registro** objeto también representa un medio alternativo para navegar de forma jerárquica organiza los datos. Un **registro** objeto puede ser creado para representar la raíz de un subárbol específico en una estructura de árbol de gran tamaño y nuevos **registro** objetos se pueden abrir para representar nodos secundarios.  
  
 Un recurso (por ejemplo, un archivo o directorio) puede identificarse de forma exclusiva por una dirección URL absoluta. Un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto se crea implícitamente y se establece en el **registro** objeto cuando la **registro** se abre mediante una dirección URL absoluta. Un **conexión** objeto puede establecerse explícitamente en el **registro** objeto a través de la [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad. Los archivos y directorios que se pueden acceder mediante el uso de la **conexión** definen el objeto de la *contexto* en el que **registro** pueden producirse operaciones.  
  
 Métodos de navegación y modificación de datos en el **registro** objeto también aceptan una dirección URL relativa que busca un recurso mediante una dirección URL absoluta o **conexión** contexto del objeto como un punto de partida.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
 Un **conexión** está asociado con cada objeto **registro** objeto. Por lo tanto, **registro** las operaciones de objeto pueden ser parte de una transacción mediante la invocación **conexión** objeto métodos de transacción.  
  
 El **registro** objeto no admite eventos de ADO y, por lo tanto, no responderá a las notificaciones.  
  
 Con los métodos y propiedades de un **registro** objeto, puede hacer lo siguiente:  
  
-   Establecer o devolver asociado **conexión** objeto con el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad.  
  
-   Indicar los permisos de acceso con el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad.  
  
-   Devolver la dirección URL del directorio, si procede, que contiene el recurso representado por la **registro** con el [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propiedad.  
  
-   Indicar la dirección URL absoluta, la dirección URL relativa, o **Recordset** desde el que el **registro** procede con la [origen](../../../ado/reference/ado-api/source-property-ado-record.md) propiedad.  
  
-   Indicar el estado actual de la **registro** con el [estado](../../../ado/reference/ado-api/state-property-ado.md) propiedad.  
  
-   Indicar el tipo de **registro** - *simple*, *colección*, o *documentos estructurados* : con la [ RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)propiedad.  
  
-   Detener la ejecución de una operación asincrónica con el [cancelar](../../../ado/reference/ado-api/cancel-method-ado.md) método.  
  
-   Desasocie el **registro** desde un origen de datos con el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método.  
  
-   Copie el archivo o directorio representado por un **registro** a otra ubicación con el [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
-   Eliminar el archivo o directorio y subdirectorios, representado por un **registro** con el [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md) método.  
  
-   Abra un **Recordset** que contiene las filas que representan los subdirectorios y archivos de la entidad representada por el **registro** con el [GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md) método.  
  
-   Mover (cambiar nombre) del archivo, o directorio y subdirectorios, representado por un **registro** a otra ubicación con el [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md) método.  
  
-   Asociar el **registro** con los datos existentes de origen, o crear un nuevo archivo o directorio con el [abierto](../../../ado/reference/ado-api/open-method-ado-record.md) método.  
  
 El **registro** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Record](../../../ado/reference/ado-api/record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Colección de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Registros y secuencias](../../../ado/guide/data/records-and-streams.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
