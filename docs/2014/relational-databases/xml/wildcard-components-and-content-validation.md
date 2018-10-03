---
title: Componentes comodín y validación del contenido | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 930fe318d47212ff52fea572974d501cc316c1ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193395"
---
# <a name="wildcard-components-and-content-validation"></a>Componentes comodín y validación del contenido
  Los componentes comodín se utilizan para aumentar la flexibilidad en cuanto a lo que se permite que aparezca en un modelo de contenido. El lenguaje XSD admite estos componentes de las formas siguientes:  
  
-   Componentes de carácter comodín de elementos. Se representan mediante el elemento **\<xsd:any>**.  
  
-   Componentes de carácter comodín de atributos. Se representan mediante el elemento **\<xsd:anyAttribute>**.  
  
 Ambos elementos de carácter comodín, **\<xsd:any>** y **\<xsd:anyAttribute>**, admiten el uso de un atributo **processContents**. Esto permite especificar un valor que indica el modo en que las aplicaciones XML controlan la validación del contenido de los documentos asociado a estos elementos de caracteres comodín. A continuación se exponen los distintos valores y su efecto:  
  
-   El valor **strict** especifica que se valida totalmente el contenido.  
  
-   El valor **skip** especifica que no se valida totalmente el contenido  
  
-   El valor **lax** especifica que solo se validan los elementos y atributos para los que hay disponibles definiciones de esquema.  
  
## <a name="lax-validation-and-xsanytype-elements"></a>La validación lax y los elementos xs:anyType  
 La especificación de esquemas XML utiliza la validación **lax** para los elementos del tipo **anyType** . Puesto que [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no admitía la validación lax, se aplicaba la validación estricta a los elementos **anyType**. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], se admite la validación lax. El contenido de los elementos de tipo **anyType** se validará utilizando la validación lax.  
  
 En el ejemplo siguiente se ilustra la validación lax: el elemento de esquema `e` es de tipo **anyType** . El ejemplo crea variables **xml** con tipo e ilustra la validación lax del elemento de tipo **anyType** .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 El ejemplo siguiente funciona correctamente porque la validación de `<e>` es correcta:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 El ejemplo siguiente funciona correctamente: se acepta la instancia, aunque no se haya definido ningún elemento `<c>` en el esquema:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 La instancia XML del ejemplo siguiente se rechaza, porque la definición del elemento `<a>` no permite un valor de cadena.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
