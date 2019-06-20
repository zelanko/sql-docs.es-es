---
title: Administrar desprotecciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], checkouts
- checkouts [SQL Server Management Studio]
- checking out files
ms.assetid: ddd4adba-d432-4005-9cb2-bb9ee3163d8e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9de9a1f8ceca0fbb05ab2b6680c5fcc34c951109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774539"
---
# <a name="manage-checkouts"></a>Administrar desprotecciones
  Una vez que un archivo se ha agregado al control de código fuente, es necesario desprotegerlo antes de poder modificarlo. Cuando se desprotege un archivo del control de código fuente, el proveedor de control de código fuente crea una copia de la última versión en el disco local y quita el atributo de solo lectura del archivo. En algunas circunstancias, quizás sea necesario modificar un archivo sin desprotegerlo. Para obtener más información acerca de cómo editar un archivo sin desprotegerlo, vea [editar archivos protegidos](../../2014/database-engine/edit-checked-in-files.md).  
  
 Puede usar [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] desproteger los archivos de forma manual o automática. Desproteger los archivos manualmente, abra la solución que contiene los archivos en el [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] entorno y, a continuación, haga clic en el **desproteger** comando. Puede desproteger archivos de forma automática si se configura el entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para que lo haga.  
  
 Según las opciones que el administrador establezca en el proveedor de control de código fuente, también podrá desproteger archivos en modo exclusivo o compartido. Si desprotege un archivo en modo exclusivo, solo usted puede modificarlo y ningún otro usuario podrá desprotegerlo hasta que usted lo vuelva a proteger. Si desprotege un archivo en modo compartido, cualquier usuario podrá desprotegerlo. A medida que cada usuario protege el archivo, el proveedor de control de código fuente intenta combinarlo con la última versión del servidor. Si surgen contradicciones entre la versión que se está protegiendo y la última, el proveedor de control de código fuente pide al usuario que solucione el conflicto.  
  
 En la tabla siguiente se describen los temas de esta sección.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Desproteger archivos](../../2014/database-engine/check-out-files.md)|Proporciona instrucciones sobre cómo desproteger un archivo para modificarlo.|  
|[Deshacer desprotecciones](../../2014/database-engine/undo-checkouts.md)|Explica cómo cancelar una desprotección existente.|  
|[Desproteger archivos automáticamente durante la modificación](../../2014/database-engine/automatically-check-out-files-upon-edit.md)|Explica cómo configurar el control de código fuente para desproteger un archivo al comenzar a modificarlo.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar protecciones](../../2014/database-engine/manage-checkins.md)   
 [Modificar archivos protegidos](../../2014/database-engine/edit-checked-in-files.md)  
  
  
