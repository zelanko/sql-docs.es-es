---
title: Desarrollar una tarea personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-custom-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
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
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 853a6e9eceaa364db25c99050c59005e0e9ad27a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="developing-a-custom-task"></a>Desarrollar una tarea personalizada
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa tareas para realizar unidades de trabajo con el fin de admitir la extracción, transformación y carga de datos. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye varias tareas que realizan las acciones usadas con más frecuencia, desde ejecutar una instrucción SQL hasta descargar un archivo de un sitio FTP. Si las tareas incluidas y las acciones compatibles no cumplen completamente sus requisitos, puede crear una tarea personalizada.  
  
 Para crear una tarea personalizada, debe crear una clase que herede de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task>, aplicar el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a la nueva clase e invalidar los métodos y propiedades importantes de la clase base, incluido el método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
## <a name="in-this-section"></a>En esta sección  
 En esta sección se describe cómo crear, configurar y codificar una tarea personalizada y su interfaz de usuario personalizada opcional.  
  
 [Crear una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)  
 Describe el primer paso, que crea la tarea personalizada.  
  
 [Codificar una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)  
 Describe cómo codificar los métodos principales de una tarea personalizada.  
  
 [Conectarse a orígenes de datos de una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
 Describe cómo conectar una tarea personalizada a un origen de datos.  
  
 [Provocar y definir eventos en una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/raising-and-defining-events-in-a-custom-task.md)  
 Describe cómo provocar eventos y definir eventos personalizados de la tarea personalizada.  
  
 [Agregar compatibilidad con la depuración de una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/adding-support-for-debugging-in-a-custom-task.md)  
 Describe cómo crear los destinos de punto de interrupción en la tarea personalizada.  
  
 [Desarrollar una interfaz de usuario para una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
 Describe cómo crear una interfaz de usuario que se muestra en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] para configurar propiedades en la tarea personalizada.  
  
## <a name="related-sections"></a>Secciones relacionadas  
  
### <a name="information-common-to-all-custom-objects"></a>Información común a todos los objetos personalizados  
 Para obtener información común a todos los tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar objetos personalizados para Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Describe los pasos básicos para implementar todos los tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Conservar objetos personalizados](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Describe la persistencia personalizada y explica cuándo es necesaria.  
  
 [Generar, implementar y depurar objetos personalizados](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Describe las técnicas para generar, firmar, implementar y depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Información sobre otros objetos personalizados  
 Para obtener información acerca de los demás tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar un administrador de conexiones personalizado](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Describe cómo programar los administradores de conexiones personalizados.  
  
 [Desarrollar un proveedor de registro personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Describe cómo programar los proveedores de registro personalizados.  
  
 [Desarrollar un enumerador ForEach personalizado](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Describe cómo programar los enumeradores personalizados.  
  
 [Desarrollar un componente de flujo de datos personalizado](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Describe cómo programar orígenes, transformaciones y destinos personalizados del flujo de datos.  
  
## <a name="see-also"></a>Ver también  
 [Extender el paquete con la tarea Script](../../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Comparar soluciones de scripting y objetos personalizados](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
