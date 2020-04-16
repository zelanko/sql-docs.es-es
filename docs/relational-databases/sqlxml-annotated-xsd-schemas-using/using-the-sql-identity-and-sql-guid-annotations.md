---
title: Utilizar las anotaciones sql:guid y sql:identity
description: Aprenda a usar las anotaciones sql:identity y sql:guid en un esquema XSD para definir el comportamiento de un diagrama de actualización XML.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f581c1a5c0d925d48df5a16d95cdb141e2d48f83
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388105"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizar las anotaciones sql:guid y sql:identity
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Puede especificar las anotaciones **sql:identity** y **sql:guid** en un esquema XSD [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en cualquier nodo que se asigne a una columna de base de datos en . Mientras que el formato updategram admite los atributos **updg:at-identity** y **updg:guid,** el formato DiffGram no. El atributo **updg:at-identity** define el comportamiento en la actualización de una columna de tipo IDENTITY. El atributo **updg:guid** permite obtener un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valor GUID y usarlo en el diagrama de actualización. Para obtener más información y ejemplos de trabajo, vea Insertar datos mediante diagramas de [actualización XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Las anotaciones **sql:identity** y **sql:guid** extienden esta funcionalidad a DiffGrams.  
  
 Cuando se ejecuta un DiffGram, primero se convierte en un diagrama de actualización que después se ejecuta. Al especificar las anotaciones **sql:identity** y **sql:guid** en el esquema XSD, de hecho está definiendo el comportamiento de un diagrama de actualización. Por consiguiente, todas las anotaciones se describen en el contexto de un diagrama de actualización. Las anotaciones se pueden utilizar tanto para DiffGrams como para diagramas de actualización; sin embargo, los diagramas de actualización ya proporcionan un modo más eficaz de administrar los valores de identidad y GUID.  
  
 Las anotaciones **sql:identity** y **sql:guid** se pueden definir en un elemento de contenido complejo.  
  
## <a name="sqlidentity-annotation"></a>Anotación sql:identity  
 Puede especificar la anotación **sql:identity** en el esquema XSD en cualquier nodo que se asigne a una columna de base de datos de tipo IDENTITY. El valor especificado para esta anotación define cómo se actualiza la columna de tipo IDENTITY (ya sea mediante el valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proporcionado en el diagrama de actualización para modificar la columna o ignorando el valor, en cuyo caso se utiliza un valor generado para esta columna).  
  
 A la anotación **sql:identity** se le pueden asignar dos valores:  
  
 ignore  
 Hace que el diagrama de actualización omita cualquier valor que se proporcione en el diagrama de actualización para esa columna y deje que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere el valor de identidad.  
  
 useValue  
 Hace que el diagrama de actualización utilice el valor que se proporciona en el diagrama de actualización para actualizar la columna de tipo IDENTITY. Un diagrama de actualización no comprueba si la columna es un valor de identidad o no.  
  
 Si el diagrama de actualización especifica un valor para la columna de tipo IDENTITY, se debe especificar **sql:identity-"useValue"** en el esquema.  
  
## <a name="sqlguid-annotation"></a>Anotación sql:guid  
 Un diagrama de actualización puede hacer que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un valor GUID para después utilizarlo en el diagrama de actualización. En el contexto de DiffGrams, puede usar la anotación **sql:guid** para especificar si se debe usar un valor GUID generado por SQL ServerSQL Server o usar el valor que se proporciona en el diagrama de actualización para esa columna.  
  
 A la anotación **sql:guid** se le pueden asignar dos valores:  
  
 generate  
 Especifica que el GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilice para esa columna en la operación de actualización.  
  
 useValue  
 Especifica que el valor especificado en el diagrama de actualización se utilice para la columna. Este es el valor predeterminado.  
  
  
