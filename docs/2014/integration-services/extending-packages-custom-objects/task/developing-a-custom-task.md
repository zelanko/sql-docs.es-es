---
title: Desarrollar una tarea personalizada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7f597ee3a063da534267f7d4674a024a8fcc02f1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62896146"
---
# <a name="developing-a-custom-task"></a>Desarrollar una tarea personalizada
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa tareas para realizar unidades de trabajo con el fin de admitir la extracción, transformación y carga de datos. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye varias tareas que realizan las acciones usadas con más frecuencia, desde ejecutar una instrucción SQL hasta descargar un archivo de un sitio FTP. Si las tareas incluidas y las acciones compatibles no cumplen completamente sus requisitos, puede crear una tarea personalizada.  
  
 Para crear una tarea personalizada, debe crear una clase que herede de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, aplicar el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a la nueva clase e invalidar los métodos y propiedades importantes de la clase base, incluido el método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
## <a name="in-this-section"></a>En esta sección  
 En esta sección se describe cómo crear, configurar y codificar una tarea personalizada y su interfaz de usuario personalizada opcional.  
  
 [Crear una tarea personalizada](creating-a-custom-task.md)  
 Describe el primer paso, que crea la tarea personalizada.  
  
 [Codificar una tarea personalizada](coding-a-custom-task.md)  
 Describe cómo codificar los métodos principales de una tarea personalizada.  
  
 [Conectarse a orígenes de datos de una tarea personalizada](connecting-to-data-sources-in-a-custom-task.md)  
 Describe cómo conectar una tarea personalizada a un origen de datos.  
  
 [Provocar y definir eventos en una tarea personalizada](raising-and-defining-events-in-a-custom-task.md)  
 Describe cómo provocar eventos y definir eventos personalizados de la tarea personalizada.  
  
 [Agregar compatibilidad con la depuración de una tarea personalizada](adding-support-for-debugging-in-a-custom-task.md)  
 Describe cómo crear los destinos de punto de interrupción en la tarea personalizada.  
  
 [Desarrollar una interfaz de usuario para una tarea personalizada](developing-a-user-interface-for-a-custom-task.md)  
 Describe cómo crear una interfaz de usuario que se muestra en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] para configurar propiedades en la tarea personalizada.  
  
## <a name="related-sections"></a>Secciones relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Información común a todos los objetos personalizados  
 Para obtener información común a todos los tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar objetos personalizados para Integration Services](../developing-custom-objects-for-integration-services.md)  
 Describe los pasos básicos para implementar todos los tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Conservar objetos personalizados](../persisting-custom-objects.md)  
 Describe la persistencia personalizada y explica cuándo es necesaria.  
  
 [Generar, implementar y depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md)  
 Describe las técnicas para generar, firmar, implementar y depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Información sobre otros objetos personalizados  
 Para obtener información acerca de los demás tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar un administrador de conexiones personalizado](../connection-manager/developing-a-custom-connection-manager.md)  
 Describe cómo programar los administradores de conexiones personalizados.  
  
 [Desarrollar un proveedor de registro personalizado](../log-provider/developing-a-custom-log-provider.md)  
 Describe cómo programar los proveedores de registro personalizados.  
  
 [Desarrollar un enumerador ForEach personalizado](../foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Describe cómo programar los enumeradores personalizados.  
  
 [Desarrollar un componente de flujo de datos personalizado](../data-flow/developing-a-custom-data-flow-component.md)  
 Describe cómo programar orígenes, transformaciones y destinos personalizados del flujo de datos.  
  
![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Extender el paquete con la tarea script](../../extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Comparar soluciones de scripting y objetos personalizados](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
