---
title: Actualizar desde la base de datos (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3b671f49-c4cc-44fd-801e-e738a8c79415
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 820ed13c81d13d0b80450d9ad8bd08359c8c0d3d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="refresh-from-database-accesstosql"></a>Actualizar desde la base de datos (AccessToSQL)
El **actualizar desde la base de datos** cuadro de diálogo permite seleccionar los objetos que desea actualizar desde la base de datos de Access. Filas en el cuadro de diálogo están codificadas mediante colores en función del estado de los metadatos:  
  
-   Si los metadatos del objeto ha cambiado localmente y en la base de datos de Access, la fila es azul.  
  
-   Si los metadatos del objeto ha cambiado en la base de datos de Access, pero no en SSMA, la fila está de color amarilla.  
  
-   Si los metadatos del objeto ha cambiado localmente, pero no en la base de datos de Access, la fila es verde.  
  
-   Si el objeto es nuevo en la base de datos de Access, la fila será rosa.  
  
Puede especificar la configuración de actualización de objeto predeterminado en el **configuración del proyecto** cuadro de diálogo. Para obtener más información, vea [configuración del proyecto &#40; Cargar objetos &#41; &#40; AccessToSQL &#41;](../../ssma/access/project-settings-loading-objects-accesstosql.md)  
  
Para tener acceso a la **actualizar desde la base de datos** diálogo cuadro, haga clic en cualquier **base de datos** nodo en el Explorador de metadatos de acceso y haga clic en **actualizar desde la base de datos**.  
  

