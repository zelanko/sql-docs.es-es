---
title: Informe de evaluación (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5202655839821515939ea920779041d6f39db28f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="assessment-report-accesstosql"></a>Informe de evaluación (AccessToSQL)
Los resultados de la conversión de objetos de base de datos que muestra la ventana de informe de evaluación [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para crear un informe de evaluación, seleccionar objetos para convertir en el Explorador de metadatos de origen, haga clic en **bases de datos**y, a continuación, seleccione **crear informe**. También puede mostrar este informe automáticamente después de convertir esquemas. Sin embargo, el nombre del informe será el informe de conversión. Para obtener más información, consulte [configuración de proyecto (GUI) (SSMA común)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
## <a name="options"></a>Opciones  
**Panel del explorador**  
Contiene una jerarquía de objetos en el informe de evaluación. Expanda las carpetas para ver los subcomponentes y objetos individuales. Al hacer clic en una categoría o un objeto, las estadísticas de conversión de dicha categoría u objeto aparecen en el panel de detalles.  
  
**Panel de detalles**  
Muestra los mensajes de estadísticas o error y advertencia para el objeto seleccionado de la conversión. Por ejemplo, si se selecciona la carpeta tablas, el panel de detalles mostrará los números de las claves externas, índices, claves principales y las tablas que se convirtieron.  
  
**Panel mensajes**  
Muestra los errores, advertencias y mensajes informativos que se generaron cuando se creó el informe de evaluación. Los mensajes se agrupan por número.  
  
Para ver los detalles del mensaje, haga clic en **errores**, **advertencias**, o **mensajes**y, a continuación, expanda un mensaje. SSMA mostrará la lista de objetos que tienen este error. Haga clic en un objeto para mostrar todos los detalles de conversión para el objeto.  
  
## <a name="see-also"></a>Vea también  
[Reference(Access) de interfaz de usuario](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)  
  
