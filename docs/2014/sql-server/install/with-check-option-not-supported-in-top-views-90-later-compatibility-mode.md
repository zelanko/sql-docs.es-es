---
title: WITH CHECK OPTION no se admite en las vistas que contienen TOP en los modos de compatibilidad 90 o posterior | Microsoft Docs
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
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
caps.latest.revision: 14
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8c64ce7395b5ecbb33530672d93817f7938db6d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244003"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>WITH CHECK OPTION no se admite en vistas que contengan TOP en el modo de compatibilidad 90 o superior
  El Asesor de actualizaciones detectó una vista que utiliza WITH CHECK OPTION y una cláusula TOP en la instrucción SELECT de la vista o en una vista a la que se hace referencia. Las vistas definidas de esta manera permiten, de forma errónea, que los datos se puedan modificar a través de la vista, lo que puede producir resultados imprecisos si el modo de compatibilidad de la base de datos se ha establecido en 80 o menos. Los datos no se pueden insertar o actualizar a través de una vista que utilice WITH CHECK OPTION cuando la vista o una vista a la que se hace referencia utilizan la cláusula TOP y el modo de compatibilidad de la base de datos está establecido en 90 o superior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Cuando actualiza, las bases de datos de usuarios conservan su modo de compatibilidad. Antes de cambiar el modo de compatibilidad de la base de datos a 100 o superior, modifique las vistas que utilizan WITH CHECK OPTION y TOP si se desea permitir la modificación de datos a través de la vista. Para obtener más información, consulte [sp_dbcmptlevel &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
