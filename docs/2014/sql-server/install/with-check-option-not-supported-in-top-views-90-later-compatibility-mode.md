---
title: WITH CHECK OPTION no se admite en las vistas que contienen TOP en los modos de compatibilidad 90 o posteriores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ee7775c875e33f104341a1da39f5fe6c9326f284
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85011782"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>WITH CHECK OPTION no se admite en vistas que contengan TOP en el modo de compatibilidad 90 o superior
  El Asesor de actualizaciones detectó una vista que utiliza WITH CHECK OPTION y una cláusula TOP en la instrucción SELECT de la vista o en una vista a la que se hace referencia. Las vistas definidas de esta manera permiten, de forma errónea, que los datos se puedan modificar a través de la vista, lo que puede producir resultados imprecisos si el modo de compatibilidad de la base de datos se ha establecido en 80 o menos. Los datos no se pueden insertar o actualizar a través de una vista que utilice WITH CHECK OPTION cuando la vista o una vista a la que se hace referencia utilizan la cláusula TOP y el modo de compatibilidad de la base de datos está establecido en 90 o superior.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Cuando actualiza, las bases de datos de usuarios conservan su modo de compatibilidad. Antes de cambiar el modo de compatibilidad de la base de datos a 100 o superior, modifique las vistas que utilizan WITH CHECK OPTION y TOP si se desea permitir la modificación de datos a través de la vista. Para obtener más información, vea [sp_dbcmptlevel &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql).  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
