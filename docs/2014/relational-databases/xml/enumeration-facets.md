---
title: Facetas de enumeración | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- enumeration facets
ms.assetid: dec23a79-ddd6-4701-9721-55a2c435a34d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c326c4f6f9d090d99de00580404953fa242586c3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104145"
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
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
