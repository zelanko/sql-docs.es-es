---
description: Integration Services (SSIS), proyectos y soluciones
title: Integration Services (SSIS), proyectos y soluciones | Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.importprojectwizard.f1
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1918d6cac049fd863426ce320ab774067c350ea5
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678928"
---
# <a name="integration-services-ssis-projects-and-solutions"></a>Integration Services (SSIS), proyectos y soluciones

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para el desarrollo de paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
Los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] residen en los proyectos. Para crear y trabajar con proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], debe instalar [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md). Para más información, vea [Instalar Integration Services](../integration-services/install-windows/install-integration-services.md).  
  
 Al crear un proyecto nuevo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el cuadro de diálogo **Nuevo proyecto** incluye una plantilla **Proyecto de Integration Services** . Esta plantilla de proyecto crea un proyecto nuevo que contiene un único paquete.
  
## <a name="projects-and-solutions"></a>Proyectos y soluciones  
 Los proyectos se almacenan en soluciones. Primero se crea una solución y luego se agrega un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a la solución. Si no existe solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea automáticamente una cuando se crea el proyecto. Una solución puede contener varios proyectos de tipos diferentes.  
  
> [!TIP]  
>  De forma predeterminada, al crear un proyecto nuevo de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], la solución no se muestra en el panel **Explorador de soluciones** . Para cambiar este comportamiento predeterminado, en el menú **Herramientas** , haga clic en **Opciones** . En el cuadro de diálogo **Opciones** , expanda **Proyectos y soluciones** y, a continuación, haga clic en **General** . En la página **General** , seleccione **Mostrar solución siempre** .  

## <a name="solutions-contain-projects"></a>Las soluciones contienen proyectos  
 Una solución es un contenedor que agrupa y administra los proyectos que se utilizan cuando se desarrollan soluciones empresariales de extremo a extremo. Una solución le permite manejar varios proyectos como una sola unidad y unir uno o más proyectos relacionados que contribuyen a una solución empresarial.  
  
 Las soluciones pueden incluir diferentes tipos de proyectos. Si desea usar el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] para crear un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debe trabajar en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en una solución proporcionada por [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Cuando se crea una nueva solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] agrega una carpeta Solución al Explorador de soluciones y crea archivos con las extensiones .sln y .suo:  
  
-   El archivo *.sln contiene información sobre la configuración de soluciones y enumera los proyectos de la solución.  
  
-   El archivo *.suo contiene información sobre sus preferencias para trabajar con la solución.  
  
 Aunque [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea automáticamente una solución al crear un nuevo proyecto, también puede crear una solución en blanco y agregar proyectos posteriormente.  
   
## <a name="integration-services-projects-contain-packages"></a>Los proyectos de Integration Services contienen paquetes  
 Un proyecto es un contenedor en el que se desarrollan los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] almacena y agrupa los archivos que están relacionados con el paquete. Por ejemplo, un proyecto incluye los archivos necesarios para crear una solución de extracción, transferencia y carga específica.  
  
 Antes de crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , debería familiarizarse con el contenido básico de este tipo de proyecto. Cuando sepa lo que un proyecto contiene, puede empezar a crear y trabajar con un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="folders-in-integration-services-projects"></a>Carpetas en proyectos de Integration Services  
 El diagrama siguiente muestra las carpetas en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
![Captura de pantalla del Explorador de soluciones con las carpetas del proyecto.](media/ssis-solution-explorer.png)
  
 La tabla siguiente describe las carpetas que aparecen en un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
|Carpeta|Descripción|  
|------------|-----------------|
|Administradores de conexión|Contiene Administradores de conexiones de proyecto. Para más información, vea [Conexiones de Integration Services (SSIS)](../integration-services/connection-manager/integration-services-ssis-connections.md).|
|[!INCLUDE[ssIS](../includes/ssis-md.md)] .|Contiene paquetes. Para obtener más información, vea [Paquetes de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md).|  
|Elementos de paquete|Contiene elementos de paquete que se pueden volver a usar o importar. Para más información, vea [Reutilización del flujo de control en paquetes mediante el uso de elementos del paquete de flujo de control](reuse-control-flow-across-packages-by-using-control-flow-package-parts.md).
|Varios|Contiene archivos que no son archivos de paquete.|  
  
## <a name="files-in-integration-services-projects"></a>Archivos en proyectos de Integration Services  
 Cuando se agrega un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuevo o existente a una solución, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] crea archivos de proyecto que tienen las extensiones .dtproj, .dtproj.user, .database y Project.params. 
  
