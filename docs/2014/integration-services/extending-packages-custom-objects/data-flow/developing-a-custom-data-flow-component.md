---
title: Desarrollar un componente de flujo de datos personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ee2b30cf0796953d12f976745fb195169de86c68
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437082"
---
# <a name="developing-a-custom-data-flow-component"></a>Desarrollar un componente de flujo de datos personalizado
  La tarea de flujo de datos consta de componentes que se conectan a varios orígenes de datos y, a continuación, transforman y enrutan esos datos a alta velocidad. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] proporciona un modelo de objetos extensible que permite que los desarrolladores creen orígenes, transformaciones y destinos personalizados que se pueden utilizar en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] y en paquetes implementados. En esta sección se incluyen temas que le guiarán a la hora de desarrollar componentes de flujo de datos personalizados.

## <a name="in-this-section"></a>En esta sección
 [Crear un componente de flujo de datos personalizado](creating-a-custom-data-flow-component.md) Describe los pasos iniciales para crear un componente de flujo de datos personalizado.

 [Métodos en tiempo de diseño de un componente de flujo de datos](design-time-methods-of-a-data-flow-component.md) Describe los métodos en tiempo de diseño para implementar en un componente de flujo de datos personalizado.

 [Métodos en tiempo de ejecución de un componente de flujo de datos](run-time-methods-of-a-data-flow-component.md) Describe los métodos en tiempo de ejecución para implementar en un componente de flujo de datos personalizado.

 [Plan de ejecución y asignación de búfer](execution-plan-and-buffer-allocation.md) Describe el plan de ejecución del flujo de datos y la asignación de búferes de datos.

 [Trabajar con tipos de datos en el flujo de datos](working-with-data-types-in-the-data-flow.md) Explica cómo el flujo de datos asigna los [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tipos de datos a .NET Framework tipos de datos administrados.

 [Validar un componente de flujo de datos](validating-a-data-flow-component.md) Explica los métodos utilizados para validar la configuración de componentes y volver a configurar los metadatos del componente.

 [Implementar metadatos externos](implementing-external-metadata.md) Explica cómo usar columnas de metadatos externas para la validación de datos.

 [Generar y definir eventos en un componente de flujo de datos](raising-and-defining-events-in-a-data-flow-component.md) Explica cómo generar eventos predefinidos y personalizados.

 [Registrar y definir entradas de registro en un componente de flujo de datos](logging-and-defining-log-entries-in-a-data-flow-component.md) Explica cómo crear y escribir en entradas de registro personalizadas.

 [Usar salidas de error en un componente de flujo de datos](using-error-outputs-in-a-data-flow-component.md) Explica cómo redirigir las filas de errores a una salida alternativa.

 [Actualizar la versión de un componente de flujo de datos](upgrading-the-version-of-a-data-flow-component.md) Explica cómo actualizar los metadatos de los componentes guardados cuando se usa por primera vez una nueva versión del componente.

 [Desarrollar una interfaz de usuario para un componente de flujo de datos](developing-a-user-interface-for-a-data-flow-component.md) Explica cómo implementar un editor personalizado para un componente.

 [Desarrollar tipos específicos de componentes de flujo de datos](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md) Contiene información sobre el desarrollo de los tres tipos de componentes de flujo de datos: orígenes, transformaciones y destinos.

## <a name="reference"></a>Referencia
 <xref:Microsoft.SqlServer.Dts.Pipeline>Contiene las clases e interfaces utilizadas para crear componentes de flujo de datos personalizados.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>Contiene las clases e interfaces que componen el modelo de objetos de la tarea flujo de datos, y se utiliza para crear componentes de flujo de datos personalizados o compilar una tarea flujo de datos.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>Contiene las clases e interfaces utilizadas para crear la interfaz de usuario para los componentes de flujo de datos.

 [Referencia de errores y mensajes de Integration Services](../../integration-services-error-and-message-reference.md) Enumera los códigos de error predefinidos [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y descripciones.

## <a name="related-sections"></a>Secciones relacionadas

### <a name="information-common-to-all-custom-objects"></a>Información común a todos los objetos personalizados
 Para obtener información común a todos los tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:

 [Desarrollar objetos personalizados para Integration Services](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md) Describe los pasos básicos para implementar todos los tipos de objetos personalizados para [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .

 [Conservar objetos personalizados](../../extending-packages-custom-objects/persisting-custom-objects.md) Describe la persistencia personalizada y explica cuándo es necesario.

 [Compilar, implementar y depurar objetos personalizados](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) Describe las técnicas para compilar, firmar, implementar y depurar objetos personalizados.

### <a name="information-about-other-custom-objects"></a>Información sobre otros objetos personalizados
 Para obtener información sobre los demás tipos de objetos personalizados que puede crear en [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], vea los temas siguientes:

 [Desarrollar una tarea personalizada](../../extending-packages-custom-objects/task/developing-a-custom-task.md) Describe cómo programar tareas personalizadas.

 [Desarrollar un administrador de conexiones personalizado](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md) Describe cómo programar administradores de conexiones personalizados.

 [Desarrollar un proveedor de registro personalizado](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md) Describe cómo programar proveedores de registro personalizados.

 [Desarrollar un enumerador Foreach personalizado](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md) Describe cómo programar los enumeradores personalizados.

![Integration Services icono (pequeño)](../../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.

## <a name="see-also"></a>Consulte también
 [Extender el flujo de datos con el componente de script] (.. /.. /Extending-Packages-scripting/Data-Flow-script-Component/Extending-the-Data-Flow-with-the-script-Component.MD [comparar soluciones de scripting y objetos personalizados](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)


