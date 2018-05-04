---
title: 'Mediante las anotaciones SQL: GUID y | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:guid
- annotated XSD schemas, IDENTITY-type columns
- annotated XSD schemas, GUID values
- DiffGrams [SQLXML], annotations
- identity annotation
- XSD schemas [SQLXML], GUID values
- GUIDs [SQLXML]
- guid annotation
- sql:identity
- IDENTITY-type column
- XSD schemas [SQLXML], IDENTITY-type columns
- updategrams [SQLXML], GUID values
ms.assetid: 7661dfd0-6573-4692-a8f1-3597adcd33c4
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2a9fcb72c9c5cd32268fc008740e230945aa3754
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizar las anotaciones sql:guid y sql:identity
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede especificar el **SQL: Identity** y **SQL** anotaciones en un esquema XSD en cualquier nodo que se asigna a una columna de base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mientras que el formato de diagrama de actualización admite la **updg: en la identidad de** y **updg: GUID** atributos, el formato DiffGram no. El **updg: en la identidad** atributo define el comportamiento en la actualización de una columna de tipo IDENTITY. El **updg: GUID** atributo permite obtener un valor GUID de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usarla en el diagrama de actualización. Para obtener más información y ejemplos prácticos, vea [insertar datos utilizando XML los diagramas de actualización &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 El **SQL: Identity** y **SQL** anotaciones amplían esta funcionalidad a los DiffGrams.  
  
 Cuando se ejecuta un DiffGram, primero se convierte en un diagrama de actualización que después se ejecuta. Mediante la especificación de la **SQL: Identity** y **SQL** las anotaciones en el esquema XSD, es en realidad es definir el comportamiento de un diagrama de actualización. Por consiguiente, todas las anotaciones se describen en el contexto de un diagrama de actualización. Las anotaciones se pueden utilizar tanto para DiffGrams como para diagramas de actualización; sin embargo, los diagramas de actualización ya proporcionan un modo más eficaz de administrar los valores de identidad y GUID.  
  
 El **SQL: Identity** y **SQL** anotaciones se pueden definir en un elemento de contenido complejo.  
  
## <a name="sqlidentity-annotation"></a>Anotación sql:identity  
 Puede especificar el **SQL: Identity** anotación en el esquema XSD en cualquier nodo que se asigna a una columna de base de datos de tipo IDENTITY. El valor especificado para esta anotación define cómo se actualiza la columna de tipo IDENTITY (ya sea utilizando el valor proporcionado en el diagrama de actualización para modificar la columna u omitiendo el valor, en cuyo caso se utiliza un valor generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para esta columna).  
  
 El **SQL: Identity** anotación se puede asignar dos valores:  
  
 ignore  
 Hace que el diagrama de actualización omita cualquier valor que se proporcione en el diagrama de actualización para esa columna y deje que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere el valor de identidad.  
  
 useValue  
 Hace que el diagrama de actualización utilice el valor que se proporciona en el diagrama de actualización para actualizar la columna de tipo IDENTITY. Un diagrama de actualización no comprueba si la columna es un valor de identidad o no.  
  
 Si el diagrama de actualización especifica un valor para la columna de tipo de identidad, el **SQL: Identity = "useValue"** debe especificarse en el esquema.  
  
## <a name="sqlguid-annotation"></a>Anotación sql:guid  
 Un diagrama de actualización puede hacer que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un valor GUID para después utilizarlo en el diagrama de actualización. En el contexto de los DiffGrams, puede usar el **SQL** anotación que se debe especificar si desea usar un valor GUID generado por SQL Server o utilice el valor que se proporciona en el diagrama de actualización para esa columna.  
  
 El **SQL** anotación se puede asignar dos valores:  
  
 generate  
 Especifica que el GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilice para esa columna en la operación de actualización.  
  
 useValue  
 Especifica que el valor especificado en el diagrama de actualización se utilice para la columna. Es el valor predeterminado.  
  
  
