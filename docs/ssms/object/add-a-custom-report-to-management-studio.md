---
title: Agregar un informe personalizado a Management Studio | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 04726d3d8f01dbb667ab728abd56fce8e7ce3933
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="add-a-custom-report-to-management-studio"></a>agregar un informe personalizado a Management Studio
En este tema se describe cómo se crea un informe sencillo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)] que se guarda como archivo .rdl y, a continuación, cómo se agrega dicho archivo a [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] como informe personalizado. [!INCLUDE[ssRS](../../includes/ssrs_md.md)] puede crear una gran variedad de informes complejos. Para crear un informe siguiendo las instrucciones de este tema, debe tener instalado [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] en el equipo. No es necesario instalar [!INCLUDE[ssRS](../../includes/ssrs_md.md)] en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para ejecutar un informe personalizado mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>Para crear un informe simple guardado como un archivo .rdl  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Microsoft SQL Server**y, luego, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En la lista **Tipos de proyecto** , haga clic en **Proyectos de Business Intelligence**.  
  
4.  En la lista **Plantillas** , haga clic en **Asistente de proyectos de servidor de informes**.  
  
5.  En **Nombre**, escriba **ConnectionsReport**y, a continuación, haga clic en **Aceptar**.  
  
6.  En la página de introducción del **Asistente para informes** , haga clic en **Siguiente**.  
  
7.  En la página **Seleccionar el origen de datos** , en el cuadro Nombre, escriba un nombre para esta conexión a [!INCLUDE[ssDE](../../includes/ssde_md.md)]y, a continuación, haga clic en **Editar**.  
  
8.  En el cuadro de diálogo **Propiedades de conexión** , en el cuadro **Nombre del servidor** , escriba el nombre de la instancia de [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
9. En el cuadro **Seleccione o escriba un nombre de base de datos** , escriba el nombre de cualquier base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], como [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)], y haga clic en **Aceptar**.  
  
10. En la página **Seleccionar el origen de datos** , haga clic en **Siguiente**.  
  
11. En la página **Diseñar la consulta** , en el cuadro **Cadena de consulta** , escriba la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql_md.md)] que muestra las conexiones actuales a [!INCLUDE[ssDE](../../includes/ssde_md.md)]y, a continuación, haga clic en **Siguiente**. El cuadro Cadena de consulta del Asistente para informes no aceptará parámetros de informe. Los informes personalizados más complejos deben crearse manualmente.  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. En la página **Seleccionar el tipo de informe** , seleccione **Tabular**y, a continuación, haga clic en **Finalizar**.  
  
13. En la página **Finalización del asistente** , en el cuadro **Nombre del informe** , escriba **ConnectionsReport**y, a continuación, haga clic en **Finalizar** para crear y guardar el informe.  
  
14. Cierre [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio_md.md)].  
  
15. Copie **ConnectionsReport.rdl** en una carpeta que haya creado en el servidor de bases de datos para los informes personalizados.  
  
### <a name="to-add-a-report-to-management-studio"></a>Para agregar un informe a Management Studio  
  
-   En [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)], haga clic con el botón derecho en un nodo del Explorador de objetos, seleccione **Informes**y haga clic en **Informes personalizados**. En el cuadro de diálogo **Abrir archivo** , busque la carpeta de informes personalizados, seleccione el archivo **ConnectionsReport.rdl** y, a continuación, haga clic en **Abrir**.  
  
    La primera vez que se abre un nuevo informe personalizado desde un nodo del Explorador de objetos, el informe personalizado se agrega a la lista de **Informes personalizados** usados más recientemente en el menú contextual de dicho nodo. Al abrir un informe estándar por primera vez, aparece además en la lista de informes usados más recientemente en **Informes personalizados**. Si se elimina un archivo de informe personalizado, la próxima vez que se seleccione el elemento aparecerá un mensaje que le indicará que elimine el elemento de la lista de informes usados más recientemente.  
  
    1.  Para cambiar el número de archivos que se muestran en esta lista, en el menú **Herramientas** , haga clic en **Opciones** , expanda la carpeta **Entorno** y, a continuación, haga clic en **General**.  
  
    2.  Ajuste el número de **Mostrar archivos de la lista de archivos recientes**.  
  
## <a name="see-also"></a>Vea también  
[Informes personalizados en Management Studio](../../ssms/object/custom-reports-in-management-studio.md)  
[Usar informes personalizados con las propiedades de nodo del Explorador de objetos](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[Anular la supresión de las advertencias de Ejecutar informe personalizado](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](http://msdn.microsoft.com/en-us/b8d18d3d-9db0-43e7-8286-7b46cc3a37ed)  
  

