---
title: Crear un informe de obtención de detalles (RDLC) con parámetros mediante ReportViewer (tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7efb713b5dbf9a3f19118bb3572ccd35778aad19
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109648"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>Crear un informe detallado (RDLC) con parámetros mediante ReportViewer (Tutorial de SSRS)
  Un informe [detallado](https://technet.microsoft.com/library/ff519554.aspx) es un informe que los usuarios abren al hacer clic en un vínculo de otro informe. Este tipo de informes suele incluir información detallada acerca de los elementos del informe de resumen original. Este tutorial le guía a través de las lecciones siguientes para crear un informe detallado con parámetros y una consulta, en [informes en modo local](local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
## <a name="requirements"></a>Requisitos  
 Para usar este tutorial, debe tener acceso a la base de datos de ejemplo **AdventureWorks2008** . La consulta que se usa en este tutorial también funcionará con la base de datos **AdventureWorks2012** . Para obtener más información sobre cómo obtener la base de datos de ejemplo **AdventureWorks2008** , vea [Tutorial: instalar la base de datos AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) para Microsoft Visual Studio 2010.  
  
 Este tutorial supone que está familiarizado con las consultas de Transaction-SQL y los objetos [DataSet](https://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) y [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) de ADO.NET.  
  
 Utilice Visual Studio 2010 o Visual Studio 2012 y el sitio Web ASP.NET para crear una página Web ASP.NET con un control ReportViewer. El control se configura para ver un informe que cree. En este tutorial, crea la aplicación en Microsoft Visual C#.  
  
## <a name="tasks"></a>Tareas  
 [Lección 1: crear un nuevo sitio web](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [Lección 2: definir una conexión de datos y una tabla de datos para el informe primario](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [Lección 3: diseñar el informe primario usando el Asistente para informes](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [Lección 4: definir una conexión de datos y una tabla de datos para el informe secundario](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [Lección 5: diseñar el informe secundario con el Asistente para informes](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [Lección 6: agregar un control ReportViewer a la aplicación](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [Lección 7: agregar una acción de obtención de detalles en el informe primario](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [Lección 8: crear un filtro de datos](../reporting-services/lesson-8-create-a-data-filter.md)   
 [Lección 9: compilar y ejecutar la aplicación](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  
