---
title: "Comprender las diferencias entre la ejecución Local y remota | Documentos de Microsoft"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1921a7760e42f101ebf5d9b898972c2b2ab8173b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Descripción de las diferencias entre la ejecución local y remota
  Los desarrolladores y administradores de paquetes deben ser conscientes de que existen restricciones en cuanto a la ubicación donde se ejecuta un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Un paquete se ejecuta en el mismo equipo que el programa que lo inicia**. El paquete se ejecuta en el equipo local aunque un programa cargue un paquete almacenado de forma remota en otro servidor.  
  
-   **Sólo se puede ejecutar un paquete fuera del entorno de desarrollo en un equipo que tiene instalado servicios de integración**. No puede ejecutar paquetes fuera de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en un equipo cliente que no tenga instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], y puede que las condiciones de su licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no le permitan instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en equipos adicionales. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un componente de servidor y no se puede distribuir a los equipos cliente. Para ejecutar paquetes desde un equipo cliente, necesita iniciarlos de manera que se garantice que los paquetes se ejecutan en el servidor.  
  
 Para obtener más información sobre la carga y ejecución de un paquete guardado, vea:  
  
-   [Cargar y ejecutar un paquete local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Cargar y ejecutar un paquete remoto mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Para obtener más información sobre cómo ejecutar un paquete y cargar su salida en un programa personalizado, vea:  
  
-   [Cargar la salida de un paquete local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>Vea también  
 [Cargar y ejecutar un paquete Local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Cargar la salida de un paquete local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  

