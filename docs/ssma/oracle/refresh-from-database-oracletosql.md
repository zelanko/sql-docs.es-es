---
title: Actualizar desde la base de datos (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 536fa920910c56698be8b161f59294f555747917
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="refresh-from-database-oracletosql"></a>Actualizar desde la base de datos (OracleToSQL)
El **actualizar desde la base de datos** cuadro de diálogo permite seleccionar los objetos que desea actualizar desde la base de datos de Oracle. Filas en el cuadro de diálogo están codificadas mediante colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de Oracle, la fila es azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de Oracle, pero no en SSMA, la fila está de color amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de Oracle, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de Oracle, la fila será rosa.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, vea [configuración del proyecto &#40; Sincronización &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
Para tener acceso a la **actualizar desde la base de datos** cuadro de diálogo, haga un objeto en el Explorador de metadatos de Oracle y haga clic en **actualizar desde la base de datos**.  
  
## <a name="options"></a>Opciones  
**Contraer (-)**  
Contraer todos los grupos de objetos para ocultar objetos individuales.  
  
**Expandir (+)**  
Expandir todos los grupos de objetos para mostrar los objetos individuales.  
  
**Mostrar u ocultar objetos iguales**  
Oculta los objetos de la lista si los metadatos del objeto son el mismo en la base de datos de Oracle y de SSMA.  
  
**Actualizar desde la base de datos (botón de flecha)**  
Use el botón de flecha para especificar que se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Hacer no actualizar desde base de datos (X botón)**  
Use el botón X para especificar que no se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Leyenda**  
Muestra un **leyenda** cuadro de diálogo. La leyenda contiene la asignación entre los Estados de metadatos y los colores de la fila.  
  
Para mantener la **leyenda** cuadro de diálogo en la parte superior de la **actualizar desde la base de datos** cuadro de diálogo, seleccione la **mostrar en la parte superior** casilla de verificación.  
  

