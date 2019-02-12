---
title: Anotaciones de XSD (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: MightyPen
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1d2e5b48d3e3be630029ab508d59470fad0f8547
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015136"
---
# <a name="xsd-annotations-sqlxml-40"></a>Anotaciones de XSD (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En la tabla siguiente se enumeran las anotaciones XSD que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y se comparan con las anotaciones XDR que se introdujeron en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
|Anotación XSD|Descripción|Vínculo de tema|Anotación XDR|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|Cuando un atributo o elemento XML está asignado a una columna BLOB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permite la solicitud de un URI de referencia. Este URI se puede usar posteriormente para devolver datos BLOB.|[Solicitar referencias URL a datos BLOB mediante sql: encode &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**url-encode**|  
|**sql:guid**|Le permite especificar si se ha de usar un valor GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el valor proporcionado en la actualización por XML (updategram) para dicha columna.|[Utilizar las anotaciones sql:guid y sql:identity](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|No compatible|  
|**sql:hide**|Oculta el elemento o atributo que se especifica en el esquema del documento XML resultante.|[Ocultar elementos y atributos mediante sql:hide](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|No compatible|  
|**sql:identity**|Se puede especificar en cualquier nodo que se asigna a una columna de base de datos del tipo IDENTITY. El valor especificado para esta anotación define cómo se actualiza la columna del tipo IDENTITY de la base de datos.|[Utilizar las anotaciones sql:guid y sql:identity](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|No compatible|  
|**sql:inverse**|Indica a la lógica del diagrama de actualización que invierta su interpretación de la relación de elementos primarios y secundarios que se ha especificado mediante  **\<SQL: Relationship >**.|[Especificar el atributo SQL: Inverse en SQL: Relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|No compatible|  
|**sql:is-constant**|Crea un elemento XML que no se asigna a ninguna tabla. El elemento aparece en el resultado de la consulta.|[Crear elementos constantes mediante sql: constante es &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|Iguales|  
|**sql:key-fields**|Permite la especificación de columnas que identifican de forma exclusiva las filas de una tabla.|[Identificar columnas de clave mediante SQL: Key-campos &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|Iguales|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|Permite limitar los valores que se devuelven en base a un valor de limitación.|[Filtrar valores mediante SQL: limit-campo y SQL: limit-valor &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|Iguales|  
|**sql:mapped**|Permite excluir los elementos de esquema del resultado.|[Excluir elementos de esquema del documento XML resultante mediante sql: asigna &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**map-field**|  
|**sql:max-depth**|Le permite especificar la profundidad de las relaciones recursivas que se especifican en el esquema.|[Especificar la profundidad en relaciones recursivas mediante sql:max-depth](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|No compatible|  
|**sql:overflow-field**|Identifica la columna de base de datos que contiene los datos de desbordamiento.|[Recuperar datos no consumidos mediante Overflow-campo &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|Iguales|  
|**sql:prefix**|Crea ID, IDREF e IDREFS de XML válidos. Antepone a los valores de ID, IDREF e IDREFS una cadena.|[Creación de un identificador válido, IDREF e IDREFS tipo atributos mediante SQL: prefix &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|Iguales|  
|**sql:relationship**|Especifica las relaciones entre los elementos XML. El **primario**, **secundarios**, **clave principal**, y **secundarios clave** atributos se utilizan para establecer la relación.|[Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|Los nombres de atributo son diferentes:<br /><br /> **key-relation**<br /><br /> **foreign-relation**<br /><br /> **key**<br /><br /> **foreign-key**|  
|**sql:use-cdata**|Permite especificar secciones CDATA que se van a utilizar para ciertos elementos en el documento XML.|[Creación de secciones de CDATA mediante SQL: use-cdata &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|Iguales|  
  
> [!NOTE]  
>  El XSD nativo **targetNamespace** atributo reemplaza el **target-namespace** anotación que se introdujo en la [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] esquema de asignación XDR.  
  
## <a name="see-also"></a>Vea también  
 [Especificar un destino Namespace mediante el atributo targetNamespace &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
