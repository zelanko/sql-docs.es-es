---
title: Uso de informes | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d71bcb0f6c695f540f1d38b1418c2c3282afea58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104394"
---
# <a name="using-reports"></a>Utilizar los informes
  Se genera un informe independiente para cada componente y, cuando es necesario, para cada instancia, los cuales analiza el Asistente para análisis del Asesor de actualizaciones en un servidor. El informe proporciona detalles sobre los problemas conocidos que afectan a una actualización. También proporciona vínculos a información y acciones recomendadas para resolver los problemas identificados.  
  
> [!NOTE]  
>  Si el Visor de informes del Asesor de actualizaciones no encuentra ningún informe en el directorio de informes predeterminado, puede cargar un informe desde un directorio diferente mediante el uso de la **abrir informe** vínculo.  
  
## <a name="viewing-reports"></a>Ver informes  
 Puede usar el Visor de informes del Asesor de actualizaciones para ver los informes del Asesor de actualizaciones. Para ver informes, en la página de inicio del Asesor de actualizaciones, haga clic en **iniciar el Visor de informes de Asesor de actualizaciones**.  
  
 Después de cargar un informe de un servidor, puede seleccionar un componente cuyos problemas de actualización desee ver. Puede aplicar un filtro de la **filtrar por** cuadro para ver el siguiente:  
  
-   Todos los problemas  
  
-   Todos los problemas de actualización  
  
-   Problemas anteriores a la actualización  
  
-   Todos los problemas de migración  
  
-   Problemas resueltos  
  
-   Problemas sin resolver  
  
 Si el informe tiene más de 20 problemas, puede mover al grupo siguiente o anterior de problemas, haga clic en **20 siguientes** o **20 anteriores** en la parte superior o inferior de la lista de problemas.  
  
 Puede ver hasta cinco informes guardados seleccionando los informes desde el **informe** cuadro de lista desplegable. Los informes se enumeran según la marca de tiempo establecida durante su generación.  
  
## <a name="report-format"></a>Formato de informe  
 El Visor de informes muestra los problemas del informe en tres columnas. Cada problema se puede contraer, de forma que puede ocultar la descripción y ver únicamente la información más importante.  
  
 La primera columna es el **importancia** columna. Los iconos indican la importancia de cada problema, mostrando un círculo rojo con una X para aquellos problemas importantes o un triángulo amarillo con un signo de admiración para problemas de tipo advertencia o que proporcionan información. La segunda columna, **cuándo solucionarlo**, indica cuándo debería resolver el problema. Puede ordenar el informe en función del **importancia** o **cuándo solucionarlo** columna. La tercera columna, **descripción**, muestra el título del problema.  
  
 Puede expandir un problema para ver información adicional, un vínculo a información detallada acerca de cómo resolver el problema y un vínculo para mostrar los detalles del problema. Al hacer clic en el vínculo para obtener información detallada acerca del problema, se muestra un tema de ayuda con información detallada acerca del problema, así como instrucciones específicas acerca de cómo solucionarlo. Después de haber corregido un problema o para administrar los elementos de acción, puede marcar los problemas como completados seleccionando la **ha resuelto este problema** casilla de verificación. Si desea quitar los problemas resueltos en la lista de problemas de actualización, haga clic en **actualizar**. El problema no se muestra otra vez hasta que se ejecute el Asistente para análisis Asesor de actualizaciones en el mismo componente o aplicar el **problemas resueltos** filtrar entre los **filtrar por** opción.  
  
## <a name="report-files"></a>Archivos de informe  
 El Asistente para análisis Asesor de actualizaciones crea informes en Mis documentos\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorio Upgrade Advisor\110\Reports y crea un subdirectorio para cada servidor que se analice. Los archivos de informe son archivos XML que siguen una convención de nomenclatura concreta. Al iniciar el Visor de informes del Asistente de actualizaciones, se muestran los archivos de informe del directorio predeterminado. Si copia los archivos de informe en esta carpeta, deben cumplir la convención de nomenclatura o el Visor de informes no los mostrará automáticamente.  
  
 Si desea compartir la información con otras personas, puede enviarles el informe XML. O, si desea utilizar otra aplicación, puede exportar el informe en un archivo de valores separados por comas que puede utilizar para crear una hoja de cálculo, un archivo de texto o un mensaje de correo electrónico.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: ver un informe del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Cómo: exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Cómo: filtrar informes](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
