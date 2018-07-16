---
title: Tablas de historial de copia de seguridad o restauración grandes hacen que la actualización aparentemente no responda | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d01d73f9456d56a8f12698b954213289ab4921d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208505"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>Las tablas de historial de restauración o copia de seguridad de gran tamaño hacen que la actualización aparentemente no responda
  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], se han agregado nuevas columnas a algunas de las tablas de historial de restauración y copia de seguridad. Al actualizar estas tablas, es necesario modificarlas para agregar las nuevas columnas. Si una o varias de estas tablas contienen un gran número de filas, la actualización se detendrá durante un periodo de tiempo importante cuando se ejecute la instrucción ALTER TABLE que agrega las columnas a esa tabla.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Puede parecer que la actualización deja de responder si alguna de las siguientes tablas de historial de restauración o copia de seguridad contiene gran cantidad de filas:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
