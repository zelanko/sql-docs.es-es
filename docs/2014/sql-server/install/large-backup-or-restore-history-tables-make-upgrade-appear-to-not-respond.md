---
title: Las tablas de historial de restauración o copia de seguridad de gran tamaño parecen no responder | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4d994eb6d345ab98e6cd51a44c7c90a74bafd3a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70874601"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>Las tablas de historial de restauración o copia de seguridad de gran tamaño hacen que la actualización aparentemente no responda
  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se han agregado nuevas columnas a algunas de las tablas de historial de restauración y copia de seguridad. Al actualizar estas tablas, es necesario modificarlas para agregar las nuevas columnas. Si una o varias de estas tablas contienen un gran número de filas, la actualización se detendrá durante un periodo de tiempo importante cuando se ejecute la instrucción ALTER TABLE que agrega las columnas a esa tabla.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Puede parecer que la actualización deja de responder si alguna de las siguientes tablas de historial de copias de seguridad o restauración contiene un gran número de filas:  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 Si alguna de estas tablas tiene 10.000 o más filas, el Asesor de actualizaciones notificará que se ha producido un error al no poder cumplir con su tarea. No notificará qué tabla supera el número permitido de filas. La primera tabla que supere las 10.000 filas generará el error.  
  
## <a name="corrective-action"></a>Acción correctora  
 Antes de actualizar una base de datos, si alguna de estas tablas supera las 10.000 filas, recomendamos reducir su número a menos de 10.000 filas. Para reducir las filas de todas estas tablas, puede ejecutar el **sp_delete_backuphistory** procedimiento almacenado. Este procedimiento elimina las entradas de todas las tablas de historial de restauración y copia de seguridad correspondientes a los conjuntos de copia de seguridad que sean anteriores a una fecha dada. Para más información, vea [sp_delete_backuphistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql).  
  
> [!NOTE]  
>  Puede actualizar una base de datos cuyas tablas de historial de restauración y copia de seguridad tengan más de 10.000 filas. Sin embargo, puede parecer que la actualización se detiene mientras se modifican esas tablas de gran tamaño. Cuanto mayor sea el tamaño de las tablas, más tiempo necesitará el programa de instalación para completar el proceso.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
