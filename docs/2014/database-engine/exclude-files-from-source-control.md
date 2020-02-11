---
title: Excluir archivos del control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- excluding files from source control
- source controls [SQL Server Management Studio], file exclusions
ms.assetid: 7dcb6514-db5c-49eb-8b5a-2c766ce39aa7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 42ae16970e59e2eac1af68e54a38b19bd760c068
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62779905"
---
# <a name="exclude-files-from-source-control"></a>Excluir archivos desde el control de código fuente
  Si la solución en la que está trabajando contiene archivos que no requieren servicios de control de código fuente, puede usar el comando **excluir del control de código** fuente para excluir el archivo del control de código fuente. Al hacer esto, el archivo permanece en la base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, aunque ya no se protege ni desprotege con el proyecto.  
  
 Debe usar el comando **excluir del control de código fuente** solo en los archivos generados. Un archivo generado es aquél que puede volver a crearse por [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] completo según el contenido de otro archivo de la solución.  
  
### <a name="to-exclude-a-file-from-source-control"></a>Para excluir un archivo del control de código fuente  
  
1.  En el Explorador de soluciones, seleccione el archivo que desea excluir.  
  
2.  En el menú **archivo** , seleccione **control de código fuente**y, a continuación, haga clic en **excluir** * \<nombre de archivo>* **del control de código fuente**.  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos del control de código fuente](../../2014/database-engine/source-control-basics.md)   
 [Establecer opciones de control de código fuente](../../2014/database-engine/set-source-control-options.md)   
 [Cambiar las conexiones del control de código fuente](../../2014/database-engine/change-source-control-connections.md)  
  
  
