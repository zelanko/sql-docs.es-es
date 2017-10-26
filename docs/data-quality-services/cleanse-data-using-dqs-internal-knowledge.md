---
title: Limpiar datos mediante el conocimiento de DQS (interno) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.dqproject.interactivecleansing.f1
- sql13.dqs.dqproject.map.f1
- sql13.dqs.dqproject.correction.f1
- sql13.dqs.dqproject.export.f1
ms.assetid: c96b13ad-02a6-4646-bcc7-b4a8d490f5cc
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8aa5b0fdf2771d83310e503f2fdd8770bf9cf324
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cleanse-data-using-dqs-internal-knowledge"></a>Limpiar datos mediante el conocimiento de DQS (interno)
  En este tema se describe cómo limpiar los datos mediante un proyecto de calidad de datos de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). La limpieza de datos se realiza en los datos de origen utilizando una base de conocimiento generada en DQS a partir de un conjunto de datos de alta calidad. Para obtener más información, consulte [Crear una base de conocimiento](../data-quality-services/building-a-knowledge-base.md).  
  
 La limpieza de datos se realiza en cuatro fases: una fase de *asignación* en la que se identifica el origen de datos que se va a limpiar y se asigna a los dominios requeridos de una base de conocimiento, una fase de *limpieza asistida por PC* en la que DQS aplica la base de conocimiento a los datos que se van a limpiar y propone o realiza cambios en los datos de origen, una fase de *limpieza interactiva* en la que los administradores de datos pueden analizar los cambios en los datos, así como aceptarlos o rechazarlos, y, por último, la fase de *exportación* que le permite exportar los datos limpios. Cada uno de estos procesos se realiza en una página distinta del asistente para la actividad de limpieza, lo que le permite desplazarse de una página a otra, volver a ejecutar el proceso, y cerrar un proceso de limpieza específico y volver a la misma fase del proceso. DQS proporciona estadísticas sobre los datos de origen y los resultados de limpieza que permiten tomar decisiones fundadas sobre la limpieza de datos.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Es necesario especificar valores de umbral apropiados para la actividad de limpieza. Para obtener más información acerca de cómo hacerlo, vea [Configurar los valores de umbral para la limpieza y coincidencia](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Debe estar disponible una base de conocimiento de DQS en [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con la que comparar y limpiar los datos de origen. Además, la base de conocimiento debe contener conocimiento sobre el tipo de datos que desea limpiar. Por ejemplo, si desea limpiar datos de origen que contienen direcciones de EE. UU., debe tener una base de conocimiento creada a partir de datos de ejemplo de “alta calidad” para las direcciones de EE. UU.  
  
-   Si los datos de origen implicados en el proceso de limpieza están en un archivo de Excel, es necesario tener instalado Microsoft Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . De lo contrario, no podrá seleccionar dicho archivo en la fase de asignación. Los archivos creados por Microsoft Excel pueden tener la extensión .xlsx, .xls o .csv. Si se utiliza la versión de 64 bits de Excel, solo se admitirán los archivos de Excel 2003 (.xls); los archivos de Excel 2007 o 2010 (.xlsx) no son compatibles. Si utiliza la versión de 64 bits de Excel 2007 o 2010, guarde el archivo como un archivo .xls o .csv, o instale una versión de 32 bits de Excel en su lugar.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para realizar la limpieza de datos.  
  
##  <a name="Create"></a> Crear un proyecto de calidad de datos de limpieza.  
 Debe utilizar un proyecto de calidad de datos para realizar la operación de limpieza de datos. Para crear un proyecto de calidad de datos de limpieza:  
  
1.  Siga los pasos 1 a 3 del tema [Crear un proyecto de calidad de datos](../data-quality-services/create-a-data-quality-project.md).  
  
2.  En el paso 3.d, seleccione la actividad **Limpieza** .  
  
3.  Haga clic en **Crear** para crear un proyecto de calidad de datos de limpieza.  
  
 De esta forma, se creará un proyecto de calidad de datos de limpieza y se abrirá la página **Asignación** del asistente para la limpieza de calidad de datos.  
  
##  <a name="Mapping"></a> Fase de asignación  
 En la fase de asignación, especifique la conexión con los datos de origen que se deben limpiar y asigne las columnas de dichos datos a los dominios adecuados de la base de conocimiento seleccionada.  
  
1.  En la página **Asignación** del asistente para la limpieza de calidad de datos seleccione los datos de origen que se van a limpiar: **SQL Server** o **Archivo de Excel**:  
  
    1.  **SQL Server**: seleccione **DQS_STAGING_DATA** como la base de datos de origen si ha copiado los datos de origen en ella y, a continuación, seleccione la tabla o vista apropiada que contenga dichos datos. En caso contrario, seleccione la base de datos de origen y la tabla o vista apropiada. La base de datos de origen debe encontrarse en la misma instancia de SQL Server que [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] para que aparezca en la lista desplegable **Base de datos** .  
  
    2.  **Archivo de Excel**: haga clic en **Examinar**y seleccione el archivo de Excel que contiene los datos que se deben limpiar. Es necesario tener instalado Microsoft Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para seleccionar un archivo de Excel. De lo contrario, el botón **Examinar** no estará disponible y se le notificará debajo de este cuadro de texto que Microsoft Excel no está instalado. Asimismo, mantenga activada la casilla **Usar la primera fila como encabezado** si la primera fila del archivo de Excel contiene datos de encabezado.  
  
2.  En **Asignaciones**, asigne las columnas de datos de los datos de origen a los dominios apropiados de la base de conocimiento; para ello, seleccione una columna de origen en la lista desplegable de la columna **Columna de origen** y, a continuación, seleccione un dominio en la lista desplegable de la columna **Dominio** de la misma fila. Repita este paso para asignar todas las columnas de los datos de origen a los dominios apropiados de la base de conocimiento. Si fuera necesario, puede hacer clic en el icono **Agregar una asignación de columna** para agregar filas a la tabla de asignaciones.  
  
    > [!NOTE]  
    >  Solo puede asignar los datos de origen para un dominio DQS a fin de realizar la limpieza de datos únicamente si el tipo de datos de origen se admiten en DQS y coincide con el tipo de datos de dominio DQS. Para obtener información acerca de los tipos de datos de origen admitidos, vea [Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
3.  Haga clic en el icono **Vista previa del origen de datos** para ver los datos de la tabla o vista de SQL Server que ha seleccionado, o para ver la hoja de cálculo de Excel que ha seleccionado.  
  
4.  Haga clic en **Ver o seleccionar dominios compuestos** para ver una lista de los dominios compuestos asignados a una columna de origen. Este botón solo estará disponible si se ha asignado al menos un dominio compuesto a una columna de origen.  
  
5.  Haga clic en **Siguiente** para continuar con la fase de limpieza asistida por PC (página**Limpieza** ).  
  
##  <a name="ComputerAssisted"></a> Fase de limpieza asistida por PC  
 En la fase de limpieza asistida por PC, se ejecuta un proceso de limpieza de datos automatizado que analiza los datos de origen comparándolos con los dominios asignados de la base de conocimiento, y que realiza y propone cambios en los datos.  
  
1.  En la página **Limpieza** del asistente para la calidad de datos, haga clic en **Iniciar** para ejecutar el proceso de limpieza asistida por PC. DQS utiliza algoritmos avanzados y niveles de confianza basados en los niveles de umbral especificados para analizar los datos comparándolos con la base de conocimiento seleccionada; a continuación, los limpia. Para obtener información detallada sobre cómo se realiza la limpieza asistida por PC en DQS, vea [Limpieza asistida por PC](../data-quality-services/data-cleansing.md#ComputerAssisted) en [Limpieza de datos](../data-quality-services/data-cleansing.md).  
  
    > [!IMPORTANT]  
    >  -   Una vez que se haya completado el análisis de los datos, el botón **Iniciar** se convertirá en el botón **Reiniciar** . Si los resultados del análisis anterior aún no se han guardado y hace clic en **Reiniciar** , los perderá. Mientras se ejecuta el análisis, no abandone la página o el proceso de análisis se terminará.  
    > -   Si la base de conocimiento utilizada para el proyecto de limpieza se actualizó y publicó con posterioridad a la creación del proyecto de limpieza y hace clic en **Iniciar** , se le preguntará si desea utilizar la última base de conocimiento para la limpieza. Generalmente, esto ocurre cuando se crea un proyecto de calidad de datos mediante una base de conocimiento, se cierra sin haberlo finalizado haciendo clic en **Cerrar**y se vuelve a abrir posteriormente para realizar la limpieza. Mientras tanto, la base de conocimiento utilizada en el proyecto de limpieza se actualizó y se publicó.  
    >   
    >      Del mismo modo, si la base de conocimiento utilizada para el proyecto de limpieza se actualizó y publicó con posterioridad a la última ejecución de la limpieza asistida por PC y hace clic en **Reiniciar** , se le preguntará si desea utilizar la última base de conocimiento para la limpieza.  
    >   
    >      En ambos casos, haga clic en **Sí** para utilizar la base de conocimiento actualizada para la limpieza asistida por PC. Además, si existen conflictos entre las asignaciones actuales y la base de conocimiento actualizada (como dominios eliminados o cambios en el tipo de datos del dominio), el mensaje también le pedirá que corrija las asignaciones actuales para que utilicen la base de conocimiento actualizada. Haga clic en **Sí** para ir a la página **Asignación** , donde podrá corregir las asignaciones antes de continuar con la limpieza asistida por PC.  
  
2.  Durante la fase de limpieza asistida por PC, active el generador de perfiles haciendo clic en la pestaña **Generador de perfiles** para ver la generación de perfiles y las notificaciones en tiempo real. Para obtener más información, consulte [Estadísticas del generador de perfiles](#Profiler).  
  
3.  Si no está satisfecho con los resultados, haga clic en **Atrás** para volver a la página **Asignación** , modifique las asignaciones que considere oportunas, vuelva a la página **Limpieza** y, a continuación, haga clic en **Reiniciar**.  
  
4.  Una vez completado el proceso de limpieza asistida por PC, haga clic en **Siguiente** para continuar con la fase de limpieza interactiva (página**Administrar y ver resultados** ).  
  
##  <a name="Interactive"></a> Fase de limpieza interactiva  
 En la fase de limpieza interactiva, puede ver los cambios propuestos por DQS y decidir si desea implementarlos o no aprobándolos o rechazándolos. En el panel izquierdo de la página **Administrar y ver resultados** , DQS muestra una lista de todos los dominios asignados en la fase de asignación, junto con el número de valores de los datos de origen analizados en cada dominio durante la fase de limpieza asistida por PC. En el panel derecho de la página **Administrar y ver resultados** , y en función de su conformidad con las reglas de dominio, las reglas de error de sintaxis y los algoritmos avanzados, DQS clasifica los datos en cinco pestañas mediante el *nivel de confianza*. El nivel de confianza indica el grado de certeza de DQS para la corrección o sugerencia, y se basa en los umbrales siguientes:  
  
-   **Umbral de corrección automática**: DQS corrige automáticamente cualquier valor que tenga un nivel de confianza por encima de este umbral. Sin embargo, el administrador de datos puede invalidar el cambio durante la limpieza interactiva. Puede especificar el valor de umbral de corrección automática en la pestaña **Configuración general** de la pantalla **Configuración** . Para obtener más información, consulte [Configurar los valores de umbral para la limpieza y coincidencia](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Umbral de sugerencia automática**: cualquier valor que tenga un nivel de confianza por encima de este umbral, pero por debajo del umbral de corrección automática, se sugiere como valor de reemplazo. DQS realizará el cambio solo si el administrador de datos lo aprueba. Puede especificar el valor de umbral de sugerencia automática en la pestaña **Configuración general** de la pantalla **Configuración** . Para obtener más información, consulte [Configurar los valores de umbral para la limpieza y coincidencia](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Otro**: DQS deja como está cualquier valor que esté por debajo del valor de umbral de sugerencia automática.  
  
 En función del nivel de confianza, los valores se muestran en las cinco pestañas siguientes:  
  
|Pestaña|Descripción|  
|---------|-----------------|  
|**Sugerido**|Muestra los valores de dominio para los que DQS detectó sugerencias con un nivel de confianza mayor que el *umbral de sugerencia automática* , pero inferior al *umbral de corrección automática* .<br /><br /> Los valores sugeridos se muestran en la columna **Corregir a** junto al valor original. Haga clic en el botón de opción de la columna **Aprobar** o **Rechazar** junto a un valor de la cuadrícula superior para aceptar o rechazar la sugerencia para todas las instancias de dicho valor. En este caso, el valor aceptado se desplaza a la pestaña **Corregido** y el valor rechazado se desplaza a la pestaña **No válido** .|  
|**Nuevo**|Muestra el dominio válido para el que DQS no tiene suficiente información, por lo que no se puede asignar a ninguna otra pestaña. Además, esta pestaña también contiene valores con un nivel de confianza inferior al *umbral de sugerencia automática* , pero lo suficientemente altos para que se identifiquen como válidos.<br /><br /> Si cree que el valor es correcto, haga clic en el botón de opción de la columna **Aprobar** . En caso contrario, haga clic en el botón de opción de la columna **Rechazar** . El valor aceptado se desplaza a la pestaña **Correcto** y el valor rechazado se desplaza a la pestaña **No válido** . También puede escribir manualmente el valor correcto como sustituto del valor original en la columna **Corregir a** para el valor y, luego, hacer clic en el botón de opción de la columna **Aprobar** para aceptar el cambio. En este caso, el valor se desplaza a la pestaña **Corregido** .|  
|**No válido**|Muestra los valores de dominio que se marcaron como no válidos en el dominio de la base de conocimiento o los valores que no cumplieron una regla de dominio. Esta pestaña también contiene los valores rechazados por el usuario en cualquiera de las otras cuatro pestañas.<br /><br /> Sin embargo, si cree que un valor es correcto, haga clic en el botón de opción de la columna **Aprobar** . El valor aceptado se desplazará a la pestaña **Correcto** . También puede escribir manualmente el valor correcto como sustituto del valor original en la columna **Corregir a** para el valor y, luego, hacer clic en el botón de opción de la columna **Aprobar** para aceptar el cambio. En este caso, el valor se desplaza a la pestaña **Corregido** .|  
|**Corregido**|Muestra los valores de dominio corregidos por DQS durante el proceso de limpieza automatizada para los que DQS detectó una corrección para el valor con un nivel de confianza por encima del umbral de corrección automática.<br /><br /> Los valores corregidos se muestran en la columna **Corregir a** junto al valor original. De forma predeterminada, se selecciona el botón de opción de la columna **Aprobar** correspondiente al valor. Si procede, puede rechazar la corrección propuesta haciendo clic en el botón de radio de la columna **Rechazar** para desplazar el valor a la pestaña **No válido** , o escribir manualmente el valor correcto en la columna **Corregir a** y, a continuación, hacer clic en el botón de opción de la columna **Aprobar** para aceptar el cambio y desplazarlo a la pestaña **Corregido** .|  
|**Correcto**|Muestra los valores de dominio que se estiman correctos. Por ejemplo, si el valor coincide con un valor de dominio. Esta pestaña también contiene los valores que aprobó el usuario haciendo clic en el botón de opción de la columna **Aprobar** de las pestañas **Nuevo** y **No válido** .<br /><br /> De forma predeterminada, el botón de opción de la columna **Aprobar** correspondiente a cada valor está seleccionado. Sin embargo, si cree que hay un valor incorrecto en esta pestaña, haga clic en el botón de opción de la columna **Rechazar** junto al valor para desplazarlo a la pestaña **No válido** , o escriba manualmente el valor correcto como sustituto del valor original en la columna **Corregir a** para el valor y, a continuación, haga clic en el botón de opción de la columna **Aprobar** para aceptar el cambio y desplazarlo a la pestaña **Corregido** .|  
  
 Para limpiar los datos de forma interactiva:  
  
1.  En la página **Administrar y ver resultados** del asistente para la limpieza de calidad de datos, haga clic en el nombre de un dominio en el panel izquierdo.  
  
2.  Revise los valores de dominio de las cinco pestañas y tome las medidas apropiadas, tal como se ha explicado anteriormente.  
  
    -   El panel situado en la zona superior derecha muestra la información siguiente para cada valor del dominio seleccionado: valor original, número de instancias (registros), un cuadro para especificar otro valor (correcto), el nivel de confianza (no disponible para los valores de la pestaña **Correcto** ), el motivo de la acción realizada por DQS con el valor y la opción de aprobar o rechazar las correcciones y sugerencias para el valor.  
  
        > [!TIP]  
        >  Puede aprobar o rechazar todos los valores del dominio seleccionado en el panel de la esquina superior derecha haciendo clic en el icono **Aprobar todos los términos** o **Rechazar todos los términos** , respectivamente. O bien, puede hacer clic con el botón secundario en un valor del dominio seleccionado y hacer clic en **Aprobar todos** o **Rechazar todos** en el menú contextual.  
  
    -   El panel inferior muestra las repeticiones individuales del valor de dominio seleccionado en el panel de la esquina superior derecha. Se muestra la información siguiente: un cuadro para especificar otro valor (correcto), el nivel de confianza (no disponible para los valores de la pestaña **Correcto** ), el motivo de la acción realizada por DQS con el valor, la opción de aprobar o rechazar las correcciones y sugerencias para el valor, y el valor original.  
  
3.  Si habilitó la característica **Corrector ortográfico** de un dominio al crearlo, los valores de dominio identificados como errores potenciales aparecerán subrayados con una línea ondulada de color rojo. Todo el valor aparecerá subrayado. Por ejemplo, si “New York” está escrito incorrectamente como “Neu York”, el corrector ortográfico mostrará un subrayado rojo debajo de “Neu York”, no solo de “Neu”. Si hace clic con el botón secundario en el valor, verá las correcciones sugeridas. Si hay más de 5 sugerencias, haga clic en **Más sugerencias** en el menú contextual para ver el resto. Al igual que sucede con la presentación de errores, las sugerencias son reemplazos del valor completo. En el ejemplo anterior, se mostrará como sugerencia “New York”, no solo “New”. Puede elegir una de las sugerencias o agregar un valor al diccionario para que se muestre para ese valor. Los valores se almacenan en un diccionario en el nivel de cuenta de usuario. Al seleccionar una sugerencia en el menú contextual del corrector ortográfico, la sugerencia seleccionada se agregará a la columna **Corregir a** . Sin embargo, si selecciona una sugerencia en la columna **Corregir a** , el valor de la columna se sustituye por la sugerencia seleccionada.  
  
     La característica de corrector ortográfico se habilita de forma predeterminada en la fase de limpieza interactiva. Para deshabilitar el corrector ortográfico en la fase de limpieza interactiva, haga clic en el icono **Habilitar o deshabilitar el corrector ortográfico** o haga clic con el botón secundario en el área de valores de dominio y, a continuación, haga clic en **Corrector ortográfico** en el menú contextual. Para habilitarlo de nuevo, siga los mismos pasos.  
  
    > [!NOTE]  
    >  La característica de corrector ortográfico solo está disponible en el panel superior (valores de dominio). Además, no es posible habilitar ni deshabilitar el corrector ortográfico para los dominios compuestos. Los dominios secundarios de un dominio compuesto que sean de tipo cadena y se hayan habilitado para la característica de corrector ortográfico tendrán también habilitada dicha característica en la fase de limpieza interactiva de forma predeterminada.  
  
4.  Durante la fase de limpieza interactiva, active el generador de perfiles haciendo clic en la pestaña **Generador de perfiles** para ver la generación de perfiles y las notificaciones en tiempo real. Para obtener más información, consulte [Estadísticas del generador de perfiles](#Profiler).  
  
5.  Una vez que haya revisado todos los valores de dominio, haga clic en **Siguiente** para continuar con la fase de exportación.  
  
##  <a name="Export"></a> Fase de exportación  
 En la fase de exportación, especifique los parámetros para exportar los datos limpios: qué se debe exportar y a dónde.  
  
1.  En la página **Exportar** del asistente para la limpieza de calidad de datos, seleccione el tipo de destino para exportar los datos limpios: **SQL Server**, **Archivo CSV**o **Archivo de Excel**.  
  
    > [!IMPORTANT]  
    >  Si utiliza la versión de 64 bits de Excel, no puede exportar los datos limpiados en un archivo de Excel; puede exportar únicamente a una base de datos de SQL Server o un archivo .csv.  
  
    1.  **SQL Server**: seleccione **DQS_STAGING_DATA** como la base de datos de destino si desea exportar aquí los datos y, a continuación, especifique el nombre de la tabla que se creará para almacenar los datos exportados. En caso contrario, seleccione la base de datos a la que desea exportar los datos y, a continuación, especifique el nombre de la tabla que se creará para almacenar los datos exportados. La base de datos de destino debe encontrarse en la misma instancia de SQL Server que [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] para que aparezca en la lista desplegable **Base de datos** .  
  
    2.  **Archivo CSV**: haga clic en **Examinar**y especifique el nombre y la ubicación del archivo .csv al que desea exportar los datos limpios. O bien, escriba el nombre del archivo .csv junto con la ruta de acceso completa. Por ejemplo, “c:\DatosExportados.csv”. El archivo se guarda en el equipo en el que se ha instalado [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] .  
  
    3.  **Archivo de Excel**: haga clic en **Examinar**y especifique el nombre y la ubicación del archivo de Excel al que desea exportar los datos limpios. O bien, escriba el nombre del archivo de Excel junto con la ruta de acceso completa. Por ejemplo, “c:\DatosExportados.xlsx”. El archivo se guarda en el equipo en el que se ha instalado [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] .  
  
2.  Active la casilla **Estandarizar salida** para normalizar la salida en función del formato de salida seleccionado para el dominio. Por ejemplo, cambiar el valor de cadena a mayúsculas o poner en mayúscula la primera letra de la palabra. Para obtener información acerca de cómo especificar el formato de salida de un dominio, vea la lista **Dar formato a la salida para** en [Establecer propiedades de dominio](../data-quality-services/set-domain-properties.md).  
  
3.  A continuación, seleccione la salida de datos: exportar solo los datos limpios o exportar los datos limpios junto con la información de limpieza.  
  
    -   **Solo los datos**: haga clic en el botón de opción para exportar solo los datos limpios.  
  
    -   **Datos e información de limpieza**: haga clic en el botón de opción para exportar los datos siguientes para cada dominio:  
  
        -   **\<dominio>_Source**: El valor original del dominio.  
  
        -   **\<dominio>_Output**: Los valores limpios del dominio.  
  
        -   **\<dominio>_Reason**: El motivo especificado para la corrección del valor.  
  
        -   **\<dominio>_Confidence**: El nivel de confianza para todos los términos que se han corregido. Se muestra como el valor decimal equivalente al valor de porcentaje correspondiente. Por ejemplo, un nivel de confianza del 95% se mostrará como 0,9500000.  
  
        -   **\<dominio>_Status**: El estado del valor del dominio tras la limpieza de los datos. Por ejemplo, **Sugerido**, **Nuevo**, **No válido**, **Corregido**o **Correcto**.  
  
        -   **Estado de registro**: Además de tener un campo de estado para cada dominio asignado **(\<nombreDeDominio>_Status**), el campo **Estado de registro** muestra el estado de un registro. Si el estado de un dominio del registro es *Nuevo* o *Correcto*, el **Estado de registro** se establece en *Correcto*. Si el estado de cualquier dominio del registro es *Sugerido*, *No válido*o *Corregido*, el **Estado de registro** se establece en el valor correspondiente. Por ejemplo, si el estado de cualquier dominio del registro es *Sugerido*, el **Estado de registro** se establece en *Sugerido*.  
  
            > [!NOTE]  
            >  Si utiliza el servicio de datos de referencia para la operación de limpieza, también estarán disponibles para la exportación algunos datos adicionales sobre el valor de dominio. Para más información, vea [Limpiar datos mediante el conocimiento de datos de referencia &#40;externo&#41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
4.  Haga clic en **Exportar** para exportar los datos al destino seleccionado. Si seleccionó:  
  
    -   **SQL Server** como destino de los datos, se creará una nueva tabla con el nombre especificado en la base de datos seleccionada.  
  
    -   **Archivo CSV** como destino de los datos, se creará un archivo .csv en la ubicación del equipo de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con el nombre de archivo especificado anteriormente en el cuadro **Nombre de archivo CSV** .  
  
    -   **Archivo de Excel** como destino de los datos, se creará un archivo de Excel en la ubicación del equipo de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con el nombre de archivo especificado anteriormente en el cuadro **Nombre del archivo de Excel** .  
  
5.  Haga clic en **Finalizar** para cerrar el proyecto de calidad de datos.  
  
##  <a name="Profiler"></a> Profiler Statistics  
 La pestaña **Generador de perfiles** proporciona estadísticas que indican la calidad de los datos de origen. El proceso de generación de perfiles de datos le ayuda a evaluar la eficacia de la actividad de limpieza de datos y, posiblemente, a determinar en qué medida le ha ayudado esta actividad a mejorar la calidad de los datos.  
  
 La pestaña **Generador de perfiles** proporciona las estadísticas siguientes para los datos de origen, por campo y dominio:  
  
-   **Registros**: el número de registros de la muestra de datos que se analizaron para la actividad de limpieza de datos  
  
-   **Registros correctos**: el número de registros correctos  
  
-   **Registros corregidos**: el número de registros que se corrigieron  
  
-   **Registros sugeridos**: el número de registros que se sugirieron  
  
-   **Registros no válidos**: el número de registros que no eran válidos  
  
 Las estadísticas del campo incluyen las siguientes:  
  
-   **Campo**: nombre del campo de los datos de origen  
  
-   **Dominio**: nombre del dominio que se asigna al campo  
  
-   **Valores corregidos**: el número de valores de dominio que se corrigieron  
  
-   **Valores sugeridos**: el número de valores de dominio que se sugirieron  
  
-   **Integridad**: la integridad de cada campo de origen que se ha asignado para la actividad de limpieza  
  
-   **Precisión**: la precisión de cada campo de origen que se ha asignado para la actividad de limpieza  
  
 El proceso de generación de perfiles de DQS proporciona dos dimensiones de calidad de datos: *integridad* (la medida en que los datos están presentes) y *precisión* (la medida en que los datos se pueden utilizar para su uso previsto). Si la generación de perfiles le indica que un campo está relativamente incompleto, puede que desee quitarlo de la base de conocimiento de un proyecto de calidad de datos. La generación de perfiles no puede proporcionar estadísticas de integridad confiables para los dominios compuestos. Si necesita estadísticas de integridad, utilice dominios individuales en lugar de dominios compuestos. Si desea utilizar dominios compuestos, puede crear una base de conocimiento con dominios individuales para generar los perfiles y determinar la integridad, y crear otro dominio con un dominio compuesto para el proceso de limpieza. Por ejemplo, la generación de perfiles podría mostrar una integridad del 95% para los registros de direcciones utilizando un dominio compuesto, pero podría haber un nivel mucho más alto de falta de integridad en una de las columnas, por ejemplo, una columna de código postal (zip). En este ejemplo, podría medir la integridad de la columna de código postal con un dominio individual. La generación de perfiles probablemente proporcione estadísticas precisas y confiables para los dominios compuestos porque permite medir la precisión de varias columnas al mismo tiempo. El valor de estos datos está en la agregación compuesta, por lo que puede ser conveniente medir la precisión con un dominio compuesto.  
  
 Es probable que la interpretación de las estadísticas de precisión sea más laboriosa si no utiliza un servicio de datos de referencia. Si utiliza un servicio de datos de referencia para la limpieza de datos, tendrá un mayor nivel de confianza en las estadísticas de precisión. Para más información sobre la limpieza de datos mediante el servicio de datos de referencia, vea [Limpiar datos mediante el conocimiento de datos de referencia &#40;externo&#41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
### <a name="cleansing-notifications"></a>Notificaciones de limpieza  
 Las condiciones siguientes producen notificaciones:  
  
-   No hay correcciones ni sugerencias para un campo. Es posible que desee quitarlo de la asignación, ejecutar primero la detección de conocimiento o utilizar otra base de conocimiento.  
  
-   Hay relativamente pocas correcciones o sugerencias para un campo. Es posible que desee quitarlo de la asignación, ejecutar primero la detección de conocimiento o utilizar otra base de conocimiento.  
  
-   El nivel de precisión del campo es muy bajo. Es posible que desee comprobar la asignación o ejecutar primero la detección de conocimiento.  
  
 Para obtener más información sobre la generación de perfiles, vea [Generación de perfiles de datos y notificaciones de DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  

