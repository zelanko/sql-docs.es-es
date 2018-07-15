---
title: 'Lección 1: Preparar la creación del conjunto de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dae41d24d9aa2637b0276e8e13caa5249e069b80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266713"
---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>Lección 1: Preparar la creación del paquete de implementación
  En esta lección, creará las carpetas de trabajo y la variables de entorno que admiten el tutorial, creará un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , agregará varios paquetes y sus archivos auxiliares al proyecto e implementará las configuraciones en los paquetes.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] implementa paquetes según un proyecto; por tanto, en el primer paso de la creación del paquete de implementación, debe recopilar todos los paquetes y sus dependencias en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . En muchas ocasiones, esto es útil para incluir otra información con los paquetes implementados: por ejemplo, también agregará un archivo Léame al proyecto que proporcione la documentación básica de este grupo de paquetes.  
  
 Después de agregar los paquetes y archivos, agregará configuraciones a los paquetes que todavía no usan configuraciones. Las configuraciones actualizan las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. En una lección posterior, modificará los valores de estas configuraciones durante la implementación de paquetes para que admitan los paquetes en el entorno implementado.  
  
 Después de agregar estas configuraciones, debe abrir los paquetes en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] , la herramienta gráfica de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para generar paquetes ETL, y examinar las propiedades de los paquetes y sus elementos, así como las configuraciones de paquetes para entender mejor los problemas que la implementación de paquetes debe controlar. Por ejemplo, uno de los paquetes extrae datos de archivos de texto, por lo que la ubicación de los archivos de datos debe actualizarse antes de que se ejecuten correctamente los paquetes implementados.  
  
 **Tiempo estimado para completar esta lección:** 1 hora  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: crear carpetas de trabajo y variables de entorno](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [Paso 2: Crear el proyecto de implementación](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [Paso 3: Agregar paquetes y otros archivos](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [Paso 4: Agregar configuraciones de paquetes](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [Paso 5: Probar los paquetes actualizados](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
 [Paso 1: Crear carpetas de trabajo y variables de entorno](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services  **<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
