---
title: "Componentes comodín y validación del contenido | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3eac26ac7add89b64c19672ae9fd34e224c6e7e1
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

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
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
