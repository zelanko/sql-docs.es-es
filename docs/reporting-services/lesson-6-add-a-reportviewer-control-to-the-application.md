---
title: "Lección 6: Agregar un Control ReportViewer a la aplicación | Documentos de Microsoft"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
caps.latest.revision: 7
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 914d8abf2ad7b72b5ce1035da2867c47b67dfa14
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>Lección 6: agregar un control ReportViewer a la aplicación
Después de diseñar el informe secundario con el Asistente de informes, el paso siguiente consiste en agregar un control ReportViewer a la aplicación del sitio Web. Si usa el sitio web de informes ASP.NET, habrá agregado el control ReportViewer a la página default.aspx.   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>Para agregar un control ReportViewer a la aplicación  
  
1.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Default.aspx**y, después, haga clic en **Diseñador de vistas**.  
  
2.  Si default.aspx ya tiene el control ReportViewer en él, vaya al **Paso 4**. En caso contrario, en el grupo **Extensiones AJAX** , en la ventana **Cuadro de herramientas** , arrastre un control **ScriptManager** a la superficie de diseño.  
  
3.  En el grupo **Reporting** , arrastre un control **ReportViewer** a la superficie de diseño debajo del control **ScriptManager** .  
  
4.  Haga clic en la flecha de la esquina superior derecha del control **ReportViewer** para abrir la ventana **Tareas de ReportViewer** .  
  
5.  En el cuadro **Elegir informe** , seleccione el informe primario que ha creado.  
  
    Al seleccionar un informe, las instancias de los orígenes de datos usados en el informe se crean automáticamente. El código se genera para crear una instancia de cada DataTable (y el contenedor [DataSet](http://msdn.microsoft.com/library/system.data.dataset.aspx) ). Un control [ObjectDataSource](http://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx) se agrega a la superficie de diseño, correspondiente a cada origen de datos usado en el informe. Este control de origen de datos se configura automáticamente.  
  
6.  En el menú Compilar, haga clic en Compilar sitio Web.  
  
    Se compila el informe y errores como un error de sintaxis en una expresión de informe aparecen en el área de **Lista de errores** . Haga clic en **Lista de errores** en la parte inferior de la ventana de Visual Studio para mostrar el área de **Lista de errores** .  
  
## <a name="next-task"></a>Tarea siguiente  
Ha agregado correctamente un control ReportViewer a la aplicación del sitio Web. Después, agregará una acción de obtención de detalles en el informe primario. Consulte [Lección 7: Agregar una acción de obtención de detalles en el informe primario](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md).  
  


