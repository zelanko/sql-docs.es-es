---
title: Registros y campos proporcionados por el proveedor | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- records-provided fields [ADO]
- provider-supplied fields [ADO]
ms.assetid: 77f95e0a-0cf2-411a-a792-593f77330fbd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93b97bce2562604a01c564a376bd093abb9b1b7c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="records-and-provider-supplied-fields"></a>Registros y campos proporcionados por el proveedor
Cuando un [registro](../../../ado/reference/ado-api/record-object-ado.md) objeto está abierto, su origen puede ser la fila actual de un formato de archivo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), una dirección URL absoluta o una dirección URL relativa junto con un formato de archivo [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto .  
  
 Si el **registro** se abre desde una **Recordset**, el **registro** objeto [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección contendrá todos los campos de la  **Conjunto de registros**, además de los campos agregados por el proveedor subyacente.  
  
 El proveedor puede insertar campos adicionales que sirven de características adicionales de la **registro**. Como resultado, un **registro** puede tener campos únicos no en el **Recordset** como un todo o cualquier **registro** derivado de otra fila de la **Recordset**.  
  
 Por ejemplo, todas las filas de un **Recordset** derivado de correo electrónico en una origen de datos podría tener columnas de, a y el asunto. A **registro** deriva que **Recordset** tendrá los mismos campos. Sin embargo, el **registro** también pueden tener otros campos únicos para el mensaje concreto representado por esa **registro**, como datos adjuntos y Cc (con copia).  
  
 Aunque la **registro** objeto y la fila actual de la **Recordset** tienen los mismos campos, son diferentes porque **registro** y **delconjuntoderegistros**objetos tienen distintos métodos y propiedades.  
  
 Un campo que tienen en común la **registro** y **Recordset** puede modificarse en cualquiera de los objetos. Sin embargo, no se puede eliminar el campo en el **registro** objeto, aunque el proveedor subyacente permita establecer el campo en null.  
  
 Después de la **registro** está abierto, puede agregar mediante programación campos. También puede eliminar campos que haya agregado, pero no se puede eliminar campos de los originales **conjunto de registros**.  
  
 También puede abrir el **registro** objeto directamente desde una dirección URL. En este caso, los campos se agregan a la **registro** dependen del proveedor subyacente. Actualmente, la mayoría de los proveedores agrega un conjunto de campos que describen la entidad representada por la **registro**. Si la entidad consta de una secuencia de bytes, como un archivo simple, un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) normalmente se puede abrir el objeto desde el **registro**.  
  
## <a name="special-fields-for-document-source-providers"></a>Campos especiales para el documento de origen de proveedores  
 Una clase especial de proveedores, denominados *proveedores de orígenes de documentos*, administra las carpetas y documentos. Cuando un **registro** objeto que representa un documento o una **Recordset** objeto representa una carpeta de documentos, el proveedor de origen de documentos rellena esos objetos con un único conjunto de campos que describen características del documento en su lugar del propio documento. Normalmente, un campo contiene una referencia a la **flujo** que representa el documento.  
  
 Estos campos constituyen un recurso **registro** o **recordset** y se enumeran para los proveedores específicos que los respaldan en [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md).  
  
 Índice de dos constantes la **campos** colección de un recurso **registro** o **Recordset** para recuperar un par de campos que se usan habitualmente. El **campo** objeto [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad devuelve el contenido deseado.  
  
-   El campo que se obtiene acceso con el **adDefaultStream** constante contiene una secuencia predeterminada asociada a la **registro** o **Recordset** objeto. El proveedor asigna una secuencia predeterminada a un objeto.  
  
-   El campo que se obtiene acceso con el **adRecordURL** constante contiene la dirección URL absoluta que identifica el documento.  
  
 Un proveedor de código fuente del documento no es compatible con la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de **registro** y **campo** objetos. El contenido de la **propiedades** colección es nulo para dichos objetos.  
  
 Un proveedor de código fuente del documento puede agregar una propiedad específica del proveedor como **tipo de origen de datos** para identificar si es un proveedor de código fuente del documento. Para obtener más información acerca de cómo determinar el tipo de proveedor, vea la documentación del proveedor.  
  
## <a name="resource-recordset-columns"></a>Columnas de conjunto de registros de recursos  
 A *el conjunto de registros de recursos* consta de las siguientes columnas.  
  
|Nombre de columna|Tipo|Description|  
|-----------------|----------|-----------------|  
|RESOURCE_PARSENAME|AdVarWChar|Solo lectura. Indica la dirección URL del recurso.|  
|RESOURCE_PARENTNAME|AdVarWChar|Solo lectura. Indica la dirección URL absoluta del registro primario.|  
|RESOURCE_ABSOLUTEPARSENAME|AdVarWChar|Solo lectura. Indica la dirección URL absoluta del recurso, que es la concatenación de PARENTNAME y PARSENAME.|  
|VALOR DE RESOURCE_ISHIDDEN|AdBoolean|Es True si el recurso está oculto. A menos que el comando que crea el conjunto de filas explícitamente selecciona filas donde el valor de RESOURCE_ISHIDDEN es True, no se devolverá ninguna fila.|  
|RESOURCE_ISREADONLY|AdBoolean|Es True si el recurso es de solo lectura. Intenta abrir este recurso con DBBINDFLAG_WRITE, se producirá un error con DB_E_READONLY. Esta propiedad se puede editar incluso cuando el recurso solo se ha abierto para lectura.|  
|RESOURCE_CONTENTTYPE|AdVarWChar|Indica el uso probable del documento, por ejemplo, de un abogado. Esto puede corresponder a la plantilla de Office que se usó para crear el documento.|  
|RESOURCE_CONTENTCLASS|AdVarWChar|Indica el tipo MIME del documento, que indica el formato como "`text/html`".|  
|RESOURCE_CONTENTLANGUAGE|AdVarWChar|Indica el idioma en el que se almacena el contenido.|  
|RESOURCE_CREATIONTIME|adFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora en que se creó el recurso. El tiempo se expresa en formato de hora Universal coordinada (UTC).|  
|RESOURCE_LASTACCESSTIME|AdFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora de último acceso a los recursos. La hora está en formato UTC. Los miembros FILETIME son cero si el proveedor no admite a este miembro de hora.|  
|RESOURCE_LASTWRITETIME|AdFileTime|Solo lectura. Indica una estructura FILETIME que contiene la hora en que se escribió por última vez el recurso. La hora está en formato UTC. Los miembros FILETIME son cero si el proveedor no admite a este miembro de hora.|  
|RESOURCE_STREAMSIZE|asUnsignedBigInt|Solo lectura. Indica el tamaño de secuencia de forma predeterminada del recurso, en bytes.|  
|RESOURCE_ISCOLLECTION|AdBoolean|Solo lectura. Es True si el recurso es una colección, como un directorio. False si el recurso es un archivo simple.|  
|RESOURCE_ISSTRUCTUREDDOCUMENT|AdBoolean|Es True si el recurso es un documento estructurado. False si el recurso no es un documento estructurado. Podría ser una colección o un archivo simple.|  
|DEFAULT_DOCUMENT|AdVarWChar|Solo lectura. Indica que este recurso contiene una dirección URL al documento simple predeterminado de una carpeta o un documento estructurado. Se utiliza cuando se solicita la secuencia predeterminada de un recurso. Esta propiedad está en blanco para un archivo simple.|  
|CHAPTERED_CHILDREN|Dbtype_hchapter|Solo lectura. Opcional. Indica el capítulo del conjunto de filas que contiene a los elementos secundarios del recurso. (El *proveedor OLE DB para Internet Publishing* no utiliza esta columna.)|  
|RESOURCE_DISPLAYNAME|AdVarWChar|Solo lectura. Indica el nombre para mostrar del recurso.|  
|RESOURCE_ISROOT|AdBoolean|Solo lectura. Es True si el recurso es la raíz de una colección o documento estructurado.|  
  
## <a name="see-also"></a>Vea también  
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)

