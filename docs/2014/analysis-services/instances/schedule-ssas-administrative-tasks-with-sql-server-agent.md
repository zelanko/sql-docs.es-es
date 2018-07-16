---
title: Programar tareas administrativas de SSAS con el Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2d1484b3-51d9-48a0-93d2-0c3e4ed22b87
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e02a5f91994d0002873984a6e77db53169d024e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37243685"
---
# <a name="schedule-ssas-administrative-tasks-with-sql-server-agent"></a>Programar tareas administrativas de SSAS con el Agente SQL Server
  Con el servicio Agente SQL Server, puede programar tareas administrativas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se ejecutan en el orden y a las horas que se necesitan. Las tareas programadas le ayudan a automatizar los procesos que se ejecutan en ciclos normales o predecibles. Puede programar tareas administrativas, como procesamiento de cubos, para que se ejecuten en momentos de poca actividad empresarial. También puede determinar el orden en el que se ejecutarán las tareas creando pasos de trabajo en un trabajo del Agente SQL Server. Por ejemplo, puede procesar un cubo y luego realizar una copia de seguridad del cubo.  
  
 Los pasos de trabajo le permiten controlar el flujo de ejecución. Si se produce un error en un trabajo, puede configurar el Agente SQL Server para continuar ejecutando las tareas restantes o para detener la ejecución. También puede configurar el Agente SQL Server para enviar notificaciones del éxito o el fracaso de la ejecución del trabajo.  
  
 Este tema es un tutorial que muestra dos formas de usar el Agente SQL Server para ejecutar el script XMLA. El primer ejemplo demuestra cómo programar el procesamiento de una sola dimensión. El segundo ejemplo muestra cómo combinar tareas de procesamiento en un único script que se ejecuta según una programación. Para completar este tutorial, deberá cumplir los siguientes requisitos previos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Se debe instalar el servicio del Agente SQL Server.  
  
 De forma predeterminada, trabajos se ejecutan con la cuenta de servicio. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la cuenta predeterminada para el Agente SQL Server es NT Service\SQLAgent$\<instancename >. Para realizar una tarea de copia de seguridad o de procesamiento, esta cuenta debe ser administrador del sistema en la instancia de Analysis Services. Para obtener más información, consulte [conceder permisos de administrador de servidor &#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
 También debe tener una base de datos de prueba para trabajar con ella. Puede implementar la base de datos de ejemplo multidimensional AdventureWorks o un proyecto del tutorial multidimensional de Analysis Services para usarlo en este tutorial. Para más información, consulte [Instalar los datos y proyectos de ejemplo para el tutorial de modelado multidimensional de Analysis Services](../install-sample-data-and-projects.md).  
  
## <a name="example-1-processing-a-dimension-in-a-scheduled-task"></a>Ejemplo 1: procesar una dimensión en una tarea programada  
 Este ejemplo muestra cómo crear y programar un trabajo que procesa una dimensión.  
  
 Una tarea programada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es un script XMLA incrustado en un trabajo del Agente SQL Server. Este trabajo se programa para ejecutarse en los momentos y con la frecuencia deseados. Dado que el Agente SQL Server es parte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se trabaja con el motor de base de datos y con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para crear y programar una tarea administrativa.  
  
###  <a name="bkmk_CreateScript"></a> Crear un script para procesar una dimensión en un trabajo del Agente SQL Server  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Abra una carpeta de base de datos y busque una dimensión. Haga clic con el botón derecho en la dimensión y seleccione **Procesar**.  
  
2.  En el cuadro de diálogo **Procesar dimensión** , en la columna **Opciones de proceso** debajo de **Lista de objetos**, compruebe que la opción en esta columna sea **Procesar completo**. De lo contrario, en **Opciones de proceso**, haga clic en la opción y, después, seleccione **Proceso completo** en la lista desplegable.  
  
3.  Haga clic **Script**.  
  
     Este paso abre una ventana **Consulta XML** que contiene el script XMLA que procesa la dimensión.  
  
4.  En el cuadro de diálogo **Procesar dimensión** , haga clic en **Cancelar** para cerrar el cuadro de diálogo.  
  
5.  En la ventana **Consulta XMLA** , resalte el script XMLA, haga clic con el botón derecho en el script resaltado y seleccione **Copiar**.  
  
     Este paso copia el script XMLA en el Portapapeles de Windows. Puede dejar el script XMLA en el portapapeles o pegarlo en el Bloc de notas u otro editor de texto. A continuación, se muestra un ejemplo del script XMLA.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Account</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
###  <a name="bkmk_ProcessJob"></a> Crear y programar el trabajo de procesamiento de dimensiones  
  
1.  Conéctese a una instancia del Motor de base de datos y, a continuación, abra el Explorador de objetos.  
  
2.  Expanda **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en **Trabajos** y seleccione **Nuevo trabajo**.  
  
4.  En el cuadro de diálogo **Nuevo trabajo** , escriba un nombre de trabajo en **Nombre**.  
  
5.  En **Seleccione una página**, seleccione **Pasos**y, a continuación, haga clic en **Nuevo**.  
  
6.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre de paso en **Nombre del paso**.  
  
7.  En **Servidor**, escriba **localhost** para una instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y **localhost\\**\<*nombre de instancia*> para una instancia con nombre.  
  
     Si va a ejecutar el trabajo desde un equipo remoto, use el nombre de servidor y el nombre de instancia donde se ejecutará el trabajo. Use el formato \< *nombre del servidor*> para una instancia predeterminada, y \< *nombre del servidor*>\\<*instancia nombre*> para una instancia con nombre.  
  
8.  En **Tipo**, seleccione **Comando de SQL Server Analysis Services**.  
  
9. En **Comando**, haga clic con el botón derecho y seleccione **Pegar**. El script XMLA que generó en el paso anterior debe aparecer en la ventana de comandos.  
  
10. Haga clic en **Aceptar**.  
  
11. En **Seleccione una página**, haga clic en **Programaciones**y, a continuación, haga clic en **Nuevo**.  
  
12. En el cuadro de diálogo **Nueva programación del trabajo** , escriba un nombre de programación en **Nombre**y, a continuación, haga clic en **Aceptar**.  
  
     Este paso crea una programación para domingo a las 12:00. El paso siguiente muestra cómo ejecutar manualmente el trabajo. También puede especificar una programación que ejecuta el trabajo cuando lo está supervisando.  
  
13. En el cuadro de diálogo **Nuevo trabajo** , haga clic en **Aceptar**.  
  
14. En el **Explorador de objetos**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que creó y, después, seleccione **Iniciar trabajo en el paso**.  
  
     Dado que el trabajo tiene un solo paso, el trabajo se ejecuta inmediatamente. Si el trabajo contuviera varios pasos, podría seleccionar el paso en el que el trabajo debe iniciarse.  
  
15. Cuando finalice el trabajo, haga clic **Cerrar**.  
  
## <a name="example-2-batch-processing-a-dimension-and-a-partition-in-a-scheduled-task"></a>Ejemplo 2: procesamiento por lotes de una dimensión y una partición en una tarea programada  
 Los procedimientos de este ejemplo demuestran cómo crear y programar una trabajo que procese por lotes una dimensión de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y al mismo tiempo procesar una partición de cubo que dependa de la dimensión para la agregación. Para obtener más información sobre el procesamiento por lotes de objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Procesamiento por lotes &#40;Analysis Services&#41;](../multidimensional-models/batch-processing-analysis-services.md).  
  
###  <a name="bkmk_BatchProcess"></a> Crear un script para el procesamiento por lotes de una dimensión y una partición en un trabajo del Agente SQL Server  
  
1.  Con la misma base de datos, expanda **Dimensiones**, haga clic con el botón derecho en la dimensión **Cliente** y seleccione **Procesar**.  
  
2.  En el cuadro de diálogo **Procesar dimensión** , en la columna **Opciones de proceso** debajo de **Lista de objetos**, compruebe que la opción en esta columna sea **Procesar completo**.  
  
3.  Haga clic **Script**.  
  
     Este paso abre una ventana **Consulta XML** que contiene el script XMLA que procesa la dimensión.  
  
4.  En el cuadro de diálogo **Procesar dimensión** , haga clic en **Cancelar** para cerrar el cuadro de diálogo.  
  
5.  Expanda **Cubos**, **Adventure Works**, **Grupos de medida**, **Venta por Internet**y **Particiones**; haga clic con el botón derecho en la última partición de la lista y seleccione **Proceso**.  
  
6.  En el cuadro de diálogo **Procesar partición** , en la columna **Opciones de proceso** debajo de **Lista de objetos**, compruebe que la opción en esta columna sea **Procesar completo**.  
  
7.  Haga clic **Script**.  
  
     Este paso abre una segunda ventana **Consulta XML** que contiene el script XMLA que procesa la partición.  
  
8.  En el cuadro de diálogo **Procesar partición** , haga clic en **Cancelar** para cerrar el editor.  
  
     En este punto debe combinar los dos scripts y asegurarse de que la dimensión se procesa en primer lugar.  
  
    > [!WARNING]  
    >  Si la partición se procesa en primer lugar, el procesamiento posterior de la dimensión provoca que la partición se quede sin procesar. La partición requeriría un segundo procesamiento para alcanzar el estado de procesada.  
  
9. En la ventana **Consulta XMLA** que contiene el script XMLA que procesa la partición, resalte el código que hay dentro de las etiquetas `Batch` y `Parallel` , haga clic con el botón derecho en el script resaltado y seleccione **Copiar**.  
  
    ```  
    <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID> Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
    ```  
  
10. Abra la ventana **Consulta XMLA** que contiene el script XMLA que procesa la dimensión. Haga clic con el botón derecho en el script situado a la izquierda de la etiqueta `</Process>` y seleccione **Pegar**.  
  
     El ejemplo siguiente muestra el script XMLA revisado.  
  
    ```  
    <Batch xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Parallel>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <DimensionID>Dim Customer</DimensionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
      <Process xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
        <Object>  
          <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2004</PartitionID>  
        </Object>  
        <Type>ProcessFull</Type>  
        <WriteBackTableCreation>UseExisting</WriteBackTableCreation>  
      </Process>  
     </Parallel>  
    </Batch>  
    ```  
  
11. Resalte el script XMLA revisado, haga clic con el botón derecho en el script resaltado y seleccione **Copiar**.  
  
12. Este paso copia el script XMLA en el Portapapeles de Windows. Puede dejar el script XMLA en el portapapeles, guardarlo en un archivo o pegarlo en el Bloc de notas u otro editor de texto.  
  
###  <a name="bkmk_Scheduling"></a> Crear y programar el trabajo de procesamiento por lotes  
  
1.  Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, a continuación, abra el Explorador de objetos.  
  
2.  Expanda **Agente SQL Server**. Inicie el servicio, si no se está ejecutando.  
  
3.  Haga clic con el botón derecho en **Trabajos** y seleccione **Nuevo trabajo**.  
  
4.  En el cuadro de diálogo **Nuevo trabajo** , escriba un nombre de trabajo en **Nombre**.  
  
5.  En **Pasos**, haga clic en **Nuevo**.  
  
6.  En el cuadro de diálogo **Nuevo paso de trabajo** , escriba un nombre de paso en **Nombre del paso**.  
  
7.  En **Tipo**, seleccione **Comando de SQL Server Analysis Services**.  
  
8.  En **Ejecutar como**, seleccione la **Cuenta del servicio del Agente SQL Server**. Recuerde de la sección Requisitos previos que esta cuenta debe tener permisos de administrador en Analysis Services.  
  
9. En **Servidor**, especifique el nombre de servidor de la instancia de Analysis Services.  
  
10. En **Comando**, haga clic con el botón derecho y seleccione **Pegar**.  
  
11. Haga clic en **Aceptar**.  
  
12. En la página **Programaciones** , haga clic en **Nuevo**.  
  
13. En el cuadro de diálogo **Nueva programación del trabajo** , escriba un nombre de programación en **Nombre**y, a continuación, haga clic en **Aceptar**.  
  
     Este paso crea una programación para domingo a las 12:00. El paso siguiente muestra cómo ejecutar manualmente el trabajo. También puede seleccionar una programación que ejecutará el trabajo cuando lo esté supervisando.  
  
14. Haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
15. En el **Explorador de objetos**, expanda **Trabajos**, haga clic con el botón derecho en el trabajo que creó y seleccione **Iniciar trabajo en el paso**.  
  
     Dado que el trabajo tiene un solo paso, el trabajo se ejecuta inmediatamente. Si el trabajo contuviera varios pasos, podría seleccionar el paso en el que el trabajo debe iniciarse.  
  
16. Cuando finalice el trabajo, haga clic **Cerrar**.  
  
## <a name="see-also"></a>Vea también  
 [Configuración y opciones de procesamiento &#40;Analysis Services&#41;](../multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Secuencia de comandos de las tareas administrativas en Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
