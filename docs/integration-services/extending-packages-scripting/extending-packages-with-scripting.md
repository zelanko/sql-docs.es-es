---
title: Ampliar paquetes con scripting | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8465b0500ae313a66b9750080f0194fb95dce75b
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35407887"
---
# <a name="extending-packages-with-scripting"></a>Ampliar paquetes con scripting
  Si los componentes integrados en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no cumplen sus requisitos, puede ampliar la eficacia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] codificando sus propias extensiones. Cuenta con dos opciones diferenciadas para ampliar los paquetes: puede escribir código dentro de los potentes contenedores que proporcionan la tarea Script y el componente de script o puede crear extensiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizadas desde cero derivando de las clases base que proporciona el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 En esta sección se explora la opción más sencilla de las dos, ampliar los paquetes con scripting.  
  
 La tarea Script y el componente de script permiten ampliar tanto el flujo de control como el flujo de datos de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con muy poca codificación. Ambos objetos utilizan el entorno de desarrollo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) y los lenguajes de programación [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# y se benefician de toda la funcionalidad que ofrece la biblioteca de clases de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], así como de los ensamblados personalizados. La tarea Script y el componente de script permiten al desarrollador de software crear funcionalidad personalizada sin necesidad de escribir todo el código de infraestructura que se suele requerir al desarrollar una tarea personalizada o un componente de flujo de datos personalizado.  
  
## <a name="in-this-section"></a>En esta sección  
 [Comparar la tarea Script y el componente de script](../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 Describe las similitudes y diferencias entre la tarea Script y el componente de script.  
  
 [Comparar soluciones de scripting y objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
 Describe los criterios que se deben utilizar al elegir entre una solución de scripting y el desarrollo de un objeto personalizado.  
  
 [Hacer referencia a otros ensamblados en soluciones de scripting](../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 Describe los pasos necesarios para hacer referencia y utilizar ensamblados y espacios de nombres externos en un proyecto de scripting.  
  
 [Extender el paquete con la tarea Script](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 Describe cómo crear tareas personalizadas mediante la tarea Script. Normalmente, se llama a una tarea una vez por ejecución del paquete o una vez por cada origen de datos que abre un paquete.  
  
 [Ampliar el flujo de datos con el componente de script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 Explica cómo crear orígenes, transformaciones y destinos personalizados de flujo de datos mediante el componente de script. Normalmente se llama a un componente de flujo de datos una vez por cada fila de datos que se procesa.  
  
## <a name="reference"></a>Referencia  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Muestra los códigos de error predefinidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y sus descripciones.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Ampliar paquetes con objetos personalizados](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Explica cómo crear tareas personalizadas de programa, componentes de flujo de datos y otros objetos de paquete para su uso en varios paquetes.  
  
 [Compilar paquetes mediante programación](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Describe cómo crear, configurar, ejecutar, cargar, guardar y administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación.  
  
## <a name="see-also"></a>Ver también  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
