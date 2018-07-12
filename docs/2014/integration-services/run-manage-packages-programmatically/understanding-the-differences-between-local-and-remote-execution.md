---
title: Descripción de las diferencias entre la ejecución local y remota | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 946419fddf2e66afc7b3182e06c6dfa5b35385fc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170946"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Descripción de las diferencias entre la ejecución local y remota
  Los desarrolladores y administradores de paquetes deben ser conscientes de que existen restricciones en cuanto a la ubicación donde se ejecuta un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Un paquete se ejecuta en el mismo equipo que el programa que lo inicia**. El paquete se ejecuta en el equipo local aunque un programa cargue un paquete almacenado de forma remota en otro servidor.  
  
-   **Solo puede ejecutar un paquete fuera del entorno de desarrollo en un equipo con Integration Services instalado**. No puede ejecutar paquetes fuera de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en un equipo cliente que no tenga instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], y puede que las condiciones de su licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no le permitan instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en equipos adicionales. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un componente de servidor y no se puede distribuir entre equipos cliente. Para ejecutar paquetes desde un equipo cliente, necesita iniciarlos de manera que se garantice que los paquetes se ejecutan en el servidor.  
  
 Para obtener más información sobre la carga y ejecución de un paquete guardado, vea:  
  
-   [Cargar y ejecutar un paquete local mediante programación](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Cargar y ejecutar un paquete remoto mediante programación](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Para obtener más información sobre cómo ejecutar un paquete y cargar su salida en un programa personalizado, vea:  
  
-   [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Cargar y ejecutar un paquete local mediante programación](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
