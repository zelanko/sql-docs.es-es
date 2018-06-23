---
title: Tipo xs:QName | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xs:QName type
ms.assetid: 72c5bfde-b0b2-4372-bf36-97ba930dea06
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 393130177c3597a9681e784e09be29fa8c2341fa
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199084"
---
# <a name="the-xsqname-type"></a>The xs:QName Type
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite los tipos derivados de **xs:QName** que utilizan un elemento de restricción de esquema XML. Actualmente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite tipos de unión con **QName** como tipo de miembro.  
  
## <a name="example"></a>Ejemplo  
 Las instrucciones `CREATE XML SCHEMA COLLECTION` siguientes no pueden cargar el esquema XML, ya que especifican el tipo `xs:QName` como tipo de miembro de la unión:  
  
```  
CREATE XML SCHEMA COLLECTION QNameLimitation1 AS N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:simpleType name="myUnion">  
        <xs:union memberTypes="xs:int xs:QName"/>  
    </xs:simpleType>  
</xs:schema>'  
GO  
  
CREATE XML SCHEMA COLLECTION QNameLimitation2 AS N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <xs:simpleType name="myUnion">  
        <xs:union memberTypes="xs:integer">  
   <xs:simpleType>  
    <xs:list itemType="xs:QName"/>  
   </xs:simpleType>  
  </xs:union>  
    </xs:simpleType>  
</xs:schema>'  
GO  
```  
  
 Ambas instrucciones generan un mensaje de error.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  