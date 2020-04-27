---
title: Ampliar paquetes con objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7384fd52f28f52647c310f7c76eec994b8c8141
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62896213"
---
# <a name="extending-packages-with-custom-objects"></a>Ampliar paquetes con objetos personalizados
  Si los componentes que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no satisfacen sus requisitos, puede ampliar la eficacia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] codificando sus propias extensiones. Cuenta con dos opciones diferenciadas para ampliar los paquetes: puede escribir código dentro de los potentes contenedores que proporcionan la tarea Script y el componente de script o puede crear extensiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizadas desde cero derivando de las clases base que proporciona el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 En esta sección, se explora la opción más avanzada de las dos, la ampliación de paquetes con objetos personalizados.  
  
 Cuando la solución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizada requiere mayor flexibilidad de la que proporcionan la tarea Script y el componente de script (o cuando necesita un componente que se pueda volver a utilizar en varios paquetes) el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite crear tareas personalizadas, componentes de flujo de datos y otros objetos de paquete en código administrado a partir de cero.  
  
## <a name="in-this-section"></a>En esta sección  
 [Desarrollar objetos personalizados para Integration Services](developing-custom-objects-for-integration-services.md)  
 Describe los objetos personalizados que se pueden crear para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y resume los pasos y valores esenciales.  
  
 [Conservar objetos personalizados](persisting-custom-objects.md)  
 Describe la persistencia predeterminada de los objetos personalizados y el proceso de implementación de la persistencia personalizada.  
  
 [Generar, implementar y depurar objetos personalizados](building-deploying-and-debugging-custom-objects.md)  
 Describe los enfoques comunes para generar, implementar y probar los diferentes tipos de objetos personalizados.  
  
 [Desarrollar una tarea personalizada](task/developing-a-custom-task.md)  
 Describe el proceso de codificación de una tarea personalizada.  
  
 [Desarrollar un administrador de conexiones personalizado](connection-manager/developing-a-custom-connection-manager.md)  
 Describe el proceso de codificación de un administrador de conexiones personalizado.  
  
 [Desarrollar un proveedor de registro personalizado](log-provider/developing-a-custom-log-provider.md)  
 Describe el proceso de codificación de un proveedor de registro personalizado.  
  
 [Desarrollar un enumerador ForEach personalizado](foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Describe el proceso de codificación de un enumerador personalizado.  
  
 [Desarrollar un componente de flujo de datos personalizado](data-flow/developing-a-custom-data-flow-component.md)  
 Describe cómo programar orígenes, transformaciones y destinos personalizados del flujo de datos.  
  
## <a name="reference"></a>Referencia  
 [Referencia de errores y mensajes de Integration Services](../integration-services-error-and-message-reference.md)  
 Muestra los códigos de error predefinidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y sus descripciones.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Ampliar paquetes con scripting](../extending-packages-scripting/extending-packages-with-scripting.md)  
 Describe cómo extender el flujo de control mediante la tarea Script o el flujo de datos mediante el componente de script.  
  
 [Compilar paquetes mediante programación](../building-packages-programmatically/building-packages-programmatically.md)  
 Describe cómo crear, configurar, ejecutar, cargar, guardar y administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación.  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Comparar soluciones de scripting y objetos personalizados](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
