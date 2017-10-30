---
title: "Documentación para desarrolladores de Integration Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
caps.latest.revision: 76
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf7d7afba8ada3f6027db3053914b1822597792c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="integration-services-developer-documentation"></a>Guía del desarrollador de Integration Services
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye un modelo de objetos completamente reescrito, que se ha mejorado con muchas características que consiguen que la extensión y la programación de paquetes resulten más sencillas, flexibles y eficaces. Los desarrolladores pueden extender y programar prácticamente cualquier aspecto de los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Como desarrollador de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], existen dos enfoques fundamentales que puede aplicar en la programación de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Puede extender los paquetes escribiendo componentes que pasan a estar disponibles en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] para proporcionar funcionalidad personalizada en un paquete.  
  
-   Puede crear, configurar y ejecutar paquetes mediante programación desde sus propias aplicaciones.  
  
 Si los componentes integrados en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no cumplen sus requisitos, puede ampliar la potencia de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] codificando sus propias extensiones. En este enfoque, tiene dos opciones diferentes:  
  
-   Para el uso ad hoc en un paquete único, puede crear una tarea personalizada escribiendo código en la tarea Script o bien crear un componente de flujo de datos personalizado escribiendo código en el componente de script, que puede configurar como origen, transformación o destino. Estos eficaces contenedores escriben automáticamente el código de la infraestructura y permiten centrarse exclusivamente en desarrollar la funcionalidad personalizada; sin embargo, no se reutilizan con facilidad en otro lugar.  
  
-   Para el uso en varios paquetes, puede crear extensiones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] personalizadas como administradores de conexión, tareas, enumeradores, proveedores de registro y componentes de flujo de datos. El modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administrado contiene clases base que proporcionan un punto de inicio y consiguen que el desarrollo de extensiones resulte más fácil que nunca.  
  
 Si desea crear paquetes de forma dinámica o administrar y ejecutar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fuera del entorno de desarrollo, puede manipular los paquetes mediante programación. Puede cargar, modificar y ejecutar los paquetes existentes o bien puede crear y ejecutar paquetes completamente nuevos mediante programación. En este enfoque, tiene un intervalo de opciones continuo:  
  
-   Cargar y ejecutar un paquete existente sin modificarlo.  
  
-   Cargar un paquete existente, volver a configurarlo (por ejemplo, especificar un origen de datos diferente) y ejecutarlo.  
  
-   Crear un nuevo paquete, agregar y configurar componentes, realizar cambios objeto a objeto y propiedad a propiedad, guardarlo y ejecutarlo.  
  
 Estos enfoques de la programación de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se describen en esta sección y se muestran con ejemplos.  
  
## <a name="in-this-section"></a>En esta sección  
 [Información general sobre la programación de Integration Services](../integration-services/integration-services-programming-overview.md)  
 Describe los roles de flujo de control y flujo de datos en el desarrollo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 [Descripción de las transformaciones sincrónicas y asincrónicas](../integration-services/understanding-synchronous-and-asynchronous-transformations.md)  
 Describe la distinción importante entre las salidas sincrónicas y asincrónicas, y los componentes que las utilizan en el flujo de datos.  
  
 [Trabajar con administradores de conexiones mediante programación](../integration-services/working-with-connection-managers-programmatically.md)  
 Enumera los administradores de conexión que puede utilizar desde el código administrado y los valores que los administradores de conexión que se devuelven cuando el código llama a la **AcquireConnection** método.  
  
 [Ampliar paquetes con scripting](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 Describe cómo extender el flujo de control mediante la tarea de secuencia de comandos o el flujo de datos mediante el componente de Script.  
  
 [Ampliar paquetes con objetos personalizados](../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Describe cómo crear y programar tareas personalizadas de programa, componentes de flujo de datos y otros objetos de paquete para su uso en varios paquetes.  
  
 [Compilar paquetes mediante programación](../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 Describe cómo crear, configurar y guardar los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mediante programación.  
  
 [Ejecutar y administrar paquetes mediante programación](../integration-services/run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 Describe cómo enumerar, ejecutar y administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] mediante programación.  
  
## <a name="reference"></a>Referencia  
 [Referencia de errores y mensajes de Integration Services](../integration-services/integration-services-error-and-message-reference.md)  
 Enumera los códigos de error predefinidos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], junto con sus nombres simbólicos y descripciones.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Herramientas para solucionar problemas del desarrollo de paquetes](../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
 Describe las características y herramientas que ofrece [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para solucionar problemas de los paquetes durante el desarrollo.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Ejemplos de CodePlex, en la página [Integration Services Product Samples](http://go.microsoft.com/fwlink/?LinkID=131204)de www.codeplex.com/MSFTISProdSamples.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
  
  

