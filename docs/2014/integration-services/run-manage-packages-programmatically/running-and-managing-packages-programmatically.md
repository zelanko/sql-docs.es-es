---
title: Ejecutar y administrar paquetes mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 1a08c75e-ce8c-45ee-81bd-32248bbdb2b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ecbaa54a723fae6a3c5fd11363bf42f1f2a57da0
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376475"
---
# <a name="running-and-managing-packages-programmatically"></a>Ejecutar y administrar paquetes mediante programación
  Si tiene que administrar y ejecutar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fuera del entorno de desarrollo, puede manipular los paquetes mediante programación. En este enfoque cuenta con varias opciones:  
  
-   Cargar y ejecutar un paquete existente sin modificarlo.  
  
-   Cargar un paquete existente, volver a configurarlo (por ejemplo, para un origen de datos diferente) y ejecutarlo.  
  
-   Crear un nuevo paquete, agregar y configurar componentes objeto por objeto y propiedad por propiedad, guardarlo y ejecutarlo.  
  
 Puede cargar y ejecutar un paquete existente desde una aplicación cliente con solo escribir unas cuantas líneas de código.  
  
 En esta sección se describe y se muestra cómo ejecutar un paquete existente mediante programación y cómo obtener acceso a la salida del flujo de datos desde otras aplicaciones. Como opción de programación avanzada, puede crear un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] línea por línea mediante programación como se describe en el tema [Building Packages Programmatically](../building-packages-programmatically/building-packages-programmatically.md).  
  
 En esta sección también se tratan otras tareas administrativas que puede realizar mediante programación para administrar paquetes almacenados, paquetes en ejecución y roles de paquete.  
  
## <a name="running-packages-on-the-integration-services-server"></a>Ejecutar paquetes en el Servidor de Integration Services  
 Cuando implemente paquetes en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], puede ejecutar paquetes utilizando el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices>. El ensamblado de Microsoft.SqlServer.Management.IntegrationServices se compila con .NET Framework 3.5. Si está generando una aplicación.NET Framework 4.0, puede que tenga que agregar la referencia de ensamblado directamente al archivo de proyecto.  
  
 También puede utilizar el espacio de nombres para implementar y administrar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener información general de espacio de nombres y los fragmentos de código, vea la entrada del blog sobre [el modelo de objetos administrados de catálogo SSIS](https://go.microsoft.com/fwlink/?LinkId=253122), en blogs.msdn.com.  
  
## <a name="in-this-section"></a>En esta sección  
 [Descripción de las diferencias entre la ejecución local y remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)  
 Describe las diferencias críticas entre ejecutar un paquete localmente o en el servidor.  
  
 [Cargar y ejecutar un paquete local mediante programación](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)  
 Describe cómo ejecutar un paquete existente desde una aplicación cliente en el equipo local.  
  
 [Cargar y ejecutar un paquete remoto mediante programación](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
 Describe cómo ejecutar un paquete existente desde una aplicación cliente y asegurarse de que el paquete se ejecuta en el servidor.  
  
 [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
 Describe cómo ejecutar un paquete en el equipo local y cargar la salida del flujo de datos en una aplicación cliente mediante el destino de DataReader y el espacio de nombres DtsClient.  
  
 [Enumerar los paquetes disponibles mediante programación](../run-manage-packages-programmatically/enumerating-available-packages-programmatically.md)  
 Describe cómo detectar los paquetes disponibles administrados por el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 [Administrar paquetes y carpetas mediante programación](../run-manage-packages-programmatically/managing-packages-and-folders-programmatically.md)  
 Describe cómo crear, cambiar de nombre y eliminar paquetes y carpetas.  
  
 [Administrar los paquetes en ejecución mediante programación](../run-manage-packages-programmatically/managing-running-packages-programmatically.md)  
 Describe cómo enumerar los paquetes que se están ejecutando actualmente, examinar sus propiedades y detener un paquete en ejecución.  
  
 [Managing Package Roles Programmatically &#40;SSIS Service&#41;](../run-manage-packages-programmatically/managing-package-roles-programmatically-ssis-service.md) (Administrar roles de paquete mediante programación &#40;servicio SSIS&#41;)  
 Describe cómo obtener o establecer información sobre los roles asignados a un paquete o una carpeta.  
  
## <a name="reference"></a>Referencia  
 [Referencia de errores y mensajes de Integration Services](../integration-services-error-and-message-reference.md)  
 Muestra los códigos de error predefinidos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con sus nombres simbólicos y sus descripciones.  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Ampliar paquetes con scripting](../extending-packages-scripting/extending-packages-with-scripting.md)  
 Explica cómo extender el flujo de control mediante la tarea Script y cómo extender el flujo de datos mediante el componente de script.  
  
 [Ampliar paquetes con objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 Explica cómo crear tareas personalizadas de programa, componentes de flujo de datos y otros objetos de paquete para su uso en varios paquetes.  
  
 [Compilar paquetes mediante programación](../building-packages-programmatically/building-packages-programmatically.md)  
 Explica cómo crear, configurar y guardar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante programación.  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, los artículos, los ejemplos y los vídeos más recientes de [!INCLUDE[msCoName](../../includes/msconame-md.md)], así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
