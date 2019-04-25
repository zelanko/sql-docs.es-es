---
title: 'Lección 3: Instalación de paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da763e2385c64a09279c9dd6ff537993c2cd6a30
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767577"
---
# <a name="lesson-3-installing-packages"></a>Lección 3: Instalación de paquetes
  En la [Lección 2: Crear el paquete de implementación](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md), ha generado una utilidad de implementación y ha creado el paquete de implementación que contiene los elementos que debe instalar los paquetes en otro equipo. También ha comprobado la lista de archivos en el paquete de implementación y ha examinado el contenido del archivo de manifiesto que se creó al generar la utilidad de implementación.  
  
 En esta lección, copiará el paquete de implementación en el equipo de destino y, a continuación, ejecutará el Asistente para la instalación de paquetes para instalar los paquetes, sus dependencias y los archivos auxiliares en ese equipo. Los paquetes se instalarán en la base de datos **de**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los otros elementos se instalarán en el sistema de archivos. Después de completar la instalación de los paquetes, para probar la implementación, ejecutará los paquetes desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] con la Utilidad de ejecución de paquetes.  
  
 **Tiempo estimado para completar esta lección:** 30 minutos  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copia del paquete de implementación](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [Paso 2: Ejecución del Asistente para la instalación de paquetes](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [Paso 3: Prueba de los paquetes implementados](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
 [Paso 1: Copia del paquete de implementación](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
