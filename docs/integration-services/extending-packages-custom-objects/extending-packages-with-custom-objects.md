---
title: Ampliar paquetes con objetos personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 40903d65bfbd65c78951f0954d3e5bd7380afa98
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="extending-packages-with-custom-objects"></a>Ampliar paquetes con objetos personalizados
  Si los componentes que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no satisfacen sus requisitos, puede ampliar la eficacia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] codificando sus propias extensiones. Cuenta con dos opciones diferenciadas para ampliar los paquetes: puede escribir código dentro de los potentes contenedores que proporcionan la tarea Script y el componente de script o puede crear extensiones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizadas desde cero derivando de las clases base que proporciona el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 En esta sección se explora la opción más avanzada de las dos, la ampliación de paquetes con objetos personalizados.  
  
 Cuando la solución de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] personalizada requiere mayor flexibilidad de la que proporcionan la tarea Script y el componente de script (o cuando necesita un componente que se pueda volver a utilizar en varios paquetes) el modelo de objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite crear tareas personalizadas, componentes de flujo de datos y otros objetos de paquete en código administrado a partir de cero.  
  
## <a name="in-this-section"></a>En esta sección  
 [Desarrollar objetos personalizados para Integration Services](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 Describe los objetos personalizados que se pueden crear para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y resume los pasos y valores esenciales.  
  
 [Conservar objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 Describe la persistencia predeterminada de los objetos personalizados y el proceso de implementación de la persistencia personalizada.  
  
 [Generar, implementar y depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 Describe los enfoques comunes para generar, implementar y probar los diferentes tipos de objetos personalizados.  
  
 [Desarrollar una tarea personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 Describe el proceso de codificación de una tarea personalizada.  
  
 [Desarrollar un administrador de conexiones personalizado](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 Describe el proceso de codificación de un administrador de conexiones personalizado.  
  
 [Desarrollar un proveedor de registro personalizado](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 Describe el proceso de codificación de un proveedor de registro personalizado.  
  
 [Desarrollar un enumerador ForEach personalizado](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 Describe el proceso de codificación de un enumerador personalizado.  
  
 [Desarrollar un componente de flujo de datos personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 Describe cómo programar orígenes, transformaciones y destinos personalizados del flujo de datos.  
  
## <a name="reference"></a>Referencia  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
 Muestra los códigos de error predefinidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y sus descripciones.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Ampliar paquetes con scripting](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Describe cómo extender el flujo de control mediante la tarea Script o el flujo de datos mediante el componente de script.  
  
 [Compilar paquetes mediante programación](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Describe cómo crear, configurar, ejecutar, cargar, guardar y administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación.  
  
## <a name="see-also"></a>Vea también  
 [Comparar soluciones de scripting y objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
