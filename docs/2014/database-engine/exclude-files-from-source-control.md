---
title: Excluir archivos de Control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b3507f06db699e8e88de2fe2e22f870b97b896e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330445"
---
# <a name="exclude-files-from-source-control"></a>Excluir archivos desde el control de código fuente
  Si la solución que está trabajando contiene archivos que no requieren servicios de control de código fuente, puede usar el **excluir del Control de código fuente** comando para excluir el archivo de control de código fuente. Al hacer esto, el archivo permanece en la base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, aunque ya no se protege ni desprotege con el proyecto.  
  
 Debe usar el **excluir del Control de código fuente** comando solo en los archivos generados. Un archivo generado es aquel que se puede volver a crear íntegramente [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] según el contenido de otro archivo en la solución.  
  
### <a name="to-exclude-a-file-from-source-control"></a>Para excluir un archivo del control de código fuente  
  
1.  En el Explorador de soluciones, seleccione el archivo que desea excluir.  
  
2.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **excluir**  *\<nombre de archivo >* **desde Control de código fuente**.  
  
## <a name="see-also"></a>Vea también  
 [Fundamentos del Control de código fuente](../../2014/database-engine/source-control-basics.md)   
 [Establecer opciones de Control de código fuente](../../2014/database-engine/set-source-control-options.md)   
 [Cambiar las conexiones del control de código fuente](../../2014/database-engine/change-source-control-connections.md)  
  
  
