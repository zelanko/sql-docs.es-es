---
title: Herramientas y enfoques de procesamiento (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 66696d32b62f29df7a4a1866978d72f5d4a173ff
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072819"
---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>Herramientas y enfoques de procesamiento (Analysis Services)
  El procesamiento es una operación en la que Analysis Services consulta un origen de datos relacional y rellena objetos de Analysis Services utilizando esos datos.  
  
 Como administrador del sistema de Analysis Services, puede ejecutar y supervisar el procesamiento de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizando estos enfoques:  
  
-   Ejecutar el análisis de impacto para conocer las dependencias del objeto y el ámbito de las operaciones  
  
-   Procesar objetos individuales en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Procesar objetos individuales o varios objetos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   Ejecutar el análisis de impacto para revisar una lista de objetos relacionados que estarán en estado no procesado como resultado de la acción actual  
  
-   Generar y ejecutar un script en una ventana Consulta XMLA de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para procesar objetos individuales o varios objetos  
  
-   Utilizar cmdlets de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell  
  
-   Usar flujos de control y tareas en paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
-   Supervisar el procesamiento con SQL Server Profiler  
  
-   Programar una solución personalizada mediante AMO Para más información, consulte [Programming AMO OLAP Basic Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects).  
  
 El procesamiento es una operación altamente configurable, controlada por un conjunto de opciones de procesamiento que determinan si se produce un procesamiento completo o incremental en el nivel de objeto. Para más información sobre las opciones de procesamiento, vea [Opciones y valores de procesamiento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md) y [Procesar objetos de Analysis Services](processing-analysis-services-objects.md).  
  
> [!NOTE]  
>  En este tema se describen las herramientas y los enfoques para procesar modelos multidimensionales. Para obtener más información acerca de cómo procesar los modelos tabulares, vea [procesar base de datos, tabla o partición](../tabular-models/process-database-table-or-partition-analysis-services.md) y [procesar datos &#40;Tabular de SSAS&#41;](../process-data-ssas-tabular.md).  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>Procesar objetos en SQL Server Management Studio  
  
1.  Inicie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y conéctese a Analysis Services.  
  
2.  Haga clic con el botón derecho en el objeto de Analysis Services que quiera procesar y haga clic en **Procesar**. Puede procesar datos en cualquiera de estos niveles:  
  
    -   Bases de datos  
  
    -   Cubos  
  
    -   Grupos de medida o particiones individuales en el grupo de medida  
  
    -   Dimensions  
  
    -   Modelos de minería de datos  
  
    -   Estructuras de minería de datos  
  
     Los objetos de Analysis Services son jerárquicos. Si elige una base de datos, el procesamiento puede producirse para todos los objetos contenidos en la base de datos. El hecho de que el procesamiento se produzca realmente variará en función de la opción de proceso que se seleccione y del estado del objeto. Concretamente, si un objeto no está procesado, el procesamiento de su objeto primario dará lugar al procesamiento de dicho objeto. Para obtener más información sobre las dependencias de objetos, vea [Processing Analysis Services Objects](processing-analysis-services-objects.md).  
  
3.  En el cuadro de diálogo **Procesar** , en **Opciones de proceso**, use el valor predeterminado proporcionado o seleccione una opción diferente de la lista. Para más información sobre cada opción, vea [Opciones y valores de procesamiento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
4.  Haga clic en **Análisis de impacto** para identificar y, opcionalmente, procesar objetos dependientes que se ven afectados si se procesan los objetos enumerados en el cuadro de diálogo Procesar.  
  
5.  Opcionalmente, haga clic en **Cambiar configuración** para modificar el orden de procesamiento, el comportamiento de procesamiento relativo a tipos de errores concretos y otras opciones de configuración.  
  
6.  Haga clic en **Aceptar**.  
  
     El cuadro de diálogo Progreso del proceso proporciona el estado actual de cada comando. Si un mensaje de estado aparece truncado, puede hacer clic en **Ver detalles** para leer la totalidad del mismo.  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>Procesar objetos en Herramientas de datos de SQL Server  
  
1.  Inicie [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y abra un proyecto que se haya implementado.  
  
2.  En el Explorador de soluciones, debajo del proyecto implementado, expanda la carpeta **Dimensiones** .  
  
3.  Haga clic con el botón derecho en una dimensión y, después, haga clic en **Procesar**. Puede hacer clic con el botón secundario en varias dimensiones para procesar varios objetos de una vez. Para más información, vea [Procesamiento por lotes &#40;Analysis Services&#41;](batch-processing-analysis-services.md).  
  
4.  En el cuadro de diálogo **Procesar dimensión** , en la columna **Opciones de proceso** debajo de **Lista de objetos**, compruebe que la opción en esta columna sea **Procesar completo**. En caso contrario, en **Opciones de proceso**, haga clic en la opción y seleccione **Proceso completo** en la lista desplegable.  
  
5.  Haga clic en **Ejecutar**.  
  
6.  Cuando el procesamiento haya finalizado, haga clic en **Cerrar**.  
  
##  <a name="bkmk_impactanalysis"></a> Ejecutar el análisis de impacto para identificar las dependencias del objeto y el ámbito de las operaciones  
  
1.  Antes de procesar un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], puede analizar el efecto sobre los objetos relacionados haciendo clic en **Análisis de impacto** en uno de los cuadros de diálogo **Procesar objetos** .  
  
2.  Haga clic con el botón derecho en una dimensión, cubo, grupo de medida o partición para abrir un cuadro de diálogo **Procesar objetos** .  
  
3.  Haga clic en **Análisis de impacto** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] examina el modelo e informa de los requisitos de nuevo procesamiento de los objetos relacionados con el objeto seleccionado para procesar.  
  
### <a name="processing-objects-using-xmla"></a>Procesar objetos utilizando XMLA  
  
1.  Inicie [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y conéctese a Analysis Services.  
  
2.  Haga clic con el botón derecho en el objeto que quiera procesar y, después, haga clic en **Procesar**.  
  
3.  En el cuadro de diálogo **Procesar** , seleccione la opción de proceso que desee utilizar. Modifique las opciones de configuración que desee. Ejecute el análisis de impacto para identificar los cambios que pueda necesitar realizar.  
  
4.  Haga clic en **Script** en la pantalla **Procesar objetos** .  
  
     Este paso genera un script XMLA y abre una ventana Consulta XMLA de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
5.  Cierre el cuadro de diálogo. El script contiene el comando y las opciones de procesamiento que se especificaron en el cuadro de diálogo.  
  
6.  Opcionalmente, puede continuar agregando al script si desea procesar objetos adicionales en el mismo lote. Para continuar, repita los pasos anteriores, anexando el script generado de forma que tenga un script único para todas las operaciones de procesamiento. Para obtener un ejemplo, vea [Schedule SSAS Administrative Tasks with SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md).  
  
7.  En la barra de menús, haga clic en **Consulta**y, a continuación, en **Ejecutar**.  
  
### <a name="processing-objects-using-powershell"></a>Procesar objetos utilizando PowerShell  
  
1.  A partir de esta versión de SQL Server, puede utilizar los cmdlets de Analysis Services PowerShell para procesar objetos. Los cmdlets siguientes pueden ejecutarse de forma interactiva o en un script:  
  
    -   [Cmdlet Invoke-ProcessCube](/sql/analysis-services/powershell/invoke-processcube-cmdlet)  
  
    -   [Cmdlet Invoke-ProcessDimension](/sql/analysis-services/powershell/invoke-processdimension-cmdlet)  
  
    -   [Cmdlet Invoke-ProcessPartition](/sql/analysis-services/powershell/invoke-processpartition-cmdlet)  
  
    -   El[cmdlet Invoke-ASCmd](/sql/analysis-services/powershell/invoke-ascmd-cmdlet), que se puede usar para ejecutar un script XMLA, MDX o DMX que incluya comandos de procesamiento.  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>Supervisar el procesamiento de objetos mediante SQL Server Profiler  
  
1.  Conéctese a una instancia de Analysis Services en SQL Server Profiler.  
  
2.  En Selección de eventos, haga clic en **Mostrar todos los eventos** para agregar todos los eventos a la lista.  
  
3.  Elija los siguientes eventos:  
  
    -   **Inicio del comando** y **Fin del comando** para mostrar cuándo se inicia y se detiene el procesamiento  
  
    -   **Error** para capturar errores  
  
    -   **Informe de progreso Inicio**, **Informe de progreso Actual**y **Fin del informe de progreso** para informar del estado del proceso y mostrar las consultas SQL usadas para recuperar los datos  
  
    -   **Ejecutar script MDX Inicio** y **Ejecutar script MDX Final** para mostrar los cálculos del cubo  
  
    -   Opcionalmente, agregue eventos de bloqueo si está diagnosticando problemas de rendimiento relacionados con el procesamiento  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>Procesar objetos de Analysis Services mediante Integration Services  
  
1.  En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], cree un paquete que use la tarea Procesamiento de Analysis Services para rellenar automáticamente objetos con datos nuevos cuando realice actualizaciones periódicas de la base de datos relacional de origen.  
  
2.  En **Cuadro de herramientas de SSIS**, haga doble clic en **Procesamiento de Analysis Services** para agregarlo al paquete.  
  
3.  Edite la tarea para especificar una conexión con la base de datos, qué objetos se van a procesar y la opción de proceso. Para obtener más información acerca de cómo implementar esta tarea, vea [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md)  
  
  
