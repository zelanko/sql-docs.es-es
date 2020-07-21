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
ms.openlocfilehash: 4176ee1dff35a0f9eaeaddf1b35155f76de526ef
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929476"
---
# <a name="retrieve-files"></a>Recuperar archivos
  Después de haber abierto un proyecto controlado por código fuente, puede utilizar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para recuperar copias locales de los archivos del proyecto desde el almacén de control de código fuente en el directorio local en el que reside el proyecto.  
  
 Puede usar el control de código fuente integrado para recuperar archivos de varias formas:  
  
-   Comando **obtener la última versión (recursivo)**  
  
     Recupera la última versión protegida de los archivos seleccionados. Si se selecciona una solución o un proyecto, este comando recupera la última versión de todos los archivos de la solución y el proyecto.  
  
-   **Get** (comando)  
  
     Muestra el cuadro de diálogo **obtener** , que puede usar para recuperar la versión más reciente de un archivo seleccionado o para recuperar un subconjunto de los archivos de la solución o proyecto seleccionados.  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>Para recuperar la última versión de todos los archivos de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el proyecto.  
  
2.  En el menú **archivo** , seleccione **control de código fuente**y, a continuación, haga clic en **obtener la última versión (recursivo)**.  
  
 Se recuperan las versiones más recientes de los archivos del proyecto en la ubicación del proyecto en el disco local.  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>Para recuperar únicamente algunos archivos de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el elemento que desea recuperar.  
  
2.  En el menú **archivo** , seleccione **control de código fuente**y, a continuación, haga clic en **obtener**.  
  
3.  En el cuadro de diálogo **obtener** , haga clic en **Aceptar**. Si ha seleccionado una solución o un proyecto en el Explorador de soluciones, también puede desactivar las casillas que aparecen junto a los elementos que no desea recuperar.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo obtener &#40;control de código fuente&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [Establecer y recuperar información de versión](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [Ver el historial del proyecto](../../2014/database-engine/view-project-history.md)   
 [Ver el estado de archivo](../../2014/database-engine/view-file-status.md)  
  
  
