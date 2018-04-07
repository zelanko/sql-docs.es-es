---
title: Actualizar desde la base de datos (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eff823289c1d28bab1d009eb9fffdb3d7fa88b21
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="refresh-from-database-accesstosql"></a>Actualizar desde la base de datos (AccessToSQL)
El **actualizar desde la base de datos** cuadro de diálogo permite seleccionar los objetos que desea actualizar desde la base de datos de Access. Filas en el cuadro de diálogo están codificadas mediante colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de Access, la fila es azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de Access, pero no en SSMA, la fila está de color amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de Access, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de Access, la fila será rosa.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto &#40;cargar objetos&#41; &#40;AccessToSQL&#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para tener acceso a la **actualizar desde la base de datos** diálogo cuadro, haga clic en cualquier **base de datos** nodo en el Explorador de metadatos de acceso y haga clic en **actualizar desde la base de datos**.  
  
