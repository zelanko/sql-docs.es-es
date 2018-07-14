---
title: Constantes de gran tamaño están tipificadas como tipos de valores grandes en los modos de compatibilidad 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
caps.latest.revision: 17
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 59f9afc3c8f083da2c1d3934d5aea5b541c6c527
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37257771"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>Las constantes de gran tamaño están tipificadas como tipos de valor grande en los modos de compatibilidad 90 o superiores
  El Asesor de actualizaciones ha detectado la presencia de constantes grandes. Las constantes de cadena de caracteres y las constantes binarias cuyo tamaño sea superior a 8.000 bytes se tratan como tipos de datos de objetos grandes en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, las constantes de cadena de caracteres de gran tamaño, Unicode y binarias están tipificadas como tipos de valor grande.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Cuando se utilizan las funciones de cadena, como CHARINDEX y PATINDEX, con cadenas o constantes binarias que superan los 8.000 bytes, [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] devuelve el número de error 8116, mientras que [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y las versiones posteriores devuelven el número de error 8152.  
  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], las funciones de cadena devuelven el error 8116 cuando se utilizan con los tipos de datos `text`, `ntext` e `image`.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, las constantes grandes se tratan como tipos de datos `varchar(max)`, `nvarchar(max)` y `varbinary(max)`, respectivamente. Estos tipos de datos son compatibles con funciones de cadena.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, las funciones de cadena, como CHARINDEX y PATINDEX, asumen que la cadena que contiene la secuencia de caracteres a buscar tienen menos de 8.000 bytes. Esta es la razón por la cual se produce el error 8152 con CHARINDEX y PATINDEX.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
