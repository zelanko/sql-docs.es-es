---
title: Tipo mixto y contenido simple | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf0e4f54334d84aea5a33392655110374e893cc4
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531099"
---
# <a name="mixed-type-and-simple-content"></a>Contenido simple y de tipo mixto
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite la restricción de un tipo mixto a un contenido simple.  
  
## <a name="example"></a>Ejemplo  
 En la colección de esquemas XML siguiente, `myComplexTypeA` es un tipo complejo que se puede vaciar. Es decir, ambos elementos tienen `minOccurs` establecido en 0. No se admite el intento de restringir esto a un contenido simple, como en la declaración `myComplexTypeB` . Por tanto, se produce un error en la creación de la colección de esquemas XML.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
