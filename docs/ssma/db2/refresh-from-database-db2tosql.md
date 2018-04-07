---
title: Actualizar desde la base de datos (DB2ToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
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
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 421c86c9b8b61c95d5221c7ca28af9762a530778
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="refresh-from-database-db2tosql"></a>Actualizar desde la base de datos (DB2ToSQL)
El **actualizar desde la base de datos** cuadro de diálogo permite seleccionar los objetos que desea actualizar desde la base de datos DB2. Filas en el cuadro de diálogo están codificadas mediante colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de DB2, la fila es azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de DB2, pero no en SSMA, la fila está de color amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de DB2, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de DB2, la fila será rosa.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto&#40;sincronización&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Para tener acceso a la **actualizar desde la base de datos** cuadro de diálogo, haga un objeto en el Explorador de metadatos de DB2 y haga clic en **actualizar desde la base de datos**.  
  
## <a name="options"></a>Opciones  
**Contraer (-)**  
Contraer todos los grupos de objetos para ocultar objetos individuales.  
  
**Expandir (+)**  
Expandir todos los grupos de objetos para mostrar los objetos individuales.  
  
**Mostrar u ocultar objetos iguales**  
Oculta los objetos de la lista si los metadatos del objeto son el mismo en la base de datos de DB2 y de SSMA.  
  
**Actualizar desde la base de datos (botón de flecha)**  
Use el botón de flecha para especificar que se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Hacer no actualizar desde base de datos (X botón)**  
Use el botón X para especificar que no se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Leyenda**  
Muestra un **leyenda** cuadro de diálogo. La leyenda contiene la asignación entre los Estados de metadatos y los colores de la fila.  
  
Para mantener la **leyenda** cuadro de diálogo en la parte superior de la **actualizar desde la base de datos** cuadro de diálogo, seleccione la **mostrar en la parte superior** casilla de verificación.  
  
