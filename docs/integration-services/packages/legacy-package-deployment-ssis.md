---
title: "Implementaci&#243;n de paquetes heredada (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "paquetes de Integration Services, implementar"
  - "implementar paquetes [Integration Services]"
  - "paquetes de SQL Server Integration Services, implementar"
  - "implementar paquetes [Integration Services], acerca de la implementación de paquetes"
  - "paquetes [Integration Services], implementar"
  - "paquetes SSIS, implementar"
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# Implementaci&#243;n de paquetes heredada (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye herramientas y asistentes para facilitar la implementación de paquetes del equipo de desarrollo en el servidor de producción o en otros equipos.  
  
 El proceso de implementación de paquetes consta de cuatro pasos:  
  
1.  El primer paso es opcional e implica crear configuraciones de paquetes que actualizan las propiedades de los elementos de los paquetes en tiempo de ejecución. Las configuraciones se incluyen automáticamente al implementar los paquetes.  
  
2.  El segundo paso es generar el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para crear una utilidad de implementación de paquetes. La utilidad de implementación del proyecto contiene los paquetes que desea implementar.  
  
3.  El tercer paso es copiar la carpeta de implementación que se creó al generar el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el equipo de destino.  
  
4.  El cuarto paso es ejecutar en el equipo de destino el Asistente para la instalación de paquetes con el fin de instalar los paquetes en el sistema de archivos o en una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Tareas relacionadas  
 Para obtener información sobre cómo crear una utilidad de implementación, vea [Crear una utilidad de implementación](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Para obtener información sobre cómo implementar paquetes mediante la utilidad de implementación, vea [Implementar los paquetes mediante la utilidad de implementación](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 Para obtener información sobre cómo crear configuraciones de paquete, vea [Crear configuraciones de paquetes](../../integration-services/packages/create-package-configurations.md).  
  
  