-   El archivo *.dtproj contiene información sobre las configuraciones del proyecto y elementos tales como paquetes.  
  
-   El archivo *.dtproj.user contiene información sobre sus preferencias para trabajar con el proyecto.  
  
-   El archivo *.database contiene información que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] requiere para abrir el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .

-   El archivo Project.params contiene información sobre los [parámetros del proyecto](integration-services-ssis-package-and-project-parameters.md).
  
## <a name="version-targeting-in-integration-services-projects"></a>Versión de destino en proyectos de Integration Services  
 En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], puede crear, mantener y ejecutar paquetes que tienen como destino SQL Server 2017, SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
 En el Explorador de soluciones, haga clic con el botón derecho en un proyecto de Integration Services y seleccione **Propiedades** para abrir las páginas de propiedades del proyecto. En la pestaña **General** de **Propiedades de configuración** , seleccione la propiedad **TargetServerVersion** y luego elija SQL Server 2017, SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
  
 ![Propiedad TargetServerVersion en el cuadro de diálogo Propiedades del proyecto](../integration-services/media/targetserverversion2.png "Propiedad TargetServerVersion en el cuadro de diálogo Propiedades del proyecto")  

## <a name="create-a-new-integration-services-project"></a>Crear un proyecto de Integration Services  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Nuevo** y haga clic en **Proyecto** .  
  
3.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Inteligencia empresarial** y después la plantilla **Proyecto de Integration Services** .  
  
     La plantilla **Proyecto de Integration Services** crea un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene un único paquete vacío.

  ![Captura de pantalla del cuadro de diálogo Nuevo proyecto con la plantilla Proyecto de Integration Services de Inteligencia empresarial resaltada.](media/ssis-ssdt-new-project.png)
  
4.  Si lo desea, modifique el nombre y la ubicación del proyecto.  
  
     El nombre de la solución se actualiza automáticamente para que coincida con el nombre del proyecto.  
  
5.  Para crear una carpeta diferente para el archivo de solución, seleccione **Crear directorio para la solución** . Ésta es la opción predeterminada.  
  
6.  Si en el equipo hay instalado software de control de código fuente, seleccione **Agregar al control de código fuente**  para asociar el proyecto con el control de código fuente.  
  
