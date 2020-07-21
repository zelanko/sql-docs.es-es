---
title: Cambios en el comportamiento de string-length y substring | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1188823a877b4c5dc9cef13431492dfe3b303e23
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85044997"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Cambios en el comportamiento de longitud de cadena y subcadena
  La [función de longitud de cadena &#40;&#41;XQuery](/sql/xquery/functions-on-string-values-string-length) y la [función Substring &#40;funciones&#41;XQuery](/sql/xquery/functions-on-string-values-substring) pueden devolver resultados diferentes cuando se utilizan con bases de datos XML que contienen caracteres suplentes.  
  
## <a name="description"></a>Description  
 Cuando una base de datos está configurada para ser compatible con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , el comportamiento de la [función de longitud de cadena &#40;&#41;XQuery](/sql/xquery/functions-on-string-values-string-length) y la [función Substring &#40;](/sql/xquery/functions-on-string-values-substring) los cambios en las funciones&#41;de XQuery cuando se trabaja con caracteres adicionales de Unicode. Estas funciones consideran cada carácter suplementario Unicode, que se define por tener un punto de código superior a U+FFFF, como un carácter en lugar de dos, como sucedía en versiones anteriores.  
  
 Para obtener más información sobre los caracteres suplentes, vea el tema sobre [caracteres suplementarios y suplentes](https://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
