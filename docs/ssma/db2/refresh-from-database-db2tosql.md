---
title: Actualizar desde la base de datos (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ef7778854248f194c01254b9cd6f833f67e9cefc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269999"
---
# <a name="refresh-from-database-db2tosql"></a>Actualizar desde la base de datos (DB2ToSQL)
El **actualizar desde la base de datos** cuadro de diálogo le permite seleccionar los objetos que desea actualizar desde la base de datos DB2. Las filas en el cuadro de diálogo están codificados con colores según el estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de DB2, la fila está en azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de DB2, pero no en SSMA, la fila está en amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de DB2, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de DB2, la fila es de color fucsia.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, consulte [configuración del proyecto&#40;sincronización&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
Para tener acceso a la **actualizar desde la base de datos** contextual de un objeto en el Explorador de metadatos de DB2 y haga clic en cuadro de diálogo **actualizar desde la base de datos**.  
  
## <a name="options"></a>Opciones  
**Contraer (-)**  
Contraer todos los grupos de objetos para ocultar objetos individuales.  
  
**Expandir (+)**  
Expandir todos los grupos de objeto para mostrar los objetos individuales.  
  
**Mostrar u ocultar objetos iguales**  
Oculta los objetos de la lista si los metadatos del objeto son el mismo en la base de datos de DB2 y de SSMA.  
  
**Actualizar desde la base de datos (botón de flecha)**  
Utilice el botón de flecha para especificar que se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Hacer no actualizar desde la base de datos (X botón)**  
Use el botón X para especificar que no se deben actualizar los metadatos de los objetos seleccionados en SSMA.  
  
**Leyenda**  
Muestra un **leyenda** cuadro de diálogo. La leyenda contiene la asignación entre los Estados de los metadatos y los colores de la fila.  
  
Para mantener la **leyenda** cuadro de diálogo en la parte superior de la **actualizar desde la base de datos** cuadro de diálogo, seleccione el **mostrar en la parte superior** casilla de verificación.  
  
