---
title: Quitar referencias a tablas del sistema no documentadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- undocumented system tables [SQL Server]
- system tables [SQL Server]
ms.assetid: 010b1236-2219-4bf4-a6db-e3fc3abfa37a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06249aa1849a1be9af40e183724e85b0f318f3dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093146"
---
# <a name="remove-references-to-undocumented-system-tables"></a>Quitar referencias a tablas del sistema no documentadas
  Muchas tablas del sistema que no estaban documentadas en las versiones anteriores han cambiado o ya no existen; por consiguiente, si se utilizan dichas tablas, se pueden producir errores tras la actualización. Dado que el Asesor de actualizaciones busca referencias a nombres de tablas del sistema, le informará sobre aquellas referencias a tablas del usuario que tengan el mismo nombre que una tabla del sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las siguientes tablas del sistema no documentadas se han quitado:  
  
-   **spt_datatype_info**  
  
-   **spt_datatype_info_ext**  
  
-   **spt_provider_types**  
  
-   **spt_server_info**  
  
-   **spt_values**  
  
-   **sysfulltextnotify**  
  
-   **syslocks**  
  
-   **sysproperties**  
  
-   **sysprotects_aux**  
  
-   **sysprotects_view**  
  
-   **SYSREMOTE_CATALOGS**  
  
-   **SYSREMOTE_COLUMN_PRIVILEGES**  
  
-   **SYSREMOTE_COLUMNS**  
  
-   **SYSREMOTE_FOREIGN_KEYS**  
  
-   **SYSREMOTE_INDEXES**  
  
-   **SYSREMOTE_PRIMARY_KEYS**  
  
-   **SYSREMOTE_PROVIDER_TYPES**  
  
-   **SYSREMOTE_SCHEMATA**  
  
-   **SYSREMOTE_STATISTICS**  
  
-   **SYSREMOTE_TABLE_PRIVILEGES**  
  
-   **SYSREMOTE_TABLES**  
  
-   **SYSREMOTE_VIEWS**  
  
-   **syssegments**  
  
-   **sysxlogins**  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique las aplicaciones según la tabla siguiente.  
  
|En lugar de|Uso|  
|----------------|---------|  
|**sysfulltextnotify**|Propiedad **TableFulltextPendingChanges** de la función OBJECTPROPERTYEX.|  
|**syslocks**|**Sys. dm_tran_locks** vista de administración dinámica, o sp_lock o la vista de compatibilidad **Sys. syslockinfo** .|  
|**sysproperties**|vista de catálogo **Sys. extended_properties** o la función **fn_ListExtendedProperty**|  
|**sysxlogins**|**Sys. server_principals** vista de catálogo o vista de compatibilidad **syslogins** .|  
|todas las tablas **spt_**|Ningún reemplazo disponible|  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
