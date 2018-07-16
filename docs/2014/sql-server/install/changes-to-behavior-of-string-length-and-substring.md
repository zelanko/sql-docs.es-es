---
title: Los cambios en el comportamiento de longitud de cadena y subcadena | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
caps.latest.revision: 9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0261587f42bfa52f2a1db59ab76fefb0c8670be7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312885"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Cambios en el comportamiento de longitud de cadena y subcadena
  El [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones pueden devolver resultados diferentes cuando se usa con las bases de datos XML que contienen caracteres suplentes.  
  
## <a name="description"></a>Descripción  
 Cuando una base de datos se establece para ser compatible con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el comportamiento de la [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones cambia cuando se trabaja con caracteres suplementarios Unicode. Estas funciones consideran cada carácter suplementario Unicode, que se define por tener un punto de código superior a U+FFFF, como un carácter en lugar de dos, como sucedía en versiones anteriores.  
  
 Para obtener más información sobre los caracteres suplentes, vea el tema sobre [caracteres suplementarios y suplentes](http://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
