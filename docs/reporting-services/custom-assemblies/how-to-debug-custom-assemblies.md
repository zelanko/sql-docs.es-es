---
title: "Cómo: depurar los ensamblados personalizados | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b6cdc41f90765a3fc1a568bc76ddf0d41c15b38a
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="how-to-debug-custom-assemblies"></a>Cómo depurar ensamblados personalizados
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proporciona varias herramientas de depuración que pueden ayudarle a analizar el código de ensamblado personalizado y localizar errores en él. La mejor herramienta para utilizar dependerá de lo que intente llevar a cabo. En este ejemplo se usa [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)].  
  
 La manera recomendada de diseñar, desarrollar y probar los ensamblados personalizados para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es crear una solución que contenga tanto los informes de prueba como el ensamblado personalizado.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>Para depurar ensamblados con una única instancia de Visual Studio  
  
1.  Cree un nuevo proyecto de informe mediante [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
     Cuando se crea un proyecto de informe, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] también se crea una solución que lo contiene.  
  
2.  Agregue un nuevo proyecto de biblioteca de clases a la solución existente. Asegúrese de que el proyecto de informe se establece como proyecto de inicio. Para obtener más información sobre cómo llevarlo a cabo, vea la documentación de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
3.  En el Explorador de soluciones, seleccione la solución.  
  
4.  En el **vista** menú, haga clic en **páginas de propiedades**.  
  
     El **páginas de propiedades de solución** abre el cuadro de diálogo.  
  
5.  En el panel izquierdo, expanda **propiedades comunes** si es necesario y haga clic en **dependencias del proyecto**. Seleccione el proyecto de informe desde el **proyecto** lista desplegable. Seleccione el proyecto de ensamblado en el **depende** lista.  
  
6.  Haga clic en **Aceptar** para guardar los cambios y cerrar la **páginas de propiedades** cuadro de diálogo.  
  
7.  En el Explorador de soluciones, seleccione su proyecto de ensamblado personalizado.  
  
8.  En el **vista** menú, haga clic en **páginas de propiedades**.  
  
     El **páginas de propiedades de proyecto** abre el cuadro de diálogo.  
  
9. Haga clic en el **generar** ficha si se encuentra en un proyecto de C# o la **compilar** ficha si se encuentra en un [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] proyecto.  
  
10. En el **generar**/**compilar** página, escriba la ruta de acceso a la carpeta del Diseñador de informes. De forma predeterminada, es C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE) en el **ruta de acceso de salida** cuadro de texto. De esta forma se genera e implementa directamente una versión actualizada del ensamblado personalizado para el Diseñador de informes antes de que se ejecute el informe.  
  
11. Cuando haya diseñado el informe y desarrollado el ensamblado personalizado, establezca puntos de interrupción en el código de ensamblado personalizado.  
  
12. Ejecute el informe en **DebugLocal** modo presionando la tecla F5. Cuando el informe se ejecuta en la ventana de la vista previa emergente, el depurador se para en los puntos de interrupción que se corresponden con el código ejecutable del ensamblado. Utilice F11 para recorrer el código de ensamblado personalizado.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>Para depurar los ensamblados con dos instancias de Visual Studio  
  
1.  Inicie [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] y abra el proyecto de ensamblado personalizado.  
  
2.  Genere el proyecto e implemente el ensamblado personalizado y el archivo .pdb acompañante para el Generador de informes. Para obtener más información acerca de la implementación, consulte [implementar un ensamblado personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md).  
  
3.  Abra un proyecto de informe que use el ensamblado personalizado mientras deja el código de ensamblado personalizado abierto en una instancia independiente de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
4.  Navegue a la instancia de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] que contiene el proyecto de ensamblado personalizado y establezca algunos puntos de interrupción en el código.  
  
5.  Con el proyecto de ensamblado personalizado aún en la ventana activa, haga clic en **adjuntar al proceso** en el **depurar** menú.  
  
     El **adjuntar al proceso** abre el cuadro de diálogo.  
  
6.  En la lista de procesos, seleccione el proceso devenv.exe que corresponde al proyecto de informe y haga clic en **adjuntar**.  
  
7.  Defina las expresiones que utilizará en el informe desde su ensamblado personalizado y diseñe el informe.  
  
8.  Cuando haya terminado de diseñar el informe, haga clic en el **vista previa** ficha.  
  
     El informe se ejecuta y el código de ensamblado personalizado debería detenerse en los puntos de interrupción predefinidos.  
  
    > [!NOTE]  
    >  Mediante el **vista previa** ficha no exige permisos de código para el ensamblado. Para realizar una prueba completa que incluye los errores de seguridad de acceso de código, inicie el proyecto de informe en el **DebugLocal** opción de configuración.  
  
9. Recorra el código con la tecla F11. Para obtener más información acerca de cómo depurar con [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], vea la documentación de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Usar ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
