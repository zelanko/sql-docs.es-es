---
title: Modelos de contenido no determinista | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- non-deterministic content models
- content models [XML in SQL Server]
ms.assetid: 9d4513e7-dd19-4491-b7c7-28bc7c2f8589
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea86115b88c693e70faa677fdea518f8886bae0f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531277"
---
# <a name="non-deterministic-content-models"></a>modelos de contenido no determinista
  Antes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 (SP1), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechazaba los esquemas XML que tenían modelos de contenido no deterministas.  
  
 Pero a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1, se aceptan modelos de contenido no deterministas si las restricciones de repetición son 0, 1 o sin delimitar.  
  
## <a name="example-non-deterministic-content-model-rejected"></a>Ejemplo: modelo de contenido no determinista rechazado  
 En el siguiente ejemplo se intenta crear un esquema XML con un modelo de contenido no determinista. El código genera un error porque no está claro si el elemento `<root>` debería tener una secuencia de dos elementos `<a>` o si el elemento `<root>` debería tener dos secuencias, cada una de ellas con un elemento `<a>` .  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="1" maxOccurs="2">  
                <element name="a" type="string" minOccurs="1" maxOccurs="2"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
 El esquema se puede corregir moviendo la restricción de repetición a una ubicación única. Por ejemplo, la restricción se puede mover a la partícula de secuencia contenedora:  
  
```  
<sequence minOccurs="1" maxOccurs="4">  
    <element name="a" type="string" minOccurs="1" maxOccurs="1"/>  
</sequence>  
```  
  
 O bien, la restricción se puede mover al elemento contenido:  
  
```  
<sequence minOccurs="1" maxOccurs="1">  
     <element name="a" type="string" minOccurs="1" maxOccurs="4"/>  
</sequence>  
```  
  
## <a name="example-non-deterministic-content-model-accepted"></a>Ejemplo: modelo de contenido no determinista aceptado  
 El esquema siguiente se rechazaría en versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1.  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
    <element name="root">  
        <complexType>  
            <sequence minOccurs="0" maxOccurs="unbounded">  
                <element name="a" type="string" minOccurs="0" maxOccurs="1"/>  
                <element name="b" type="string" minOccurs="1" maxOccurs="unbounded"/>  
            </sequence>  
        </complexType>  
    </element>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
