---
title: Ampliar paquetes con scripting | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ad036177e6265c31697a98c9e24fc4d1c11b310b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967255"
---
# <a name="extending-packages-with-scripting"></a>Ampliar paquetes con scripting
  Si los componentes integrados en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no cumplen sus requisitos, puede ampliar la eficacia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] codificando sus propias extensiones. Cuenta con dos opciones diferenciadas para ampliar los paquetes: puede escribir código dentro de los potentes contenedores que proporcionan la tarea Script y el componente de script o puede crear extensiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizadas desde cero derivando de las clases base que proporciona el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

 En esta sección, se explora la opción más sencilla de las dos: ampliar los paquetes con scripting.

 La tarea Script y el componente de script permiten ampliar tanto el flujo de control como el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con muy poca codificación. Ambos objetos utilizan el entorno de desarrollo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) y los lenguajes de programación [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y se benefician de toda la funcionalidad que ofrece la biblioteca de clases de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], así como de los ensamblados personalizados. La tarea Script y el componente de script permiten al desarrollador de software crear funcionalidad personalizada sin necesidad de escribir todo el código de infraestructura que se suele requerir al desarrollar una tarea personalizada o un componente de flujo de datos personalizado.

## <a name="in-this-section"></a>En esta sección
 [Comparar la tarea script y el componente de script](../extending-packages-scripting/comparing-the-script-task-and-the-script-component.md) Describe las similitudes y diferencias entre la tarea script y el componente de script.

 [Comparar soluciones de scripting y objetos personalizados](comparing-scripting-solutions-and-custom-objects.md) Describe los criterios que se deben usar para elegir entre una solución de scripting y el desarrollo de un objeto personalizado.

 [Hacer referencia a otros ensamblados en soluciones de scripting](referencing-other-assemblies-in-scripting-solutions.md) Describe los pasos necesarios para hacer referencia y usar ensamblados y espacios de nombres externos en un proyecto de scripting.

 [Extender el paquete con la tarea script](../extending-packages-scripting/task/extending-the-package-with-the-script-task.md) Describe cómo crear tareas personalizadas mediante la tarea script. Normalmente, se llama a una tarea una vez por ejecución del paquete o una vez por cada origen de datos que abre un paquete.

 [Extender el flujo de datos con el componente de script](data-flow-script-component/extending-the-data-flow-with-the-script-component.md) Describe cómo crear orígenes, transformaciones y destinos de flujo de datos personalizados mediante el componente de script. Normalmente se llama a un componente de flujo de datos una vez por cada fila de datos que se procesa.

## <a name="reference"></a>Referencia
 [Referencia de errores y mensajes de Integration Services](../integration-services-error-and-message-reference.md) Enumera los códigos de error predefinidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y descripciones.

## <a name="related-sections"></a>Secciones relacionadas
 [Ampliar paquetes con objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md) Describe cómo crear tareas personalizadas de programa, componentes de flujo de datos y otros objetos de paquete para su uso en varios paquetes.

 [Compilar paquetes mediante programación](../building-packages-programmatically/building-packages-programmatically.md) Describe cómo crear, configurar, ejecutar, cargar, guardar y administrar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes mediante programación.

![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, los artículos, los ejemplos y los vídeos más recientes de [!INCLUDE[msCoName](../../includes/msconame-md.md)], así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.

## <a name="see-also"></a>Consulte también
 [SQL Server Integration Services](../sql-server-integration-services.md)


