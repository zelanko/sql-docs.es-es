---
title: Actualizar desde la base de datos (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 49595bb772d2ac5cd49be9f67c9004f2f0e1e098
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-from-database-mysqltosql"></a>Actualizar desde la base de datos (MySQLToSQL)
El **actualizar desde la base de datos** cuadro de diálogo permite seleccionar los objetos que desea actualizar desde la base de datos de MySQL. Filas en el cuadro de diálogo están codificadas mediante colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos MySQL, la fila es azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos MySQL, pero no en SSMA, la fila está de color amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos MySQL, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos MySQL, la fila será rosa.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto &#40;sincronización&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Para tener acceso a la **actualizar desde la base de datos** cuadro de diálogo, haga un objeto en el Explorador de metadatos de MySQL y haga clic en **actualizar desde la base de datos**.  
  
## <a name="options"></a>Opciones  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Contraer (-)**|Contraer todos los grupos de objetos para ocultar objetos individuales.|  
|**Expandir (+)**|Expandir todos los grupos de objetos para mostrar los objetos individuales.|  
|**Mostrar u ocultar objetos iguales**|Oculta los objetos de la lista si los metadatos del objeto son el mismo en la base de datos MySQL y SSMA.|  
|**Actualizar desde la base de datos (botón de flecha)**|Use el botón de flecha para especificar que se deben actualizar los metadatos de los objetos seleccionados en SSMA.|  
|**Hacer no actualizar desde base de datos (X botón)**|Use el botón X para especificar que no se deben actualizar los metadatos de los objetos seleccionados en SSMA.|  
|**Leyenda**|Muestra un **leyenda** cuadro de diálogo. La leyenda contiene la asignación entre los Estados de metadatos y los colores de la fila.<br /><br />Para mantener la **leyenda** cuadro de diálogo en la parte superior de la **actualizar desde la base de datos** cuadro de diálogo, seleccione la **mostrar en la parte superior** casilla de verificación.|  
  
