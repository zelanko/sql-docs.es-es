---
title: Ver y trabajar con la salida del Asistente para la optimización de motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dta.reports.f1
- sql12.dta.sessionmonitor.f1
- sql12.dta.recommendations.f1
- sql12.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83b44addd88b83b424e9cd956dcc4bd7621ee118
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167106"
---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>Ver y trabajar con la salida del Asistente para la optimización de motor de base de datos
  Cuando el Asistente para la optimización de motor de base de datos optimiza bases de datos, crea resúmenes, recomendaciones, informes y registros de optimización. Puede utilizar la salida de registro de optimización para solucionar problemas de las sesiones de optimización del Asistente para la optimización de motor de base de datos. Puede usar los resúmenes, recomendaciones e informes para determinar si desea implementar las recomendaciones de optimización o continuar con la optimización hasta alcanzar las mejoras de rendimiento de consultas que necesita para la instalación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener información acerca de cómo usar el Asistente para la optimización de bases de datos para crear cargas de trabajo y optimizar una base de datos, vea [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md).  
  
##  <a name="View"></a> Ver la salida de optimización  
 Los procedimientos siguientes describen cómo ver las recomendaciones, resúmenes, informes y registros de optimización utilizando la GUI del Asistente para la optimización de motor de base de datos. Para obtener información sobre las opciones de la interfaz de usuario, vea [Descripciones de la interfaz de usuario](#UI) más adelante en este tema.  
  
 También puede usar la GUI para ver la salida de optimización generada por la utilidad de línea de comandos **dta** .  
  
> [!NOTE]  
>  Si usa la utilidad de línea de comandos **dta** y especifica que la salida se escriba en un archivo XML con el argumento **-ox** , puede abrir y ver el archivo de salida XML si hace clic en **Abrir archivo** en el menú **Archivo** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para más información, consulte [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md). Para obtener información sobre la utilidad de línea de comandos **dta** , vea [dta (utilidad)](../../tools/dta/dta-utility.md).  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para ver recomendaciones de optimización con la GUI del Asistente para la optimización de motor de base de datos  
  
1.  Optimice una base de datos con la GUI del Asistente para la optimización de motor de base de datos o mediante la utilidad de línea de comandos **dta** . Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si desea usar una sesión de optimización existente, omita este paso y vaya al paso 2.  
  
2.  Inicie la GUI del Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si quiere ver las recomendaciones de una sesión de optimización existente, ábrala; para ello, haga doble clic en el nombre de sesión en la ventana **Monitor de sesión**.  
  
     Una vez finalizada la nueva sesión de optimización o después de que la herramienta haya cargado la sesión existente, se muestra la página **Recomendaciones** .  
  
3.  En la página **Recomendaciones** , haga clic en **Recomendaciones de partición** y **Recomendaciones de índices** para ver los paneles de resultados de las sesiones de optimización. Si al establecer las opciones de optimización de esta sesión no especificó ninguna partición, el panel **Recomendaciones de partición** estará vacío.  
  
4.  En los paneles **Recomendaciones de partición** o **Recomendaciones de índices** , utilice las barras de desplazamiento para ver toda la información de la cuadrícula.  
  
5.  Desactive **Mostrar objetos existentes** en la parte inferior de la página con pestañas **Recomendaciones** . La cuadrícula muestra solo los objetos de la base de datos a los que se hace referencia en la recomendación. Use la barra de desplazamiento inferior para ver la columna más a la derecha de la cuadrícula de recomendaciones y haga clic en un elemento de la columna **Definición** para ver o copiar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] que crea ese objeto en la base de datos.  
  
6.  Si desea guardar en un archivo de scripts todos los scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] que crean o quitan objetos de base de datos de esta recomendación, haga clic en **Guardar recomendaciones** en el menú **Acciones** .  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>Para ver resúmenes e informes de optimización con la GUI del Asistente para la optimización de motor de base de datos  
  
1.  Optimice una base de datos con la GUI del Asistente para la optimización de motor de base de datos o mediante la utilidad de línea de comandos **dta** . Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si desea usar una sesión de optimización existente, omita este paso y vaya al paso 2.  
  
2.  Inicie la GUI del Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si quiere ver los resúmenes e informes de optimización de una sesión de optimización existente, ábrala; para ello, haga doble clic en el nombre de sesión en la ventana **Monitor de sesión**.  
  
3.  Una vez finalizada la nueva sesión de optimización o después de que la herramienta haya cargado la sesión existente, haga clic en la pestaña **Informes** .  
  
