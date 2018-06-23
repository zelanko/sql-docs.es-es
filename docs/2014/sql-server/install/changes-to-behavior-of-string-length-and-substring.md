---
title: Cambia al comportamiento de longitud de la cadena y subcadena | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3bdc5e23a18b1b182703a1773dc8476eda8d4b14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197887"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Cambios en el comportamiento de longitud de cadena y subcadena
  El [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones pueden devolver resultados diferentes cuando se usa con las bases de datos XML que contienen caracteres suplentes.  
  
## <a name="description"></a>Descripción  
 Cuando una base de datos está establecida para ser compatible con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], el comportamiento de la [función string-length &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length) y [substring, función &#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring) funciones cambia cuando se trabaja con los caracteres Unicode suplementarios. Estas funciones consideran cada carácter suplementario Unicode, que se define por tener un punto de código superior a U+FFFF, como un carácter en lugar de dos, como sucedía en versiones anteriores.  
  
 Para obtener más información sobre los caracteres suplentes, vea el tema sobre [caracteres suplementarios y suplentes](http://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
