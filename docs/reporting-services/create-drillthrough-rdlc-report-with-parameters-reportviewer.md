---
title: Crear un informe detallado (RDLC) con parámetros mediante - ReportViewer | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 21de137cefcfc61e91739ff33b2a9f0de4c3a05f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194374"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>Crear un informe detallado (RDLC) con parámetros mediante - ReportViewer
Un informe [detallado](https://technet.microsoft.com/library/ff519554.aspx) es un informe que los usuarios abren al hacer clic en un vínculo de otro informe. Este tipo de informes suele incluir información detallada acerca de los elementos del informe de resumen original. Este tutorial le guía a través de las lecciones siguientes para crear un informe detallado con parámetros y una consulta, en [informes en modo local](report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md).  
  
## <a name="requirements"></a>Requisitos  
Para usar este tutorial, debe tener acceso a la base de datos de ejemplo **AdventureWorks2014** . Para más información sobre cómo obtener la base de datos de ejemplo **AdventureWorks2014**, vea [Bases de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
Este tutorial supone que está familiarizado con las consultas de Transaction-SQL y los objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) y [DataTable](https://msdn.microsoft.com/library/system.data.datatable.aspx) de ADO.NET.  
  
Use Visual Studio 2015 y la aplicación web ASP.NET para crear una página web ASP.NET con un control ReportViewer. El control se configura para ver un informe que cree. En este tutorial, crea la aplicación en Microsoft Visual C#.  
  
## <a name="tasks"></a>Tareas  
[Lección 1: Crear un sitio Web nuevo](../reporting-services/lesson-1-create-a-new-web-site.md)  
[Lección 2: definir una conexión de datos y una tabla de datos para el informe primario](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[Lección 3: diseñar el informe primario con el Asistente para informes](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[Lección 4: definir una conexión de datos y una tabla de datos para el informe secundario](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[Lección 5: diseñar el informe secundario con el Asistente para informes](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[Lección 6: agregar un control ReportViewer a la aplicación](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[Lección 7: agregar una acción de obtención de detalles en el informe primario](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[Lección 8: crear un filtro de datos](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Consulte también  
[Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  