4.  El panel **Resumen de la optimización** contiene información acerca de la sesión de optimización. La información que proporcionan los elementos **Porcentaje de mejora esperada** y **Espacio usado por la recomendación** puede ser particularmente útil a la hora de decidir si va a implementar la recomendación.  
  
5.  En el panel **Informes de optimización** , haga clic en **Seleccionar informe** para elegir el informe de optimización que desea ver.  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>Para ver registros de optimización con la GUI del Asistente para la optimización de motor de base de datos  
  
1.  Optimice una base de datos con la GUI del Asistente para la optimización de motor de base de datos o mediante la utilidad de línea de comandos **dta** . Asegúrese de que ha activado **Guardar registro de optimización** en la pestaña **General** al optimizar la carga de trabajo. Si desea usar una sesión de optimización existente, omita este paso y vaya al paso 2.  
  
2.  Inicie la GUI del Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si quiere ver los resúmenes e informes de optimización de una sesión de optimización existente, ábrala; para ello, haga doble clic en el nombre de sesión en la ventana **Monitor de sesión** .  
  
3.  Una vez finalizada la nueva sesión de optimización o después de que la herramienta haya cargado la sesión existente, haga clic en la pestaña **Progreso** . El panel **Registro de optimización** muestra el contenido del registro. El registro contiene información acerca de los eventos de carga de trabajo que el Asistente para la optimización de motor de base de datos no puede analizar.  
  
     Si el Asistente para la optimización de motor de base de datos analiza todos los eventos en una sesión de optimización, aparecerá un mensaje que indica que el registro de optimización está vacío. Si no se activó **Guardar registro de optimización** en la pestaña **General** cuando se ejecutó la sesión de optimización, aparecerá un mensaje con esa información.  
  
##  <a name="Implement"></a> Implementar recomendaciones de optimización  
 Se pueden implementar las recomendaciones del Asistente para la optimización de motor de base de datos manual o automáticamente como parte de la sesión de optimización. Si desea examinar los resultados de optimización antes de implementarlos, utilice la GUI del Asistente para la optimización de motor de base de datos. A continuación, puede utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ejecutar manualmente los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] que el Asistente para la optimización de motor de base de datos genera como resultado del análisis de una carga de trabajo para implementar las recomendaciones. Si no necesita examinar los resultados antes de implementarlos, puede usar la opción **-a** con la utilidad de símbolo del sistema **dta** . Esto hace que la utilidad implemente automáticamente las recomendaciones de optimización después de analizar la carga de trabajo. En los siguientes procedimientos se explica cómo utilizar ambas interfaces del Asistente para la optimización de motor de base de datos con el fin de implementar las recomendaciones de optimización.  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para implementar las recomendaciones de optimización manualmente mediante la GUI del Asistente para la optimización de motor de base de datos  
  
1.  Optimice la base de datos mediante la GUI del Asistente para la optimización de motor de base de datos o la utilidad del símbolo del sistema **dta** . Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si desea usar una sesión de optimización existente, omita este paso y vaya al paso 2.  
  
2.  Inicie la GUI del Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si quiere implementar las recomendaciones de optimización para una sesión de optimización existente, ábrala haciendo doble clic en el nombre de la sesión en **Monitor de sesión**.  
  
3.  Una vez finalizada la nueva sesión de optimización, o bien después de que la herramienta haya cargado la sesión existente, haga clic en la opción **Aplicar recomendaciones** del menú **Acciones** .  
  
4.  En el cuadro de diálogo **Aplicar recomendaciones** , elija **Aplicar ahora** o **Programar para más tarde**. Si elige **Programar para más tarde**, seleccione la fecha y la hora.  
  
5.  Haga clic en **Aceptar** para aplicar las recomendaciones.  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>Para implementar automáticamente las recomendaciones de optimización mediante la utilidad del símbolo del sistema dta  
  
1.  Determine las características de la base de datos (índices, vistas indizadas, creación de particiones) que desee que el Asistente para la optimización de motor de base de datos pueda agregar, quitar o retener durante el análisis.  
  
     Tenga en cuenta las siguientes consideraciones antes de empezar la optimización:  
  
    -   Cuando use una tabla de seguimiento como una carga de trabajo, esa tabla debe existir en el mismo servidor en el que el Asistente para la optimización de motor de base de datos está realizando la optimización. Si crea la tabla de seguimiento en otro servidor, trasládela al servidor en el que el Asistente para la optimización de motor de base de datos realiza la optimización.  
  
    -   Si la ejecución de una sesión de optimización dura más de lo previsto, puede detenerla mediante CTRL+C. En estas circunstancias, CTRL+C obliga a **dta** a crear la mejor recomendación posible en función de la cantidad de la carga de trabajo consumida, y no pierde el tiempo que la herramienta ya ha usado para optimizar la carga de trabajo.  
  
