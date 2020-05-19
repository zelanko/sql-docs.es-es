---
title: Anotaciones XSD (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b7fa444ebbf33c48a243703a19d1f296ce91816e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703463"
---
# <a name="xsd-annotations-sqlxml-40"></a>Anotaciones de XSD (SQLXML 4.0)
  En la tabla siguiente se enumeran las anotaciones XSD que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y se comparan con las anotaciones XDR que se introdujeron en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Anotación XSD|Descripción|Vínculo de tema|Anotación XDR|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|Cuando un atributo o elemento XML está asignado a una columna BLOB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permite la solicitud de un URI de referencia. Este URI se puede usar posteriormente para devolver datos BLOB.|[Solicitar referencias URL a datos BLOB mediante SQL: encode &#40;SQLXML 4,0&#41;](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|Le permite especificar si se ha de usar un valor GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el valor proporcionado en la actualización por XML (updategram) para dicha columna.|[Utilizar las anotaciones sql:guid y sql:identity](using-the-sql-identity-and-sql-guid-annotations.md)|No compatible|  
|`sql:hide`|Oculta el elemento o atributo que se especifica en el esquema del documento XML resultante.|[Ocultar elementos y atributos mediante sql:hide](hiding-elements-and-attributes-by-using-sql-hide.md)|No compatible|  
|`sql:identity`|Se puede especificar en cualquier nodo que se asigna a una columna de base de datos del tipo IDENTITY. El valor especificado para esta anotación define cómo se actualiza la columna del tipo IDENTITY de la base de datos.|[Utilizar las anotaciones sql:guid y sql:identity](using-the-sql-identity-and-sql-guid-annotations.md)|No compatible|  
|`sql:inverse`|Indica a la lógica de diagrama que inverso su interpretación de la relación de elementos primarios y secundarios que se ha especificado mediante ** \< SQL: Relationship>**.|[Especificar el atributo SQL: inverso en SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|No compatible|  
|`sql:is-constant`|Crea un elemento XML que no se asigna a ninguna tabla. El elemento aparece en el resultado de la consulta.|[Crear elementos constantes mediante SQL: is-Constant &#40;SQLXML 4,0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Iguales|  
|`sql:key-fields`|Permite la especificación de columnas que identifican de forma exclusiva las filas de una tabla.|[Identificar columnas de clave mediante SQL: Key-Fields &#40;SQLXML 4,0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Iguales|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|Permite limitar los valores que se devuelven en base a un valor de limitación.|[Filtrar valores mediante SQL: Limit-Field y SQL: Limit-Value &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|Iguales|  
|`sql:mapped`|Permite excluir los elementos de esquema del resultado.|[Excluir elementos de esquema del documento XML resultante mediante SQL: asignado &#40;SQLXML 4,0&#41;](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|Le permite especificar la profundidad de las relaciones recursivas que se especifican en el esquema.|[Especificar la profundidad en relaciones recursivas utilizando sql:max-depth](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|No compatible|  
|`sql:overflow-field`|Identifica la columna de base de datos que contiene los datos de desbordamiento.|[Recuperar datos no utilizados mediante SQL: Overflow-Field &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|Iguales|  
|`sql:prefix`|Crea ID, IDREF e IDREFS de XML válidos. Antepone a los valores de ID, IDREF e IDREFS una cadena.|[Crear atributos válidos de tipo ID, IDREF e IDREFS mediante SQL: prefix &#40;SQLXML 4,0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Iguales|  
|`sql:relationship`|Especifica las relaciones entre los elementos XML. Los atributos `parent`, `child`, `parent-key` y `child-key` se usan para establecer la relación.|[Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|Los nombres de atributo son diferentes:<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|Permite especificar secciones CDATA que se van a utilizar para ciertos elementos en el documento XML.|[Crear secciones CDATA mediante SQL: Use-CDATA &#40;SQLXML 4,0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Iguales|  
  
> [!NOTE]  
>  El atributo XSD nativo `targetNamespace` reemplaza la anotación `target-namespace` que se introdujo en el esquema de asignación XDR [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Especificar un espacio de nombres de destino mediante el atributo targetNamespace &#40;SQLXML 4,0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
