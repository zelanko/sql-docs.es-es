---
title: Crear un informe detallado (RDLC) con parámetros mediante ReportViewer (Tutorial de SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 2124efb2b773f76b6d117d9163b159affb79ffac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198635"
---
# <a name="create-a-drillthrough-rdlc-report-with-parameters-using-reportviewer-ssrs-tutorial"></a>Crear un informe detallado (RDLC) con parámetros mediante ReportViewer (Tutorial de SSRS)
  Un informe [detallado](http://technet.microsoft.com/library/ff519554.aspx) es un informe que los usuarios abren al hacer clic en un vínculo de otro informe. Este tipo de informes suele incluir información detallada acerca de los elementos del informe de resumen original. Este tutorial le guía a través de las lecciones siguientes para crear un informe detallado con parámetros y una consulta, en [informes en modo local](http://msdn.microsoft.com/library/ff487969.aspx).  
  
## <a name="requirements"></a>Requisitos  
 Para usar este tutorial, debe tener acceso a la **AdventureWorks2008** base de datos de ejemplo. La consulta usada en este tutorial también funcionará con **AdventureWorks2012** base de datos. Para obtener más información sobre cómo obtener el **AdventureWorks2008** base de datos de ejemplo, vea [Tutorial: instalar la base de datos de AdventureWorks](http://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx) para Microsoft Visual Studio 2010.  
  
 En este tutorial se da por supuesto que está familiarizado con las consultas Transaction-SQL y ADO.NET [conjunto de datos](http://msdn.microsoft.com/library/system.data.dataset\(v=vs.100\).aspx) y [DataTable](http://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) objetos.  
  
 Utilice Visual Studio 2010 o Visual Studio 2012 y el sitio Web ASP.NET para crear una página Web ASP.NET con un control ReportViewer. El control se configura para ver un informe que cree. En este tutorial, crea la aplicación en Microsoft Visual C#.  
  
## <a name="tasks"></a>Tareas  
 [Lección 1: Crear un nuevo sitio Web](../reporting-services/lesson-1-create-a-new-web-site.md)   
 [Lección 2: Definir una conexión de datos y la tabla de datos para el informe primario](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)   
 [Lección 3: Diseñar el informe primario usando al Asistente para informes](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)   
 [Lección 4: Definir una conexión de datos y la tabla de datos para el informe secundario](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)   
 [Lección 5: Diseñar el informe secundario usando al Asistente para informes](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)   
 [Lección 6: Agregar un Control ReportViewer a la aplicación](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)   
 [Lección 7: Agregar una acción de obtención de detalles en el informe primario](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)   
 [Lección 8: Crear un filtro de datos](../reporting-services/lesson-8-create-a-data-filter.md)   
 [Lección 9: compilar y ejecutar la aplicación](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)   
 [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
  
  