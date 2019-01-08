---
title: Con las anotaciones de sql:identity y sql:guid | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb953042707054a7dbfdee697b986e7e65f7059b
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52786187"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizar las anotaciones sql:guid y sql:identity
  Puede especificar el `sql:identity` y `sql:guid` anotaciones en un esquema XSD en cualquier nodo que se asigna a una columna de base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mientras que el formato de diagrama de actualización (updategram) admite los atributos `updg:at-identity` y `updg:guid`, el formato de DiffGram no. El atributo `updg:at-identity` define el comportamiento al actualizar una columna de tipo IDENTITY. El atributo `updg:guid` permite obtener un valor GUID de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y utilizarlo en el diagrama de actualización. Para obtener más información y ejemplos de trabajo, consulte [actualización de inserción de datos usando XML &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Las anotaciones `sql:identity` y `sql:guid` extienden esta funcionalidad a los DiffGrams.  
  
 Cuando se ejecuta un DiffGram, primero se convierte en un diagrama de actualización que después se ejecuta. Al especificar las anotaciones `sql:identity` y `sql:guid` en el esquema XSD, lo que se está haciendo en realidad es definir el comportamiento de un diagrama de actualización. Por consiguiente, todas las anotaciones se describen en el contexto de un diagrama de actualización. Las anotaciones se pueden utilizar tanto para DiffGrams como para diagramas de actualización; sin embargo, los diagramas de actualización ya proporcionan un modo más eficaz de administrar los valores de identidad y GUID.  
  
 Las anotaciones `sql:identity` y `sql:guid` se pueden definir en un elemento de contenido complejo.  
  
## <a name="sqlidentity-annotation"></a>Anotación sql:identity  
 Puede especificar la anotación `sql:identity` en el esquema XSD en cualquier nodo que se asigne a una columna de base de datos de tipo IDENTITY. El valor especificado para esta anotación define cómo se actualiza la columna de tipo IDENTITY (ya sea mediante el valor proporcionado en el diagrama de actualización para modificar la columna o se omite el valor, en cuyo caso un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-valor generado se usa para esta columna).  
  
 A la anotación `sql:identity` se le pueden asignar dos valores:  
  
 ignore  
 Hace que el diagrama de actualización omita cualquier valor que se proporcione en el diagrama de actualización para esa columna y deje que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere el valor de identidad.  
  
 useValue  
 Hace que el diagrama de actualización utilice el valor que se proporciona en el diagrama de actualización para actualizar la columna de tipo IDENTITY. Un diagrama de actualización no comprueba si la columna es un valor de identidad o no.  
  
 Si el diagrama de actualización especifica un valor para la columna de tipo IDENTITY, se debe especificar `sql:identity="useValue"` en el esquema.  
  
## <a name="sqlguid-annotation"></a>Anotación sql:guid  
 Un diagrama de actualización puede hacer que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un valor GUID para después utilizarlo en el diagrama de actualización. En el contexto de los DiffGrams, puede utilizar la anotación `sql:guid` para especificar si desea utilizar un valor GUID generado por SQL Server o utilizar el valor que se proporciona en el diagrama de actualización para esa columna.  
  
 A la anotación `sql:guid` se le pueden asignar dos valores:  
  
 generate  
 Especifica que el GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilice para esa columna en la operación de actualización.  
  
 useValue  
 Especifica que el valor especificado en el diagrama de actualización se utilice para la columna. Este es el valor predeterminado.  
  
  
