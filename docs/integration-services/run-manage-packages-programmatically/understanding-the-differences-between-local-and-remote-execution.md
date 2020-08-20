---
description: Descripción de las diferencias entre la ejecución local y remota
title: Descripción de las diferencias entre la ejecución local y remota | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- packages [Integration Services], troubleshooting
ms.assetid: 610ee7d9-4fea-4aba-9395-57add826923b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e9ed7d79855fdef0dfc64d37367ee7b8bc919ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495534"
---
# <a name="understanding-the-differences-between-local-and-remote-execution"></a>Descripción de las diferencias entre la ejecución local y remota

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Los desarrolladores y administradores de paquetes deben ser conscientes de que existen restricciones en cuanto a la ubicación donde se ejecuta un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   **Un paquete se ejecuta en el mismo equipo que el programa que lo inicia**. El paquete se ejecuta en el equipo local aunque un programa cargue un paquete almacenado de forma remota en otro servidor.  
  
-   **Solo puede ejecutar un paquete fuera del entorno de desarrollo en un equipo con Integration Services instalado**. No puede ejecutar paquetes fuera de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en un equipo cliente que no tenga instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], y puede que las condiciones de su licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no le permitan instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en equipos adicionales. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un componente de servidor y no se puede distribuir entre equipos cliente. Para ejecutar paquetes desde un equipo cliente, necesita iniciarlos de manera que se garantice que los paquetes se ejecutan en el servidor.  
  
 Para obtener más información sobre la carga y ejecución de un paquete guardado, vea:  
  
-   [Cargar y ejecutar un paquete local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
  
-   [Cargar y ejecutar mediante programación un paquete remoto](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
 Para obtener más información sobre cómo ejecutar un paquete y cargar su salida en un programa personalizado, vea:  
  
-   [Cargar la salida de un paquete local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
## <a name="see-also"></a>Consulte también  
 [Cargar y ejecutar un paquete local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Cargar la salida de un paquete local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
