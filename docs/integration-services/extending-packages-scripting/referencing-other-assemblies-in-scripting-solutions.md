---
title: Hacer referencia a otros ensamblados en soluciones de Scripting | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Hacer referencia a otros ensamblados en soluciones de scripting
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] biblioteca de clases proporciona al desarrollador de script con un conjunto eficaz de herramientas para implementar funcionalidad personalizada en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes. Tanto la tarea como el componente Script también pueden usar ensamblados administrados personalizados.  
  
> [!NOTE]  
>  Para habilitar los paquetes para utilizar los objetos y métodos de un servicio Web, use la **Agregar referencia Web** comandos disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools para aplicaciones (VSTA). En versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], tenía que generar una clase de proxy para utilizar un servicio web.  
  
## <a name="using-a-managed-assembly"></a>Utilizar un ensamblado administrado  
 Para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para buscar un ensamblado administrado en tiempo de diseño, debe hacer lo siguiente:  
  
1.  Almacene el ensamblado administrado en una carpeta del equipo.  
  
    > [!NOTE]  
    >  En versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], podría agregar solamente una referencia a un ensamblado administrado que estuviera almacenado en la carpeta %windir%\Microsoft.NET\Framework\vx.x.xxxxx o %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Agregue una referencia al ensamblado administrado.  
  
     Para agregar la referencia, en VSTA, en la **Agregar referencia** cuadro de diálogo, en la **examinar** ficha, busque y agregue el ensamblado administrado.  
  
 Para que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] busque en tiempo de ejecución el ensamblado administrado, debe efectuar los pasos siguientes:  
  
1.  Firme un ensamblado administrado con un nombre seguro.  
  
2.  Instale el ensamblado en la memoria caché de ensamblados global en el equipo en el que se ejecuta el paquete.  
  
     Para obtener más información, consulte [Building, Deploying and Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Utilizar la Biblioteca de clases de Microsoft .NET Framework  
 Tanto la tarea como el componente Script pueden aprovechar todos los demás objetos y la funcionalidad expuesta por la biblioteca de clases de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Por ejemplo, mediante [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede recuperar información acerca del entorno e interactuar con el equipo que está ejecutando el paquete.  
  
 En esta lista se describen algunas de las clases más utilizadas de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:  
  
-   **System.Data** contiene la arquitectura de ADO.NET.  
  
-   **System.IO** proporciona una interfaz para el sistema de archivos y secuencias.  
  
-   **System.Windows.Forms** proporciona la creación de formularios.  
  
-   **System.Text.RegularExpressions** proporciona clases para trabajar con expresiones regulares.  
  
-   **System.Environment** devuelve información sobre el equipo local, el usuario actual y la configuración de equipo y usuario.  
  
-   **System.Net** proporciona comunicaciones por red.  
  
-   **System.DirectoryServices** expone Active Directory.  
  
-   **System.Drawing** proporciona bibliotecas de manipulación de imágenes completas.  
  
-   **System.Threading** habilita la programación multiproceso.  
  
 Para obtener más información acerca de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea MSDN Library.  
  
## <a name="see-also"></a>Vea también  
 [Ampliar paquetes con Scripting](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  

