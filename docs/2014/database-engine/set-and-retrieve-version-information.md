---
title: Establecer y recuperar información de versión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0dde0359b67d34e712b76e53a855efaafc29b5b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265243"
---
# <a name="set-and-retrieve-version-information"></a>Establecer y recuperar información de versión
  La información de versión incluye el historial y el estado actual de un archivo controlado por código fuente. [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe conserva un historial completo de cada archivo controlado por código fuente, lo que permite realizar un seguimiento de la evolución de uno o más archivos a lo largo del tiempo. Además, esta información se puede utilizar para recuperar una copia local de cualquier versión del archivo o para comparar dos versiones cualesquiera.  
  
 El historial de un archivo incluye:  
  
-   El número de versión, que identifica su secuencia entre otras versiones del mismo archivo.  
  
-   La acción llevada a cabo. Las operaciones realizadas incluyen la creación del archivo, la protección y la eliminación.  
  
-   El nombre de usuario de la persona que realizó una acción con el archivo.  
  
-   La fecha y la hora en que se realizó la operación.  
  
 Visual SourceSafe también conserva información de estado actual sobre la solución cargada. Esta información proporciona una instantánea del estado actual del archivo, lo que incluye:  
  
-   La identidad del usuario que tiene desprotegido el archivo.  
  
-   El número de la última versión del archivo seleccionado.  
  
-   La fecha en la que se creó la versión.  
  
-   Los comentarios de usuario asociados a la versión.  
  
-   Las rutas de acceso a los proyectos que comparten el archivo.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Ver el historial de un archivo](../../2014/database-engine/view-file-history.md)  
  
-   [Ver el historial del proyecto](../../2014/database-engine/view-project-history.md)  
  
-   [Ver el estado de archivo](../../2014/database-engine/view-file-status.md)  
  
-   [Recuperar archivos](../../2014/database-engine/retrieve-files.md)  
  
-   [Especificar una versión como última versión](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [Comparar archivos](../../2014/database-engine/compare-files.md)  
  
-   [Compartir archivos](../../2014/database-engine/share-files.md)  
  
-   [Crear informes de historial y estado](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>Vea también  
 [Fundamentos del control de código fuente](../../2014/database-engine/source-control-basics.md)  
  
  
