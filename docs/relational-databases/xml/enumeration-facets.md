---
title: "Facetas de enumeración | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enumeration facets
ms.assetid: dec23a79-ddd6-4701-9721-55a2c435a34d
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 106f9d6c0cd5b737e602b4192545419b982ca50a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="enumeration-facets"></a>facetas de enumeración
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza los esquemas XML con tipos que tienen facetas de patrón o enumeraciones que infringen estas facetas.  
  
## <a name="example"></a>Ejemplo  
 El esquema siguiente se verá rechazado porque su valor de enumeración incluye un valor con mayúsculas y minúsculas mezcladas. También se rechazará porque infringe el valor de patrón que limita los valores únicamente a letras minúsculas.  
  
```  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
    <simpleType name="MyST">  
       <restriction base="string">  
          <pattern value="[a-z]*"/>  
       </restriction>  
    </simpleType>  
  
    <simpleType name="MyST2">  
       <restriction base="ns:MyST">  
           <enumeration value="mYstring"/>  
       </restriction>  
    </simpleType>  
</schema>'  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
