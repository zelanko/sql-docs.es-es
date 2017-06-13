---
title: "Crear informe detallado (RDLC) con los parámetros - ReportViewer | Documentos de Microsoft"
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
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8ce79884745b9e2fc9fbddfd7d312e982b2dd61c
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>Crear informe detallado (RDLC) con los parámetros - ReportViewer
Un informe [detallado](http://technet.microsoft.com/library/ff519554.aspx) es un informe que los usuarios abren al hacer clic en un vínculo de otro informe. Este tipo de informes suele incluir información detallada acerca de los elementos del informe de resumen original. Este tutorial le guía a través de las lecciones siguientes para crear un informe detallado con parámetros y una consulta, en [informes en modo local](http://msdn.microsoft.com/library/ff487969.aspx).  
  
## <a name="requirements"></a>Requisitos  
Para usar este tutorial, debe tener acceso a la base de datos de ejemplo **AdventureWorks2014** . Para obtener más información sobre cómo obtener la base de datos de ejemplo **AdventureWorks2014** , consulte [Microsoft SQL Server Database Product Samples](http://msftdbprodsamples.codeplex.com/)(Ejemplos de productos de bases de datos de Microsoft SQL Server).  
  
Este tutorial supone que está familiarizado con las consultas de Transaction-SQL y los objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset.aspx) y [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) de ADO.NET.  
  
Use Visual Studio 2015 y la aplicación web ASP.NET para crear una página web ASP.NET con un control ReportViewer. El control se configura para ver un informe que cree. En este tutorial, crea la aplicación en Microsoft Visual C#.  
  
## <a name="tasks"></a>Tareas  
[Lección 1: Crear un sitio Web nuevo](../reporting-services/lesson-1-create-a-new-web-site.md)  
[Lección 2: Definir una conexión de datos y una tabla de datos para el informe primario](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[Lección 3: Diseñar el informe primario usando el Asistente para informes](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[Lección 4: Definir una conexión de datos y una tabla de datos para el informe secundario](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[Lección 5: Diseñar el informe secundario usando el Asistente para informes](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[Lección 6: agregar un control ReportViewer a la aplicación](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[Lección 7: Agregar una acción de obtención de detalles en el informe primario](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[Lección 8: Crear un filtro de datos](../reporting-services/lesson-8-create-a-data-filter.md)  
[Lesson 9: Build and Run the Application](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Vea también  
[Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  


