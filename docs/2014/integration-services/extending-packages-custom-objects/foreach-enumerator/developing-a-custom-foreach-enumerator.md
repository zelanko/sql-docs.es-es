---
title: Desarrollar un enumerador Para cada uno personalizado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d81d34389aaa46c6e4946cf4a159818724f70bbd
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394513"
---
# <a name="developing-a-custom-foreach-enumerator"></a>Desarrollar un enumerador foreach personalizado
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] usa enumeradores de foreach para iterar por los elementos de una colección y realizar las mismas tareas para cada elemento. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] incluye varios enumeradores de foreach que admiten las colecciones de uso más frecuente, como todos los archivos de una carpeta, todas las tablas de una base de datos o todos los elementos de una lista almacenados en una variable de paquete. Si las colecciones y enumeradores foreach que se proporcionan no cumplen completamente sus requisitos, puede crear un enumerador foreach personalizado.  
  
 Para crear un enumerador foreach personalizado, debe crear una clase que herede de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>, aplicar el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> a la nueva clase e invalidar los métodos y propiedades importantes de la clase base, incluido el método <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>.  
  
## <a name="in-this-section"></a>En esta sección  
 En esta sección se describe cómo crear, configurar y codificar un enumerador foreach personalizado y su interfaz de usuario personalizada.  
  
 [Crear un enumerador ForEach personalizado](creating-a-custom-foreach-enumerator.md)  
 Describe cómo crear las clases para un proyecto de enumerador foreach personalizado.  
  
 [Codificar un enumerador ForEach personalizado](coding-a-custom-foreach-enumerator.md)  
 Describe cómo implementar un enumerador foreach personalizado invalidando los métodos y propiedades de la clase base.  
  
 [Desarrollar una interfaz de usuario para un enumerador ForEach personalizado](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 Describe cómo implementar la clase de interfaz de usuario y el formulario que se utilizan para configurar el enumerador foreach personalizado.  
  
## <a name="related-topics"></a>Temas relacionados  
  
### <a name="information-common-to-all-custom-objects"></a>Información común a todos los objetos personalizados  
 Para obtener información común a todos los tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar objetos personalizados para Integration Services](../developing-custom-objects-for-integration-services.md)  
 Describe los pasos básicos para implementar todos los tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
 [Conservar objetos personalizados](../persisting-custom-objects.md)  
 Describe la persistencia personalizada y explica cuándo es necesaria.  
  
 [Generar, implementar y depurar objetos personalizados](../building-deploying-and-debugging-custom-objects.md)  
 Describe las técnicas para generar, firmar, implementar y depurar objetos personalizados.  
  
### <a name="information-about-other-custom-objects"></a>Información sobre otros objetos personalizados  
 Para obtener información sobre los demás tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:  
  
 [Desarrollar una tarea personalizada](../task/developing-a-custom-task.md)  
 Describe cómo programar las tareas personalizadas.  
  
 [Desarrollar un administrador de conexiones personalizado](../connection-manager/developing-a-custom-connection-manager.md)  
 Describe cómo programar los administradores de conexiones personalizados.  
  
 [Desarrollar un proveedor de registro personalizado](../log-provider/developing-a-custom-log-provider.md)  
 Describe cómo programar los proveedores de registro personalizados.  
  
 [Desarrollar un componente de flujo de datos personalizado](../data-flow/developing-a-custom-data-flow-component.md)  
 Describe cómo programar orígenes, transformaciones y destinos personalizados del flujo de datos.  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