7.  Si el software de control de código fuente es [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, se abre el cuadro de diálogo **Inicio de sesión en Visual SourceSafe** . En **Inicio de sesión en Visual SourceSafe** , proporcione un nombre de usuario, una contraseña y el nombre de la base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe. Haga clic en **Examinar** para buscar la base de datos.  
  
    > **NOTA:** Para ver y cambiar el complemento de control de código fuente seleccionado y para configurar el entorno de control de código fuente, haga clic en **Opciones** en el menú **Herramientas** y, después, expanda el nodo **Control de código fuente** .  
  
8.  Haga clic en **Aceptar** para agregar la solución al **Explorador de soluciones** y agregue el proyecto a la solución.  

## <a name="import-an-existing-project-with-the-import-project-wizard"></a>Importación de un proyecto existente con el Asistente para importar proyectos
  
1.  En [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], haga clic en **Nuevo** > **Proyecto** en el menú **Archivo** .  
  
2.  En el área **Plantillas instaladas** de la ventana **Nuevo proyecto** , expanda **Business Intelligence** y haga clic en **Integration Services** .  
  
3.  Seleccione **Asistente para importar proyectos de Integration Services** de la lista de tipos de proyecto.  
  
4.  Escriba un nombre para el proyecto que va a crear en el cuadro de texto **Nombre** .  
  
5.  Escriba la ruta de acceso o la ubicación del proyecto en el cuadro de texto **Ubicación** o haga clic en **Examinar** para seleccionar uno.  
  
6.  Escriba un nombre para la solución en el cuadro de texto **Nombre de solución** .  
  
7.  Haga clic en **Aceptar** para iniciar el cuadro de diálogo **Asistente para importar proyectos de Integration Services** .  
  
8.  Haga clic en **Siguiente** para cambiar a la página **Seleccionar origen** .  
  
9. Si va a importar desde un archivo **.ispac** , escriba la ruta de acceso con el nombre de archivo incluido en el cuadro de texto **Ruta de acceso** . Haga clic en **Examinar** para navegar hasta la carpeta donde desea almacenar la solución, escriba el nombre del archivo en el cuadro de texto **Nombre de archivo** y haga clic en **Abrir** .  
  
     Si va a importar desde un **Catálogo de Integration Services** , escriba el nombre de la instancia de base de datos en el cuadro de texto **Nombre del servidor** , o bien haga clic en **Examinar** y seleccione la instancia de base de datos que contiene el catálogo.  
  
     Haga clic en **Examinar** junto al cuadro de texto **Ruta de acceso** , expanda la carpeta del catálogo, seleccione el proyecto que desea importar y haga clic en **Aceptar** .  
  
     Haga clic en **Siguiente** para pasar a la página **Revisión** .  
  
10. Revise la información y haga clic en **Importar** para crear un proyecto basado en el proyecto existente que ha seleccionado.  
  
11. Opcional: haga clic en **Guardar informe** para guardar los resultados en un archivo  
  
12. Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Asistente para importar proyectos de Integration Services** .  

## <a name="add-a-project-to-a-solution"></a>Adición de un proyecto a una solución 
 Cuando agregue un proyecto, puede crear uno en blanco con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o agregar uno creado anteriormente para otra solución. Solo puede agregar un proyecto a una solución existente mientras la solución está visible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
### <a name="add-a-new-project-to-a-solution"></a>Agregar un nuevo proyecto a una solución  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución para la cual desea agregar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] nuevo y realice una de las siguientes acciones:  
  
    -   Haga clic con el botón derecho en la solución, seleccione **Agregar** y, después, haga clic en **Nuevo proyecto** .  
  
    -   En el menú **Archivo** , seleccione **Agregar** y haga clic en **Nuevo proyecto** .  
  
2.  En el cuadro de diálogo **Nuevo proyecto** , seleccione **Proyecto de Integration Services** del panel **Plantillas** .  
  
3.  Opcionalmente, modifique el nombre y ubicación del proyecto.  
  
4.  Haga clic en **OK** .  
  
### <a name="add-an-existing-project-to-a-solution"></a>Agregar un proyecto existente a una solución  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución para la cual desee agregar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] existente y realice una de las siguientes acciones:  
  
    -   Haga clic con el botón derecho en la solución, seleccione **Agregar** y, después, haga clic en **Proyecto existente** .  
  
    -   En el menú **Archivo** , seleccione **Agregar** y haga clic en **Proyecto existente** .  
  
2.  En el cuadro de diálogo **Agregar proyecto existente** , busque el proyecto que desee agregar y haga clic en **Abrir** .  
  
3.  El proyecto se agrega a la carpeta de soluciones en el **Explorador de soluciones** .  
  
## <a name="remove-a-project-from-a-solution"></a>Eliminación de un proyecto de una solución
 Solo puede quitar un proyecto de una solución mientras la solución está visible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una vez que la solución está visible, puede quitar todos los proyectos excepto uno. Tan pronto como queda un solo proyecto, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ya no muestra la carpeta de la solución y no se puede quitar el último proyecto.  
   
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución de la que desea quitar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y, después, haga clic en **Descargar el proyecto** .  
  
3.  Haga clic en **Aceptar** para confirmar la eliminación.  

## <a name="add-an-item-to-a-project"></a>Adición de un elemento a un proyecto  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución que contiene el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al que desea agregar un elemento.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, seleccione **Agregar** y realice una de las siguientes acciones:  
  
    -   Haga clic en **Nuevo elemento** y a continuación, seleccione una plantilla del panel **Plantillas** en el cuadro de diálogo **Agregar nuevo elemento** .  
  
    -   Haga clic en **Elemento existente** , examine el cuadro de diálogo **Agregar elemento existente** para encontrar el elemento que desea agregar al proyecto y luego haga clic en **Agregar** .  
  
3.  El nuevo elemento aparece en la carpeta correspondiente en el Explorador de soluciones.  

## <a name="copy-project-items"></a>Copiar los elementos de proyectos  
Puede copiar objetos dentro de un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o entre proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. También puede copiar objetos entre los otros tipos de proyectos de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para copiar entre proyectos, el proyecto debe formar parte de la misma solución de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] .

1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución o el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el que desea trabajar.  
  
2.  Expanda el proyecto y la carpeta de elementos desde donde se copiará.  
  
3.  Haga clic con el botón derecho en el elemento y, después, haga clic en **Copiar** .  
  
4.  Haga clic con el botón derecho en el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y luego haga clic en **Pegar** .  
  
     Los elementos se copian automáticamente en la carpeta correcta. Si copia elementos al proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que no son paquetes, estos elementos se copian en la carpeta **Varios** .  

## <a name="next-steps"></a>Pasos siguientes

- Descargue e instale [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md).
- [Tutorial de SSIS: Crear un paquete ETL sencillo](ssis-how-to-create-an-etl-package.md)
