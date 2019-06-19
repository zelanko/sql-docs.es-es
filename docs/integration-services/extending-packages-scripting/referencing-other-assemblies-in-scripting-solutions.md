---
title: Hacer referencia a otros ensamblados en soluciones de scripting | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 889bd1f743b30727bed5266b0c725733b823d654
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724137"
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Hacer referencia a otros ensamblados en soluciones de scripting

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La biblioteca de clases de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proporciona al desarrollador de script un conjunto eficaz de herramientas para implementar una funcionalidad personalizada en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Tanto la tarea como el componente Script también pueden usar ensamblados administrados personalizados.  
  
> [!NOTE]
>  Para permitir que los paquetes usen los objetos y métodos de un servicio web, use el comando **Agregar referencia web** disponible en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). En versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], tenía que generar una clase de proxy para utilizar un servicio web.  
  
## <a name="using-a-managed-assembly"></a>Utilizar un ensamblado administrado  
 Para que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] busque en tiempo de diseño un ensamblado administrado, debe efectuar los pasos siguientes:  
  
1.  Almacene el ensamblado administrado en una carpeta del equipo.  
  
    > [!NOTE]  
    >  En versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], podría agregar solamente una referencia a un ensamblado administrado que estuviera almacenado en la carpeta %windir%\Microsoft.NET\Framework\vx.x.xxxxx o %ProgramFiles%\Microsoft SQL Server\100\SDK\Assemblies.  
  
2.  Agregue una referencia al ensamblado administrado.  
  
     Para agregar la referencia, en VSTA, en el cuadro de diálogo **Agregar referencia**, en la pestaña **Examinar**, busque y agregue el ensamblado administrado.  
  
 Para que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] busque en tiempo de ejecución el ensamblado administrado, debe efectuar los pasos siguientes:  
  
1.  Firme un ensamblado administrado con un nombre seguro.  
  
2.  Instale el ensamblado en la memoria caché de ensamblados global en el equipo en el que se ejecuta el paquete.  
  
     Para obtener más información, consulte [Generar, implementar y depurar objetos personalizados](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Utilizar la Biblioteca de clases de Microsoft .NET Framework  
 Tanto la tarea como el componente Script pueden aprovechar todos los demás objetos y la funcionalidad expuesta por la biblioteca de clases de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Por ejemplo, mediante [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede recuperar información acerca del entorno e interactuar con el equipo que está ejecutando el paquete.  
  
 En esta lista se describen algunas de las clases más utilizadas de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:  
  
-   **System.Data** Contiene la arquitectura de ADO.NET.  
  
-   **System.IO** Proporciona una interfaz para el sistema de archivos y los flujos.  
  
-   **System.Windows.Forms** Permite la creación de formularios.  
  
-   **System.Text.RegularExpressions** Proporciona las clases para trabajar con expresiones regulares.  
  
-   **System.Environment** Devuelve información acerca del equipo local, el usuario actual y los valores del equipo y del usuario.  
  
-   **System.Net** Proporciona comunicaciones por red.  
  
-   **System.DirectoryServices** Expone Active Directory.  
  
-   **System.Drawing** Proporciona bibliotecas de manipulación de imágenes completas.  
  
-   **System.Threading** Habilita la programación multiproceso.  
  
 Para obtener más información acerca de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], vea MSDN Library.  
  
## <a name="see-also"></a>Consulte también  
 [Ampliar paquetes con scripting](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
