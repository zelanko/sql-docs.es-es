---
title: Elemento &lt;xsd:redefine&gt; | Microsoft Docs
description: Obtenga información sobre la compatibilidad de con el elemento de redefinición XSD de W3C y cómo actualizar un esquema XML o sus componentes.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f2791ea8a8cae425ae7839a7af2d722e8cfe8a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729864"
---
# <a name="the-ltxsdredefinegt-element"></a>Elemento &lt;xsd:redefine&gt;
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  El elemento **redefine** de W3C XSD proporciona compatibilidad con la nueva definición de componentes de esquema. Pero la compatibilidad con esta directiva puede afectar al rendimiento y también requiere que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vuelva a validar todas las instancias del tipo de datos **xml** asociado al esquema que se ha vuelto a definir. Por consiguiente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite este elemento. El servidor rechaza los esquemas XML que incluyen el elemento **\<xsd:redefine>** .  
  
 Para actualizar un esquema o sus componentes, puede hacer, en su lugar, lo que se indica a continuación:  
  
1.  Cree una nueva colección de esquemas XML con los componentes de esquema modificados.  
  
2.  Vuelva a escribir todos los tipos de datos **xml** (XML DT) que usan la colección de esquemas XML que se va a volver a definir para usar la nueva colección de esquemas XML en su lugar. Para ello, use la opción ALTER COLUMN del comando ALTER TABLE para volver a escribir columnas o bien, cambie las restricciones de la colección de esquemas XML en variables o parámetros.  
  
3.  Quite la versión anterior de la colección de esquemas XML.  

## <a name="see-also"></a>Consulte también  
 [Requisitos y limitaciones de las colecciones de esquemas XML en el servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
