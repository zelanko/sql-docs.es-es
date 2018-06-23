---
title: Elemento &lt;xsd:redefine&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 4ca94410d7011c30de0a5481451337d11fa57120
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204758"
---
# <a name="the-ltxsdredefinegt-element"></a>Elemento &lt;xsd:redefine&gt;
  El elemento **redefine** de W3C XSD proporciona compatibilidad con la nueva definición de componentes de esquema. Sin embargo, la compatibilidad con esta directiva puede afectar al rendimiento y también requiere que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] volver a validar todas las instancias de la `xml` tipo de datos asociado con el esquema redefinido. Por consiguiente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite este elemento. El servidor rechaza los esquemas XML que incluyen el elemento **\<xsd:redefine>**.  
  
 Para actualizar un esquema o sus componentes, puede hacer, en su lugar, lo que se indica a continuación:  
  
1.  Cree una nueva colección de esquemas XML con los componentes de esquema modificados.  
  
2.  Vuelva a escribir todos los tipos de datos `xml` (XML DT) que usan la colección de esquemas XML que se va a volver a definir para usar la nueva colección de esquemas XML en su lugar. Para ello, use la opción ALTER COLUMN del comando ALTER TABLE para volver a escribir columnas o bien, cambie las restricciones de la colección de esquemas XML en variables o parámetros.  
  
3.  Quite la versión anterior de la colección de esquemas XML.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  