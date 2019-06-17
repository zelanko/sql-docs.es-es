---
title: Actualizar desde la base de datos (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 690d12a2f5f397256760c1c0cf5e2ee954d90843
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473901"
---
# <a name="refresh-from-database-mysqltosql"></a>Actualizar desde la base de datos (MySQLToSQL)
El **actualizar desde la base de datos** cuadro de diálogo le permite seleccionar los objetos que desea actualizar desde la base de datos MySQL. Las filas en el cuadro de diálogo están codificados con colores según el estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos MySQL, la fila está en azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos MySQL, pero no en SSMA, la fila está en amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos MySQL, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos MySQL, la fila es de color fucsia.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto &#40;sincronización&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
Para tener acceso a la **actualizar desde la base de datos** contextual de un objeto en el Explorador de metadatos de MySQL y haga clic en cuadro de diálogo **actualizar desde la base de datos**.  
  
## <a name="options"></a>Opciones  
  
|||  
|-|-|  
|**Término**|**Definición**|  
|**Contraer (-)**|Contraer todos los grupos de objetos para ocultar objetos individuales.|  
|**Expandir (+)**|Expandir todos los grupos de objeto para mostrar los objetos individuales.|  
|**Mostrar u ocultar objetos iguales**|Oculta los objetos de la lista si los metadatos del objeto son el mismo en la base de datos MySQL y de SSMA.|  
|**Actualizar desde la base de datos (botón de flecha)**|Utilice el botón de flecha para especificar que se deben actualizar los metadatos de los objetos seleccionados en SSMA.|  
|**Hacer no actualizar desde la base de datos (X botón)**|Use el botón X para especificar que no se deben actualizar los metadatos de los objetos seleccionados en SSMA.|  
|**Leyenda**|Muestra un **leyenda** cuadro de diálogo. La leyenda contiene la asignación entre los Estados de los metadatos y los colores de la fila.<br /><br />Para mantener la **leyenda** cuadro de diálogo en la parte superior de la **actualizar desde la base de datos** cuadro de diálogo, seleccione el **mostrar en la parte superior** casilla de verificación.|  
  
