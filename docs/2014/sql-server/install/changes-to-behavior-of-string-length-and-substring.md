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
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66428847"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>Cambios en el comportamiento de longitud de cadena y subcadena
  La [función de longitud de cadena &#40;&#41;XQuery](/sql/xquery/functions-on-string-values-string-length) y la [función Substring &#40;funciones&#41;XQuery](/sql/xquery/functions-on-string-values-substring) pueden devolver resultados diferentes cuando se utilizan con bases de datos XML que contienen caracteres suplentes.  
  
## <a name="description"></a>Descripción  
 Cuando una base de datos está configurada [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]para ser compatible con, el comportamiento de la [función de longitud de cadena &#40;&#41;XQuery](/sql/xquery/functions-on-string-values-string-length) y la [función Substring &#40;](/sql/xquery/functions-on-string-values-substring) los cambios en las funciones&#41;de XQuery cuando se trabaja con caracteres adicionales de Unicode. Estas funciones consideran cada carácter suplementario Unicode, que se define por tener un punto de código superior a U+FFFF, como un carácter en lugar de dos, como sucedía en versiones anteriores.  
  
 Para obtener más información sobre los caracteres suplentes, vea el tema sobre [caracteres suplementarios y suplentes](https://go.microsoft.com/fwlink/?LinkId=178317).  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
