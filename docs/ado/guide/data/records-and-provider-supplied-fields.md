---
title: Registros y campos proporcionados por el proveedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3eb100042c36d86d604d48e716023dc0c0c4b04c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679973"
---
# <a name="records-and-provider-supplied-fields"></a>Registros y campos proporcionados por el proveedor
Cuando un [registro](../../../ado/reference/ado-api/record-object-ado.md) se abre el objeto, su origen puede ser la fila actual de una abierta [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), una dirección URL absoluta o una dirección URL relativa junto con una apertura [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto .  
  
 Si el **registro** se abre desde una **Recordset**, el **registro** objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección contendrá todos los campos de la  **Conjunto de registros**, además de los campos agregados por el proveedor subyacente.  
  
 El proveedor puede insertar campos adicionales que sirven de características adicionales de la **registro**. Como resultado, un **registro** puede tener campos únicos no en el **Recordset** como un todo o cualquier **registro** deriva de otra fila de la **Recordset**.  
  
 Por ejemplo, todas las filas de una **Recordset** derivado de correo electrónico en una origen de datos puede tener columnas de, a y el asunto. Un **registro** deriva que **Recordset** tendrá los mismos campos. Sin embargo, el **registro** también pueden tener otros campos únicos para el mensaje concreto representado por dicho **registro**, como datos adjuntos y Cc (con copia).  
  
 Aunque el **registro** objeto y la fila actual de la **Recordset** tienen los mismos campos, son diferentes porque **registro** y **Recordset**objetos tienen distintos métodos y propiedades.  
  
 Un campo que tienen en común la **registro** y **Recordset** puede modificarse en cualquiera de los objetos. Sin embargo, no se puede eliminar el campo en el **registro** objeto, aunque el proveedor subyacente permita establecer el campo en null.  
  
 Después de la **registro** está abierto, puede agregar mediante programación los campos. También puede eliminar los campos que se han agregado, pero no se puede eliminar campos de los originales **Recordset**.  
  
 También puede abrir el **registro** objeto directamente desde una dirección URL. En este caso, los campos se agregan a la **registro** dependen del proveedor subyacente. Actualmente, la mayoría de los proveedores agrega un conjunto de campos que describen la entidad representada por el **registro**. Si la entidad consta de una secuencia de bytes, como un archivo simple, un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto normalmente se puede abrir desde el **registro**.  
  
## <a name="special-fields-for-document-source-providers"></a>Campos especiales para el documento de origen de los proveedores  
 Una clase especial de proveedores, denominados *proveedores de código fuente de documentos*, administra las carpetas y documentos. Cuando un **registro** objeto que representa un documento o una **Recordset** objeto representa una carpeta de documentos, el proveedor de origen de documentos rellena esos objetos con un único conjunto de campos que describen las características del documento en su lugar del propio documento. Normalmente, un campo contiene una referencia a la **Stream** que representa el documento.  
  
 Estos campos constituyen un recurso **registro** o **recordset** y se muestran para los proveedores específicos que los respaldan en [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Índice de dos constantes del **campos** colección de un recurso **registro** o **Recordset** para recuperar un par de campos de uso general. El **campo** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad devuelve el contenido deseado.  
  
-   El campo que se obtiene acceso con el **adDefaultStream** constante contiene un flujo predeterminado asociado con el **registro** o **Recordset** objeto. El proveedor asigna una secuencia predeterminada a un objeto.  
  
-   El campo que se obtiene acceso con el **adRecordURL** constante contiene la dirección URL absoluta que identifica el documento.  
  
 Un proveedor de código fuente del documento no se admite la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de **registro** y **campo** objetos. El contenido de la **propiedades** collection es null para dichos objetos.  
  
 Un proveedor de código fuente del documento puede agregar una propiedad específica del proveedor como **el tipo de origen de datos** para identificar si es un proveedor de código fuente del documento. Para obtener más información acerca de cómo determinar el tipo de proveedor, vea la documentación del proveedor.  
  
## <a name="resource-recordset-columns"></a>Columnas del conjunto de registros de recursos  
 Un *conjunto de registros de recursos* consta de las siguientes columnas.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|adVarWChar|Solo lectura. Indica la dirección URL del recurso.|  
|RESOURCE_PARENTNAME|adVarWChar|Solo lectura. Indica la dirección URL absoluta del registro primario.|  
|RESOURCE_ABSOLUTEPARSENAME|adVarWChar|Solo lectura. Indica la dirección URL absoluta del recurso, que es la concatenación de PARENTNAME y PARSENAME.|  
|VALOR DE RESOURCE_ISHIDDEN|adBoolean|True si el recurso está oculto. A menos que el comando que crea explícitamente el conjunto de filas selecciona filas donde el valor de RESOURCE_ISHIDDEN es True, no se devolverá ninguna fila.|  
|RESOURCE_ISREADONLY|adBoolean|True si el recurso es de solo lectura. Si intenta abrir este recurso con DBBINDFLAG_WRITE, se producirá un error con DB_E_READONLY. Esta propiedad se puede editar incluso cuando el recurso solo se ha abierto para lectura.|  
|RESOURCE_CONTENTTYPE|adVarWChar|Indica el uso probable del documento, por ejemplo, de un abogado. Esto es posible que se corresponde con la plantilla de Office que se usó para crear el documento.|  
|RESOURCE_CONTENTCLASS|adVarWChar|Indica el tipo MIME del documento, que indica el formato, como "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|adVarWChar|Indica el idioma en el que se almacena el contenido.|  
|RESOURCE_CREATIONTIME|adFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora en que se creó el recurso. El tiempo se expresa en formato de hora Universal coordinada (UTC).|  
|RESOURCE_LASTACCESSTIME|adFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora de último acceso al recurso. La hora está en formato UTC. Los miembros FILETIME son cero si el proveedor no admite a este miembro de hora.|  
|RESOURCE_LASTWRITETIME|adFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora en que se escribió por última vez el recurso. La hora está en formato UTC. Los miembros FILETIME son cero si el proveedor no admite a este miembro de hora.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Solo lectura. Indica el tamaño de la secuencia predeterminada del recurso, en bytes.|  
|RESOURCE_ISCOLLECTION|adBoolean|Solo lectura. True si el recurso es una colección, como un directorio. False si el recurso es un archivo simple.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|adBoolean|True si el recurso es un documento estructurado. False si el recurso no es un documento estructurado. Podría ser una colección o un archivo simple.|  
|DEFAULT_DOCUMENT|adVarWChar|Solo lectura. Indica que este recurso contiene una dirección URL al documento simple predeterminado de una carpeta o un documento estructurado. Se utiliza cuando se solicita la secuencia predeterminada de un recurso. Esta propiedad está en blanco para un archivo simple.|  
|CHAPTERED_CHILDREN|adChapter|Solo lectura. Opcional. Indica el capítulo del conjunto de filas que contiene a los elementos secundarios del recurso. (El *proveedor OLE DB para la publicación en Internet* no utiliza esta columna.)|  
|RESOURCE_DISPLAYNAME|adVarWChar|Solo lectura. Indica el nombre para mostrar del recurso.|  
|RESOURCE_ISROOT|adBoolean|Solo lectura. True si el recurso es la raíz de una colección o documento estructurado.|  
  
## <a name="see-also"></a>Vea también  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
