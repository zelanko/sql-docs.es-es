---
title: 'Lección 1: Crear un proyecto de servidor de informes (Reporting Services) | Microsoft Docs'
ms.date: 05/01/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c3a32b6b27a8919d729c95bfe29f50c2bda81db8
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65095858"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lección 1: Crear un proyecto de servidor de informes (Reporting Services)

En esta lección, creará un *proyecto de servidor de informes* y un archivo de *definición de informe (.rdl)* con el *Diseñador de informes*.

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] es un entorno [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para crear soluciones de inteligencia empresarial. SSDT cuenta con un Diseñador de informes para crear el entorno, donde puede abrir, modificar, obtener una vista previa, guardar e implementar definiciones de informe paginadas de [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] , orígenes de datos compartidos, conjuntos de datos compartidos y elementos de informe.

Al crear informes con el Diseñador de informes, se crea un proyecto de servidor de informes que contiene los archivos de informes y otros archivos de recursos utilizados por los informes.

## <a name="to-create-a-report-server-project"></a>Para crear un proyecto de servidor de informes
  
1. En el menú **Archivo**, seleccione **Nuevo** > **Proyecto**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. En la columna más a la izquierda, debajo de **Instalado**, seleccione **Reporting Services**. En algunos casos, puede estar debajo del grupo **Business Intelligence**.

    ![select-report-server-project-template](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > Para VS, si no ve Reporting Services en la columna izquierda, agregue el Diseñador de informes mediante la instalación de la carga de trabajo SSDT. En el menú **Herramientas**, seleccione **Obtener herramientas y características...** y, después, **SQL Server Data Tools** en las cargas de trabajo mostradas. Si no ve los objetos de los servicios de informes en la columna central, agregue las extensiones de Reporting Services. En el menú **Herramientas**, seleccione **Extensiones y actualizaciones** > **En línea**. En la columna central, seleccione **Proyectos de Microsoft Reporting Services** > **Descargar** en las extensiones mostradas. Para SSDT, ea [Descargar e instalar SQL Server Data Tools (SSDT) para Visual Studio](../ssdt/download-sql-server-data-tools-ssdt.md).

3. Seleccione el icono de **Proyecto de servidor de informes** &nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;en la columna central del cuadro de diálogo **Nuevo proyecto**.

4. En el cuadro de texto **Nombre**, escriba “Tutorial” para el nombre del proyecto. De forma predeterminada, en el cuadro de texto **Ubicación**, se muestra la ruta de acceso a la carpeta "Documents\Visual Studio 20xx\Projects\". El Diseñador de informes crea una carpeta denominada Tutorial debajo de esta ruta de acceso y crea el proyecto Tutorial en esta carpeta. Si el proyecto no pertenece a una solución de VS, entonces VS también crea un archivo de solución (.sln).

5. Seleccione **Aceptar** para crear el proyecto. El proyecto Tutorial se muestra en el panel **Explorador de soluciones** de la derecha.
  
## <a name="creating-a-report-definition-file-rdl"></a>Creación del archivo de definición de informe (RDL)  
  
1. En el panel **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Informes**. Si no ve el panel **Explorador de soluciones**, seleccione el menú **Ver** > **Explorador de soluciones**.

2. Seleccione **Agregar** > **Nuevo elemento**.

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)

3. En la ventana **Agregar nuevo elemento**, seleccione el icono **Informe**.

4. Escriba "Sales Orders.rdl" en el cuadro de texto **Nombre**.

5. Seleccione el **botón Agregar** en la parte inferior derecha del cuadro de diálogo **Agregar nuevo elemento** para completar el proceso. El Diseñador de informes se abre y muestra el archivo del informe Sales Orders en la vista Diseño.

    ![ssrs-ssdt-01-new-report-designer](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>Pasos siguientes

Hasta ahora, ha creado el proyecto de informe Tutorial y el informe Sales Orders. En las demás lecciones, aprenderá a:

- Configurar un origen de datos para el informe
- Crear un conjunto de datos a partir del origen de datos
- Diseñar el informe y dar formato a dicho diseño

Continúe con la [Lección 2: Especificar información de conexión &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).
