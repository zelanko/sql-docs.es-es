---
title: Cambiar las conexiones del Control de código fuente | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connections [SQL Server Management Studio], source controls
- source controls [SQL Server Management Studio], connections
ms.assetid: 538e3beb-f99c-4095-bd65-6413e872d26e
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bb9453806d27f55cf081eb1196e886cecf1789c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106192"
---
# <a name="change-source-control-connections"></a>Cambiar las conexiones del control de código fuente
  La primera vez que se agrega una solución al control de código fuente o se abre desde él, el proveedor de control de código fuente crea una asociación entre la carpeta raíz del directorio local de la solución y su correspondiente carpeta del servidor.  
  
 La carpeta raíz (también denominada raíz unificada) reside en el cliente. Es la carpeta en la que se pueden encontrar todos los archivos a los que hace referencia una solución o un proyecto. Para buscar la última versión de una solución, su historial y su información de estado, busque la carpeta del servidor, que reside en el servidor de control de código fuente. En [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, las carpetas del servidor se denominan proyectos.  
  
 En muchas situaciones, es necesario anular el enlace o desconectar una solución de su carpeta del servidor. Por ejemplo, si el equipo en el que reside el proveedor de control de código fuente no está disponible, es posible conectar a un equipo auxiliar, volver a enlazar la solución a una carpeta del servidor con copia de seguridad y seguir trabajando normalmente. Además, si un proyecto de control de código fuente está bifurcado, quizás tenga que enlazar la solución a la carpeta del servidor en que reside la nueva versión del proyecto.  
  
 Utilice la interfaz de usuario del proveedor de control de código fuente para cambiar la carpeta del servidor a la que está enlazada una solución. Puede abrir la interfaz de usuario del control de código fuente desde el entorno de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-open-the-source-control-user-interface-from-the-studio-environment"></a>Para abrir la interfaz de usuario del control de código fuente desde el entorno de Visual Studio  
  
1.  En el **archivo** menú, elija **Control de código fuente**y, a continuación, haga clic en **iniciar Microsoft Visual SourceSafe**.  
  
## <a name="see-also"></a>Vea también  
 [Fundamentos del Control de código fuente](../../2014/database-engine/source-control-basics.md)   
 [Establecer opciones de Control de código fuente](../../2014/database-engine/set-source-control-options.md)   
 [Excluir archivos de Control de código fuente](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  