2.  En el símbolo del sistema, escriba lo siguiente:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     donde **-E** especifica que la sesión de optimización usa una conexión de confianza (en lugar de un identificador de inicio de sesión y una contraseña), **-D** especifica el nombre de la base de datos que se quiere optimizar o una lista delimitada por comas de varias bases de datos usadas por la carga de trabajo, **-if** especifica el nombre y la ruta de acceso de un archivo de carga de trabajo, **-s** especifica un nombre para la sesión de optimización y **-a** especifica que quiere que la utilidad del símbolo del sistema **dta** aplique automáticamente las recomendaciones de optimización una vez analizada la carga de trabajo sin solicitarlo al usuario. Para más información acerca de cómo usar la utilidad de símbolo del sistema **dta** para optimizar bases de datos, consulte [Start and Use the Database Engine Tuning Advisor](database-engine-tuning-advisor.md).  
  
3.  Presione ENTRAR.  
  
##  <a name="Analysis"></a> Realizar análisis de exploración  
 La característica de configuración especificada por el usuario del Asistente para la optimización de motor de base de datos permite a los administradores de bases de datos realizar análisis de exploración. Mediante esta característica, los administradores de bases de datos especifican el diseño físico de la base de datos que deseen para el Asistente para la optimización de motor de base de datos y, así, pueden evaluar los efectos de ese diseño en el rendimiento sin necesidad de implementarlo. Tanto la utilidad de línea de comandos como la interfaz gráfica de usuario (GUI) del Asistente para la optimización de motor de base de datos admiten la característica de configuración especificada por el usuario. No obstante, la utilidad de línea de comandos ofrece la mayor flexibilidad.  
  
 Si utiliza la GUI del Asistente para la optimización de motor de base de datos, podrá evaluar los efectos de la implementación de un subconjunto de recomendaciones de optimización del Asistente para la optimización de motor de base de datos, pero no podrá agregar estructuras de diseño físico hipotéticas para que el Asistente para la optimización de motor de base de datos las evalúe.  
  
 En los procedimientos siguientes se explica cómo utilizar esta característica con ambas interfaces.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>Usar la GUI del Asistente para la optimización de motor de base de datos para evaluar recomendaciones de optimización  
 En el procedimiento siguiente se describe cómo evaluar una recomendación generada por el Asistente para la optimización de motor de base de datos; sin embargo, la GUI no le permite especificar nuevas estructuras de diseño físico para la evaluación.  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Para evaluar recomendaciones de optimización con la GUI del Asistente para la optimización de motor de base de datos  
  
1.  Use la GUI del Asistente para la optimización de motor de base de datos para optimizar una base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md). Si quiere evaluar una sesión de optimización ya existente, haga doble clic en **Monitor de sesión**.  
  
2.  En la pestaña **Recomendaciones** , borre las estructuras de diseño físico recomendadas que no va a utilizar.  
  
3.  En el menú **Acciones** , haga clic en **Evaluar recomendaciones**. Se creará una sesión de optimización.  
  
4.  Escriba el **Nombre de sesión**. Para ver la configuración de la estructura de diseño físico de la base de datos que está evaluando, elija **Haga clic aquí para ver la sección de configuración** , en el área **Descripción** , situada en la parte inferior de la ventana de aplicación del Asistente para la optimización de motor de base de datos.  
  
5.  Haga clic en el botón **Iniciar análisis** de la barra de herramientas. Una vez que el Asistente para la optimización de motor de base de datos haya acabado, podrá ver los resultados en la pestaña **Recomendaciones** .  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>Usar la GUI del Asistente para la optimización de motor de base de datos para exportar los resultados de una sesión de optimización para el análisis de optimización de escenarios condicionales  
 En el procedimiento siguiente se explica cómo exportar los resultados de una sesión de optimización del Asistente para la optimización de motor de base de datos a un archivo XML, que podrá editar y, luego, optimizar con la utilidad de línea de comandos **dta** . Esto le permite realizar análisis de optimización en estructuras hipotéticas de diseño físico sin necesidad de implementarlas en la base de datos antes de averiguar si se producen las mejoras en el rendimiento que desea. El uso de la GUI del Asistente para la optimización de motor de base de datos para optimizar inicialmente la base de datos y exportar luego los resultados de la optimización a un archivo **.xml** es un buen método para los usuarios que no conocen bien XML, ya que se aprovecha la flexibilidad del esquema XML del Asistente para la optimización de motor de base de datos para realizar un análisis de escenarios condicionales.  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>Para exportar resultados de una sesión de optimización desde la GUI del Asistente para la optimización de motor de base de datos para el análisis "y si" con la utilidad de línea de comandos dta  
  
