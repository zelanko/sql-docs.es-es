---
title: Utilizar las anotaciones sql:guid y sql:identity
description: 'Obtenga información sobre cómo usar las anotaciones SQL: Identity y SQL: GUID en un esquema XSD para definir el comportamiento de un diagrama XML.'
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
ms.openlocfilehash: 2d1d8c72851c945f178bb9e206ad536a23f24891
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724760"
---
# <a name="using-the-sqlidentity-and-sqlguid-annotations"></a>Utilizar las anotaciones sql:guid y sql:identity
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Puede especificar las anotaciones **SQL: Identity** y **SQL: GUID** en un esquema XSD en cualquier nodo que se asigne a una columna de base de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Mientras que el formato diagrama admite los atributos **atributo updg: at-Identity** y **atributo updg: GUID** , el formato DiffGram no lo es. El atributo **atributo updg: at-Identity** define el comportamiento en la actualización de una columna de tipo Identity. El atributo **atributo updg: GUID** permite obtener un valor GUID de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usarlo en diagrama. Para obtener más información y ejemplos de trabajo, vea [Insertar datos mediante XML diagramas &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
 Las anotaciones **SQL: Identity** y **SQL: GUID** amplían esta funcionalidad a DiffGrams.  
  
 Cuando se ejecuta un DiffGram, primero se convierte en un diagrama de actualización que después se ejecuta. Al especificar las anotaciones **SQL: Identity** y **SQL: GUID** en el esquema XSD, en realidad está definiendo el comportamiento de un diagrama. Por consiguiente, todas las anotaciones se describen en el contexto de un diagrama de actualización. Las anotaciones se pueden utilizar tanto para DiffGrams como para diagramas de actualización; sin embargo, los diagramas de actualización ya proporcionan un modo más eficaz de administrar los valores de identidad y GUID.  
  
 Las anotaciones **SQL: Identity** y **SQL: GUID** se pueden definir en un elemento de contenido complejo.  
  
## <a name="sqlidentity-annotation"></a>Anotación sql:identity  
 Puede especificar la anotación **SQL: Identity** en el esquema XSD en cualquier nodo que se asigne a una columna de base de datos de tipo Identity. El valor especificado para esta anotación define cómo se actualiza la columna de tipo de identidad (ya sea mediante el valor proporcionado en diagrama para modificar la columna o omitiendo el valor, en cuyo caso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa un valor generado por para esta columna).  
  
 A la anotación **SQL: Identity** se le pueden asignar dos valores:  
  
 ignore  
 Hace que el diagrama de actualización omita cualquier valor que se proporcione en el diagrama de actualización para esa columna y deje que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere el valor de identidad.  
  
 useValue  
 Hace que el diagrama de actualización utilice el valor que se proporciona en el diagrama de actualización para actualizar la columna de tipo IDENTITY. Un diagrama de actualización no comprueba si la columna es un valor de identidad o no.  
  
 Si diagrama especifica un valor para la columna IDENTITY-Type, se debe especificar **SQL: Identity = "useValue"** en el esquema.  
  
## <a name="sqlguid-annotation"></a>Anotación sql:guid  
 Un diagrama de actualización puede hacer que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genere un valor GUID para después utilizarlo en el diagrama de actualización. En el contexto de los DiffGrams, puede usar la anotación **SQL: GUID** para especificar si se va a usar un valor GUID generado por SQL Server o usar el valor que se proporciona en diagrama para esa columna.  
  
 A la anotación **SQL: GUID** se le pueden asignar dos valores:  
  
 generate  
 Especifica que el GUID generado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se utilice para esa columna en la operación de actualización.  
  
 useValue  
 Especifica que el valor especificado en el diagrama de actualización se utilice para la columna. Este es el valor predeterminado.  
  
  
