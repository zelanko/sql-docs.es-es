---
title: Quitar dos puntos después de la palabra clave reservada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fc6882439338509a3c716129d9504f209ab1e555
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065197"
---
# <a name="remove-colon-following-reserved-keyword"></a>Quitar los dos puntos que siguen a las palabras claves reservadas
  El Asesor de actualizaciones detectó un script que contiene dos puntos (:) después de una palabra clave reservada. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta sintaxis no se tenía en cuenta y las instrucciones se ejecutaban correctamente. Ahora, esta sintaxis hace que la instrucción no se pueda ejecutar si el modo de compatibilidad de la base de datos está establecido en 100 o más.  
  
 Las bases de datos de usuario mantienen su modo de compatibilidad.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de cambiar el modo de compatibilidad de la base de datos a 100 o más, modifique sus scripts quitando los dos puntos que siguen a las palabras clave reservadas. Para obtener más información, vea "sp_dbcmptlevel" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