1.  Use la GUI del Asistente para la optimización de motor de base de datos para optimizar una base de datos. Para más información, consulte [Start and Use the Database Engine Tuning Advisor](database-engine-tuning-advisor.md). Si quiere evaluar una sesión de optimización ya existente, haga doble clic en **Monitor de sesión**.  
  
2.  En el menú **Archivo** , haga clic en **Exportar resultados de sesión** y guarde la exportación como archivo XML.  
  
3.  Abra el archivo XML creado en el paso 2 en un editor XML, un editor de texto o en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Desplácese hacia abajo hasta la `Configuration` elemento. Copie y pegue el `Configuration` después de la plantilla del archivo de entrada de sección del elemento en un archivo XML la `TuningOptions` elemento. Guarde este archivo de entrada XML.  
  
4.  En el archivo de entrada XML nuevo que creó en el paso 3, especifique todas las opciones de optimización que desee en el elemento `TuningOptions`, modifique la sección del elemento `Configuration` (agregue o elimine las estructuras de diseño físico según sea necesario para su análisis), guarde el archivo y valídelo según el esquema XML del Asistente para la optimización de motor de base de datos. Para obtener información sobre cómo modificar este archivo XML, vea [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
5.  Use el archivo XML creado en el paso 4 como entrada para la utilidad de línea de comandos **dta** . Para obtener información sobre cómo utilizar los archivos de entrada XML con esta herramienta, vea la sección "Optimizar una base de datos mediante la utilidad dta" en [Start and Use the Database Engine Tuning Advisor](database-engine-tuning-advisor.md).  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Usar la característica de configuración especificada por el usuario con la utilidad de línea de comandos dta  
 Si es usted un programador de XML experimentado, puede crear un archivo de entrada XML del Asistente para la optimización de motor de base de datos en el que podrá especificar una carga de trabajo y una configuración hipotética de las estructuras de diseño físico de la base de datos, como índices, vistas indizadas o particiones. Luego, podrá usar la utilidad de línea de comandos **dta** para analizar los efectos de esta configuración hipotética en el rendimiento de las consultas en la base de datos. En el siguiente procedimiento se explica este proceso paso a paso:  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Para usar la característica de configuración especificada por el usuario con la utilidad de línea de comandos dta  
  
1.  Cree una carga de trabajo de optimización. Para obtener información sobre esta tarea, vea [Start and Use the Database Engine Tuning Advisor](database-engine-tuning-advisor.md).  
  
2.  Copie y pegue el [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md) en el editor XML o en un editor de texto. Use este ejemplo para crear un archivo de entrada XML para su sesión de optimización. Para obtener información sobre la realización de esta tarea, vea la sección "Crear archivos de entrada XML" en [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md).  
  
3.  Editar el `TuningOptions` y `Configuration` elementos en el archivo de entrada de XML de ejemplo. En el `TuningOptions` elemento, especifique las estructuras de diseño físico que desea Database Engine Tuning Advisor a tener en cuenta durante la sesión de optimización. En el elemento `Configuration`, especifique las estructuras de diseño físico que coincidan con la configuración hipotética de las estructuras de diseño físico de la base de datos que desea que analice el Asistente para la optimización de motor de base de datos. Para obtener información sobre los atributos y elementos secundarios puede usar con el `TuningOptions` y `Configuration` elementos primarios, consulte [referencia del archivo de entrada XML &#40;Database Engine Tuning Advisor&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
4.  Guarde el archivo de entrada con la extensión **.xml** .  
  
5.  Valide el archivo de entrada XML que guardó en el paso 4 con el esquema XML del Asistente para la optimización de motor de base de datos. Este esquema se instala en la siguiente ubicación al instalar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     El esquema XML del Asistente para la optimización de motor de base de datos también se encuentra disponible en línea en [http://schemas.microsoft.com/sqlserver/2004/07/dta](http://schemas.microsoft.com/sqlserver/2004/07/dta).  
  
6.  Tras crear una carga de trabajo y un archivo de entrada XML, está preparado para enviar el archivo de entrada a la utilidad de línea de comandos **dta** para el análisis. Asegúrese de especificar un nombre de archivo de salida XML para el argumento de la utilidad **-ox** . Esto crea un archivo de salida XML con una configuración recomendada especificada en el `Configuration` elemento. Si desea ejecutar Database Engine Tuning Advisor nuevo para comprobar otra configuración hipotética basada en la salida, puede copiar y pegar el `Configuration` contenido del elemento desde el archivo de salida en un nuevo o el archivo de entrada XML original. Para obtener información acerca del uso del archivo de entrada XML con la utilidad **dta** , vea la sección "Optimizar una base de datos mediante la utilidad dta" en [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md).  
  
     Una vez finalizada la optimización, puede utilizar la GUI del Asistente para la optimización de motor de base de datos para ver los informes de la optimización, o bien puede abrir el archivo de salida XML para ver los elementos `TuningSummary` y `Configuration` y comprobar las recomendaciones del Asistente para la optimización de motor de base de datos. Para obtener información acerca de cómo ver los resultados de la sesión de optimización, revise [Ver la salida de optimización](#View) anteriormente en este tema. Tenga en cuenta también que el archivo de salida XML puede contener informes de análisis del Asistente para la optimización de motor de base de datos.  
  
7.  Repita los pasos 6 y 7 hasta que cree la configuración hipotética que produce las mejoras que necesita en el rendimiento de las consultas. A continuación, podrá implementar la nueva configuración. Para obtener más información, vea [Implementar recomendaciones de optimización](#Implement) anteriormente en este tema.  
  
##  <a name="ReviewEvaluateClone"></a> Revisar, evaluar y clonar sesiones de optimización  
 El Asistente para la optimización de motor de base de datos crea una nueva sesión de optimización cada vez que se empiezan a analizar los efectos de una carga de trabajo de una o varias bases de datos. Puede utilizar el **Monitor de sesión** de la GUI del Asistente para la optimización de motor de base de datos para ver o volver a cargar todas las sesiones de optimización que se han ejecutado en una instancia determinada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando todas las sesiones de optimización existentes están disponibles para revisión, resulta fácil: clonar sesiones basándose en las existentes, modificar recomendaciones de optimización existentes y, luego, utilizar el Asistente para la optimización de motor de base de datos para evaluar la sesión modificada, o bien realizar optimizaciones en intervalos regulares para supervisar el diseño físico de las bases de datos. Por ejemplo, se puede optimizar una base de datos mensualmente.  
  
 Para poder revisar las sesiones de optimización de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se deben crear sesiones de optimización en la instancia de servidor optimizando las cargas de trabajo mediante el Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md).  
  
### <a name="review-existing-tuning-sessions"></a>Revisar las sesiones de optimización existentes  
 Siga los pasos que se indican a continuación para explorar las sesiones de optimización existentes de una instancia determinada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##### <a name="to-review-existing-tuning-sessions"></a>Para revisar las sesiones de optimización existentes  
  
1.  Inicie la GUI del Asistente para la optimización de motor de base de datos. Para más información, consulte [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md).  
  
2.  Todas las sesiones de optimización existentes aparecerán en la mitad superior de la ventana **Monitor de sesión** . El número de sesiones que aparecen depende de las veces que se han optimizado bases de datos en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilice las barras de desplazamiento para ver todas las sesiones de optimización.  
  
3.  Haga clic una vez en el nombre de una sesión de optimización para ver sus detalles en la mitad inferior de la ventana **Monitor de sesión** .  
  
4.  Si hace doble clic en el nombre de una sesión de optimización, se cargará su información en el Asistente para la optimización de motor de base de datos. Una vez cargada la información de la sesión, podrá elegir cualquiera de las pestañas para ver información sobre la sesión en cuestión.  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>Evaluar las sesiones de optimización existentes como configuraciones hipotéticas  
 Siga los pasos que se indican a continuación para evaluar una sesión de optimización existente. La evaluación de una sesión de optimización implica la visualización y modificación de sus recomendaciones, seguidas de una nueva optimización. Por ejemplo, si decide que solo desea crear índices en **table1**, eliminará la creación de vistas indizadas y la creación de particiones de una recomendación de optimización existente. A continuación, el Asistente para la optimización de motor de base de datos creará una nueva sesión de optimización y optimizará la carga de trabajo de las bases de datos mediante las recomendaciones modificadas como configuración hipotética. Esto significa que el Asistente para la optimización de motor de base de datos optimiza la carga de trabajo de las bases de datos como si se hubieran implementado las recomendaciones, lo que permite realizar análisis de escenarios condicionales limitados. Estos análisis son limitados porque solo se puede elegir un subconjunto de una recomendación existente cuando se utiliza la GUI del Asistente para la optimización de motor de base de datos. Para realizar análisis de escenarios condicionales completos, especificando una configuración hipotética totalmente nueva que no sea un subconjunto de una sesión de optimización anterior, deberá usar el archivo de entrada XML del Asistente para la optimización de motor de base de datos con la utilidad de la línea de comandos **dta** .  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>Para evaluar una sesión de optimización existente  
  
1.  Tras iniciar el Asistente para la optimización de motor de base de datos, haga doble clic en una sesión de optimización en la mitad superior del **Monitor de sesión**, que cargará la información de sesión en el Asistente para la optimización de motor de base de datos.  
  
2.  Haga clic en la pestaña **Progreso** para comprobar el registro de optimización, que incluye información de errores sobre todos los eventos de la carga de trabajo que el Asistente para la optimización de motor de base de datos no pudo optimizar. Esta información le ayudará a evaluar la eficacia de la carga de trabajo.  
  
3.  Si desea realizar una revisión más detallada de los resultados de optimización de esta sesión, haga clic en la pestaña **Informes** . Podrá ver el resumen de optimización o elegir un informe de optimización en la lista **Seleccionar informe** .  
  
4.  Haga clic en la pestaña **Recomendaciones** para ver las recomendaciones de optimización.  
  
5.  Si hay alguna recomendación de la que no está seguro que desea implementar, deselecciónela.  
  
6.  En el menú **Acciones** , haga clic en **Evaluar recomendaciones**. El Asistente para la optimización de motor de base de datos creará una nueva sesión de optimización que utilizará la recomendación modificada como configuración hipotética. Para ver la configuración hipotética en XML, elija **Haga clic aquí para ver la sección de configuración**.  
  
7.  En la pestaña **General** , escriba un **Nombre de sesión**y compruebe que se ha especificado la **Carga de trabajo** correcta.  
  
8.  En la pestaña **Opciones de optimización** , puede especificar una hora para la optimización o cualquiera de las **Opciones avanzadas**.  
  
9. Haga clic en el botón **Iniciar análisis** de la barra de herramientas. El Asistente para la optimización de motor de base de datos iniciará la optimización de las bases de datos mediante la configuración hipotética. Cuando el Asistente acabe, verá los resultados de esta sesión del mismo modo que para cualquier otra.  
  
### <a name="clone-existing-tuning-sessions"></a>Clonar las sesiones de optimización existentes  
 Para crear nuevas sesiones de optimización basadas en sesiones existentes, elija la opción de clonación en el Asistente para la optimización de motor de base de datos. Cuando utilice la opción de clonación, basará una sesión de optimización nueva en una existente. A continuación, podrá cambiar las opciones de optimización de la nueva sesión según precise. Cuando evalúe una sesión existente tal como se describe en el procedimiento anterior, el Asistente para la optimización de motor de base de datos también creará una nueva sesión de optimización, pero no podrá cambiar las opciones de optimización.  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>Para crear nuevas sesiones de optimización mediante la clonación de sesiones existentes  
  
1.  Tras iniciar el Asistente para la optimización de motor de base de datos, haga doble clic en una sesión de optimización en la mitad superior del **Monitor de sesión**, que cargará la información de sesión en el Asistente para la optimización de motor de base de datos.  
  
2.  En el menú **Acciones** , haga clic en **Clonar sesión**.  
  
3.  En la pestaña **General** , escriba un **Nombre de sesión**y compruebe que se ha especificado la **Carga de trabajo** correcta.  
  
4.  En la pestaña **Opciones de optimización** , podrá especificar una hora para la optimización, las estructuras de diseño físico cuya creación debe considerar el Asistente para la optimización de motor de base de datos y lo que debe considerar quitar de su recomendación.  
  
5.  Haga clic en **Opciones avanzadas** si desea establecer un límite de espacio para las recomendaciones, un número máximo de columnas por índice y si desea que el Asistente para la optimización de motor de base de datos genere recomendaciones que se puedan implementar mientras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en línea.  
  
6.  Haga clic en el botón **Iniciar análisis** de la barra de herramientas para analizar los efectos de la carga de trabajo igual que cualquier otra sesión de optimización. Cuando el Asistente acabe, verá los resultados de esta sesión del mismo modo que para cualquier otra.  
  
##  <a name="UI"></a> Descripciones de la interfaz de usuario  
  
### <a name="sessions-monitor"></a>Monitor de sesiones  
 El**Monitor de sesión** muestra información sobre las sesiones abiertas en el Asistente para la optimización de motor de base de datos. Para que se muestre información sobre la sesión en la ventana de propiedades, seleccione un nombre de sesión en el **Monitor de sesión**.  
  
### <a name="recommendations-tab"></a>Pestaña Recomendaciones  
 La pestaña **Recomendaciones** aparece después de que el Asistente para la optimización de motor de base de datos haya finalizado el análisis de una carga de trabajo. Esta cuadrícula contiene las recomendaciones de cada uno de los objetos tomados en consideración. Las recomendaciones sobre particiones, si las hay, se presentan en la cuadrícula superior, y las recomendaciones sobre índices se presentan en la cuadrícula inferior. En caso de que no haya ninguna recomendación, no aparecerá ninguna cuadrícula.  
  
 La columna **Definición** contiene la definición de la partición recomendada o del índice recomendado como un hipervínculo. Esta columna suele ser demasiado estrecha como para que pueda verse toda la definición. Haga clic en el hipervínculo para que se muestre el cuadro de diálogo que contiene la definición completa y el botón **Copiar al Portapapeles** .  
  
#### <a name="partition-recommendations"></a>Recomendaciones de partición  
 **Nombre de la base de datos**  
 Base de datos que contiene los objetos que se recomienda modificar.  
  
 **Recomendación**  
 Acción recomendada para mejorar el rendimiento. Los valores posibles son Crear y Eliminar.  
  
 **Destino de la recomendación**  
 Función o esquema de partición que se ven afectados por la recomendación. El icono de esta columna refleja la recomendación que debe quitarse o agregarse en el **Destino de la recomendación** y si se trata de una función o de un esquema de partición.  
  
 **Detalles**  
 Descripción del **Destino de la recomendación**. Entre los posibles valores, se incluye un intervalo para las funciones de partición, o un valor en blanco para los esquemas de partición.  
  
 **Número de particiones**  
 Número de particiones definidas por las funciones de partición recomendadas. Cuando esta función se utiliza con un esquema y se aplica después a una tabla, los datos de la tabla se dividen en dicho número de particiones.  
  
 **Definición**  
 Definición del **Destino de la recomendación**. Haga clic en la columna para abrir el cuadro de diálogo Vista previa de script SQL, que contiene un script para la acción recomendada.  
  
##### <a name="index-recommendations"></a>Recomendaciones de índices  
 **Database Name**  
 Base de datos que contiene los objetos que se recomienda modificar.  
  
 **Nombre de objeto**  
 Tabla relacionada con la recomendación.  
  
 **Recomendación**  
 Acción recomendada para mejorar el rendimiento. Los valores posibles son Crear y Eliminar.  
  
 **Destino de la recomendación**  
 Índice o vista que se ven afectados por la recomendación. El icono de esta columna refleja las recomendaciones que deben quitarse o agregarse en el **Destino de la recomendación**.  
  
 **Detalles**  
 Descripción del **Destino de la recomendación**. Entre los posibles valores, se encuentran agrupado, vista indizada o en blanco, que indica un índice no clúster. También indica si el índice es único.  
  
 **Esquema de partición**  
 El esquema de partición se proporcionará en esta columna si es recomendable realizar particiones.  
  
 **Tamaño (KB)**  
 El tamaño esperado del nuevo objeto recomendado. Si esta columna está en blanco, haga clic en **Consulte los informes para ver los tamaños de los objetos existentes**.  
  
 **Definición**  
 Definición del **Destino de la recomendación**. Haga clic en la columna para abrir el cuadro de diálogo Vista previa de script SQL, que contiene un script para la acción recomendada.  
  
 **Mostrar objetos existentes**  
 Seleccione esta opción para que todos los objetos existentes se muestren en la cuadrícula, aunque el Asistente para la optimización de motor de base de datos no haya hecho ninguna recomendación relacionada con los objetos.  
  
 **Consulte los informes para ver los tamaños de los objetos existentes**  
 Seleccione esta opción para ver informes que proporcionan el tamaño de objetos existentes en la cuadrícula de recomendaciones.  
  
### <a name="actions-menuapply-recommendations-options"></a>Opciones del menú Acciones y de Aplicar recomendaciones  
 Después de que se haya analizado una carga de trabajo y de que se hayan presentado las recomendaciones, en el menú **Acciones** , haga clic en **Aplicar recomendaciones** para abrir el cuadro de diálogo **Aplicar recomendaciones** .  
  
 **Aplicar ahora**  
 Genera un script para las recomendaciones y ejecuta el script para implementar las recomendaciones.  
  
 **Programar para más tarde**  
 Genera un script para las recomendaciones y guarda las acciones como trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Date**  
 Especifica la fecha en la que desea ejecutar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aplicar las recomendaciones.  
  
 **Time**  
 Especifica la hora en la que desea ejecutar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aplicar las recomendaciones.  
  
### <a name="reports-tab-options"></a>Opciones de la pestaña Informes  
 La pestaña **Informes** aparece después de que el Asistente para la optimización de motor de base de datos haya finalizado el análisis de una carga de trabajo.  
  
 **Resumen de la optimización**  
 Muestra un resumen de las recomendaciones del Asistente para la optimización de motor de base de datos.  
  
 **Date**  
 Fecha en que el Asistente para la optimización de motor de base de datos creó el informe.  
  
 **Time**  
 Hora a la que el Asistente para la optimización de motor de base de datos creó el informe.  
  
 **Server**  
 Servidor que era el destino de la carga de trabajo del Asistente para la optimización de motor de base de datos.  
  
 **Bases de datos para optimizar**  
 Bases de datos afectadas por las recomendaciones del Asistente para la optimización de motor de base de datos.  
  
 **Archivo de carga de trabajo**  
 Aparece cuando la carga de trabajo es un archivo.  
  
 **Tabla de carga de trabajo**  
 Aparece cuando la carga de trabajo es una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Carga de trabajo**  
 Aparece cuando la carga de trabajo se ha importado desde el Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Tiempo máximo de optimización**  
 Tiempo máximo configurado que va estar disponible para el análisis del Asistente para la optimización de motor de base de datos.  
  
 **Tiempo dedicado a la optimización**  
 Tiempo realmente utilizado por el Asistente para la optimización de motor de base de datos para analizar la carga de trabajo.  
  
 **Porcentaje de mejora esperada**  
 Porcentaje de mejora esperada con la carga de trabajo de destino si se han implementado todas las recomendaciones del Asistente para la optimización de motor de base de datos.  
  
 **Espacio máximo para la recomendación (MB)**  
 Espacio máximo considerado para las recomendaciones. Este valor se configura antes de que se realice el análisis, mediante el botón **Opciones avanzadas** , en la pestaña **Opciones de optimización** .  
  
 **Espacio en uso (MB)**  
 Espacio actualmente utilizado por los índices de la base de datos analizada.  
  
 **Espacio usado por la recomendación (MB)**  
 Espacio aproximado que se espera que utilicen los índices si se han implementado todas las recomendaciones del Asistente para la optimización de motor de base de datos.  
  
 **Número de eventos de la carga de trabajo**  
 Número de eventos incluidos en la carga de trabajo.  
  
 **Número de eventos optimizados**  
 Número de eventos de la carga de trabajo que se han optimizado. Si un evento no puede optimizarse, se incluye en el registro de optimización, que está disponible en la pestaña **Progreso** .  
  
 **Número de instrucciones optimizadas**  
 Número de instrucciones de la carga de trabajo que se han optimizado. Si una instrucción no puede optimizarse, se incluye en el registro de optimización, que está disponible en la pestaña **Progreso** .  
  
 **Porcentaje de instrucciones SELECT en el conjunto optimizado**  
 Porcentaje de instrucciones optimizadas que son instrucciones SELECT. Solo aparece si se han optimizado instrucciones SELECT.  
  
 **Porcentaje de instrucciones UPDATE en el conjunto optimizado**  
 Porcentaje de instrucciones optimizadas que son instrucciones UPDATE. Solo aparece si se han optimizado instrucciones UPDATE.  
  
 **Número de índices que se recomienda [crear | quitar]**  
 Número recomendado de índices que deben crearse o quitarse en la base de datos optimizada. Solo aparece si los índices forman parte de la recomendación.  
  
 **Número de índices de vistas que se recomienda [crear | quitar]**  
 Número recomendado de índices de vistas que deben crearse o quitarse en la base de datos optimizada. Solo aparece si los índices de vistas forman parte de la recomendación.  
  
 **Número de estadísticas que se recomienda crear**  
 Número recomendado de estadísticas que deben crearse o quitarse en la base de datos optimizada. Solo aparece si se han recomendado las estadísticas.  
  
 **Select Report**  
 Muestra los detalles del informe seleccionado. Las columnas de la cuadrícula varían con cada informe.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md)   
 [dta (utilidad)](../../tools/dta/dta-utility.md)  
  
  
