---
title: Recuperar archivos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 548fac7dbc7d1f2750a130da9847be406361d8bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843671"
---
# <a name="retrieve-files"></a>Recuperar archivos
  Después de haber abierto un proyecto controlado por código fuente, puede utilizar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para recuperar copias locales de los archivos del proyecto desde el almacén de control de código fuente en el directorio local en el que reside el proyecto.  
  
 Puede usar el control de código fuente integrado para recuperar archivos de varias formas:  
  
-   **Obtener la última versión (recursivo)** comando  
  
     Recupera la última versión protegida de los archivos seleccionados. Si se selecciona una solución o un proyecto, este comando recupera la última versión de todos los archivos de la solución y el proyecto.  
  
-   **Obtener** comando  
  
     Muestra el **obtener** cuadro de diálogo que puede usar para recuperar la versión más reciente de un archivo seleccionado, o para recuperar un subconjunto de los archivos de la solución o proyecto seleccionado.  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>Para recuperar la última versión de todos los archivos de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el proyecto.  
  
2.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **obtener última versión (recursivo)**.  
  
 Se recuperan las versiones más recientes de los archivos del proyecto en la ubicación del proyecto en el disco local.  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>Para recuperar únicamente algunos archivos de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el elemento que desea recuperar.  
  
2.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **obtener**.  
  
3.  En el **obtener** cuadro de diálogo, haga clic en **Aceptar**. Si ha seleccionado una solución o un proyecto en el Explorador de soluciones, también puede desactivar las casillas que aparecen junto a los elementos que no desea recuperar.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo obtener &#40;Control de código fuente&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [Establecer y recuperar información de versión](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [Ver el historial de proyecto](../../2014/database-engine/view-project-history.md)   
 [Ver el estado de archivo](../../2014/database-engine/view-file-status.md)  
  
  
