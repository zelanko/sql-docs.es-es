---
title: WITH ROWS no se admite en las instrucciones CREATE STATISTICs en el modo de compatibilidad de 90 o posterior | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- WITH ROWS in CREATE STATISTICS statement
ms.assetid: 197b2ecf-a1a3-4a3a-a523-a0ee919c1dde
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e48602f61c09a8de76e2894a4fa808b2f39f4cbe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66090966"
---
# <a name="with-rows-is-not-supported-in-create-statistics-statements-in-the-compatibility-mode-of-90-or-later"></a>No se admite WITH ROW en instrucciones CREATE STATISTICS en el modo de compatibilidad de 90 o superior
  No se admite el uso de WITH ROWS en instrucciones CREATE STATISTICS si se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el modo de compatibilidad establecido en 90 o más.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las instrucciones CREATE STATISTICs que incluyan WITH ROWS especificando con filas de *número* de muestra o especificando otras opciones que cumplan con la sintaxis documentada. Para obtener más información, vea el tema "CREATE STATISTICs (Transact-SQL) en Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
