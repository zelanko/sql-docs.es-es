---
title: Elemento &lt;xsd:redefine&gt; | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: rothja
ms.author: jroth
ms.openlocfilehash: ce439e81cf87e97b4afe6e25a201e1ab0cb2a458
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059466"
---
# <a name="the-ltxsdredefinegt-element"></a>Elemento &lt;xsd:redefine&gt;
  El elemento **redefine** de W3C XSD proporciona compatibilidad con la nueva definición de componentes de esquema. Sin embargo, la compatibilidad con esta directiva es potencialmente costosa para el rendimiento y también requiere que vuelva a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] validar todas las instancias del `xml` tipo de datos asociado al esquema redefinido. Por consiguiente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite este elemento. El servidor rechaza los esquemas XML que incluyen el **\<xsd:redefine>** elemento.  
  
 Para actualizar un esquema o sus componentes, puede hacer, en su lugar, lo que se indica a continuación:  
  
1.  Cree una nueva colección de esquemas XML con los componentes de esquema modificados.  
  
2.  Vuelva a escribir todos los `xml` tipos de datos (XML DT) que usan la colección de esquemas XML que se van a redefinir para usar la nueva colección de esquemas XML en su lugar. Para ello, use la opción ALTER COLUMN del comando ALTER TABLE para volver a escribir columnas o bien, cambie las restricciones de la colección de esquemas XML en variables o parámetros.  
  
3.  Quite la versión anterior de la colección de esquemas XML.  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
