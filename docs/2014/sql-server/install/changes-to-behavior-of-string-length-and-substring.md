---
title: Los cambios en el comportamiento de longitud de cadena y subcadena | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d5fad3b875e781f7682f7e381dbcd4b2db1b3b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48202892"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Cambios en el comportamiento de longitud de cadena y subcadena
  El [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones pueden devolver resultados diferentes cuando se usa con las bases de datos XML que contienen caracteres suplentes.  
  
## <a name="description"></a>Descripción  
 Cuando una base de datos se establece para ser compatible con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el comportamiento de la [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones cambia cuando se trabaja con caracteres suplementarios Unicode. Estas funciones consideran cada carácter suplementario Unicode, que se define por tener un punto de código superior a U+FFFF, como un carácter en lugar de dos, como sucedía en versiones anteriores.  
  
 Para obtener más información sobre los caracteres suplentes, vea el tema sobre [caracteres suplementarios y suplentes](http://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
