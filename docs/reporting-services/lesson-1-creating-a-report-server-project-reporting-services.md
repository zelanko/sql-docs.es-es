---
title: 'Lección 1: Crear un proyecto de servidor de informes (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 11/30/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
caps.latest.revision: 57
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fea148cc4148b4beaf14c8b31d7bd23aad734a0b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lección 1: Crear un proyecto de servidor de informes (Reporting Services)

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Lección 1: Crear un proyecto de servidor de informes (Reporting Services)](https://msdn.microsoft.com/en-US/library/ms167559(SQL.120).aspx).

En esta lección, creará un *proyecto de servidor de informes* y un archivo de *definición de informe (.rdl)* en [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] dentro de Visual Studio. 

Para crear un informe con [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], primero necesita un proyecto de servidor de informes en el que guardar el archivo de definición del informe (.rdl) y cualquier otro archivo de recurso que necesite para el informe. 

En las siguientes lecciones, defina un origen de datos para el informe, un conjunto de datos y el diseño del informe. Cuando ejecuta el informe, los datos se recuperan y combinan con el diseño y luego se representan en pantalla, desde donde se pueden exportar, imprimir o guardar.  
  
  
  
## <a name="to-create-a-report-server-project"></a>Para crear un proyecto de servidor de informes  
  
1.  Abra [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)].  
  
2.  En el menú **Archivo** > **Nuevo** > **Proyecto**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3.  En **Plantillas** > **instaladas** > **Business Intelligence**, haga clic en **Reporting Services**.

    ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png)

5. Haga clic en **Proyecto de servidor de informes** ![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png). 

   >**Nota**: Si no ve las opciones **Business Intelligence** o **Proyecto de servidor de informes**, tiene que actualizar SSDT con las plantillas de Business Intelligence. Consulte [Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  
  
5.  En **Nombre**, escriba **tutorial**.  

    De forma predeterminada, se crea en la carpeta Visual Studio 2015\Projects en un directorio nuevo.
    
    ![ssrs-ssdt-01-solution-location](../reporting-services/media/ssrs-ssdt-01-solution-location.png)
  
6.  Haga clic en **Aceptar** para crear el proyecto.  
  
    El proyecto Tutorial se muestra en el panel Explorador de soluciones de la derecha.  
  
## <a name="to-create-a-new-report-definition-file"></a>Para crear un nuevo archivo de definición de informe  
  
1.  En el panel **Explorador de soluciones** , haga clic con el botón derecho en **Informes** > **Agregar** > **Nuevo elemento**. 

    >**Consejo**: si no ve el panel del **Explorador de soluciones** , en el menú **View** , haga clic en el **Explorador de soluciones**. 

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2.  En la ventana **Agregar nuevo elemento** , haga clic en **Informe** ![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png).  
  
3.  En **Nombre**, escriba **Sales Orders.rdl** y, después, haga clic en **Agregar**.  
  
    Se abrirá el Diseñador de informes y se mostrará el nuevo archivo .rdl en la vista Diseño.  
    
    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     El Diseñador de informes es un componente de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que se ejecuta en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tiene dos vistas: **Diseño** y **Vista previa**. Haga clic en cada pestaña para cambiar las vistas.  
  
    Los datos se definen en el panel **Datos de informe** . El diseño del informe se define en la vista **Diseño** . Puede ejecutar el informe y ver su aspecto en la vista **Vista previa** .  
  
## <a name="next-lesson"></a>Lección siguiente  
Ha creado un proyecto de informe denominado "Tutorial" y ha agregado un archivo de definición de informe (.rdl) al proyecto del informe correctamente. A continuación, debe especificar un origen de datos para utilizarlo con el informe. Vea [Lección 2: Especificar información de conexión &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Ver también  
[Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  

