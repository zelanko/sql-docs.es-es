---
title: Uso de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eb2537af2539854f0f66e3f6c39c3b6e5315ec6f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989763"
---
# <a name="using-reports"></a>Utilizar los informes
  Se genera un informe independiente para cada componente y, cuando es necesario, para cada instancia, los cuales analiza el Asistente para análisis del Asesor de actualizaciones en un servidor. El informe proporciona detalles sobre los problemas conocidos que afectan a una actualización. También proporciona vínculos a información y acciones recomendadas para resolver los problemas identificados.  
  
> [!NOTE]  
>  Si el Visor de informes del Asesor de actualizaciones no encuentra ningún informe en el directorio de informes predeterminado, puede cargar un informe desde un directorio diferente mediante la **abrir informe** vínculo.  
  
## <a name="viewing-reports"></a>Ver informes  
 Puede usar el Visor de informes del Asesor de actualizaciones para ver los informes del Asesor de actualizaciones. Para ver informes, en la página de inicio del Asesor de actualizaciones, haga clic en **iniciar Visor de informes de Asesor de actualizaciones**.  
  
 Después de cargar un informe de un servidor, puede seleccionar un componente cuyos problemas de actualización desee ver. Puede aplicar un filtro en el **filtrar por** cuadro para ver lo siguiente:  
  
-   Todos los problemas  
  
-   Todos los problemas de actualización  
  
-   Problemas anteriores a la actualización  
  
-   Todos los problemas de migración  
  
-   Problemas resueltos  
  
-   Problemas sin resolver  
  
 Si el informe tiene más de 20 problemas, puede mover al grupo siguiente o anterior de problemas haciendo **20 siguientes** o **20 anteriores** en la parte superior o inferior de la lista de problemas.  
  
 Puede ver hasta cinco informes guardados seleccionando los informes desde el **informe** cuadro de lista desplegable. Los informes se enumeran según la marca de tiempo establecida durante su generación.  
  
## <a name="report-format"></a>Formato de informe  
 El Visor de informes muestra los problemas del informe en tres columnas. Cada problema se puede contraer, de forma que puede ocultar la descripción y ver únicamente la información más importante.  
  
 La primera columna es el **importancia** columna. Los iconos indican la importancia de cada problema, mostrando un círculo rojo con una X para aquellos problemas importantes o un triángulo amarillo con un signo de admiración para problemas de tipo advertencia o que proporcionan información. La segunda columna, **cuándo solucionarlo**, indica cuándo debe resolver el problema. Puede ordenar el informe en función del **importancia** o **cuándo solucionarlo** columna. La tercera columna, **descripción**, muestra el título del problema.  
  
 Puede expandir un problema para ver información adicional, un vínculo a información detallada acerca de cómo resolver el problema y un vínculo para mostrar los detalles del problema. Al hacer clic en el vínculo para obtener información detallada acerca del problema, se muestra un tema de ayuda con información detallada acerca del problema, así como instrucciones específicas acerca de cómo solucionarlo. Después de haber corregido un problema o para administrar los elementos de acción, puede marcar problemas como completados si activa la **este problema se ha resuelto** casilla de verificación. Si desea quitar los problemas resueltos en la lista de problemas de actualización, haga clic en **actualizar**. El problema no se muestra otra vez hasta que se ejecutó el Asistente para actualizar un análisis del Asistente para el mismo componente o aplicar el **problemas resueltos** filtrar desde el **filtrar por** opción.  
  
## <a name="report-files"></a>Archivos de informe  
 El Asistente para actualizar Analysis Advisor crea informes en los documentos de mi\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directory Upgrade Advisor\110\Reports y crea un subdirectorio para cada servidor que se analice. Los archivos de informe son archivos XML que siguen una convención de nomenclatura concreta. Al iniciar el Visor de informes del Asistente de actualizaciones, se muestran los archivos de informe del directorio predeterminado. Si copia los archivos de informe en esta carpeta, deben cumplir la convención de nomenclatura o el Visor de informes no los mostrará automáticamente.  
  
 Si desea compartir la información con otras personas, puede enviarles el informe XML. O, si desea utilizar otra aplicación, puede exportar el informe en un archivo de valores separados por comas que puede utilizar para crear una hoja de cálculo, un archivo de texto o un mensaje de correo electrónico.  
  
## <a name="see-also"></a>Vea también  
 [Cómo: Ver un informe del Asesor de actualizaciones](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Cómo: Exportar informes](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Cómo: Informes de filtro](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Resolver problemas de actualización](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
