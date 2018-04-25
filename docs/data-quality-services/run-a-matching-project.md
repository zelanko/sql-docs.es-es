---
title: Ejecutar un proyecto de coincidencia | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.matchingproject.map.f1
- sql13.dqs.matchingproject.matching.f1
- sql13.dqs.matchingproject.export.f1
ms.assetid: 6aa9d199-83ce-4b5d-8497-71eef9258745
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae48076185149d0ba1306260459ec7b34dcc8123
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="run-a-matching-project"></a>Ejecutar un proyecto de coincidencia

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo realizar la búsqueda de coincidencias de datos en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). El proceso de búsqueda de coincidencias identifica los clústeres de registros coincidentes en función de las reglas de coincidencia existentes en la directiva de coincidencia, designa un registro de cada clúster como el registro que permanece basándose en una regla de permanencia, y exporta los resultados. DQS realiza el proceso de búsqueda de coincidencias, también denominado eliminación de datos duplicados, en un proceso asistido por PC, pero es usted quien crea las reglas de coincidencia de forma interactiva y quien selecciona la regla de permanencia entre varias opciones, por lo que también es quien controla el proceso de búsqueda de coincidencias.  
  
 La búsqueda de coincidencias se realiza en tres fases: un proceso de asignación en el que se identifica el origen de datos y se asignan los dominios a dicho origen de datos, un proceso de búsqueda de coincidencias en el que se ejecuta el análisis de coincidencia, y un proceso de permanencia y exportación en el que se designa la regla de permanencia y se exportan los resultados de la búsqueda de coincidencias. Cada uno de estos procesos se realiza en una página distinta del asistente para la actividad de coincidencia, lo que le permite desplazarse de una página a otra, volver a ejecutar el proceso, y cerrar un proceso de búsqueda de coincidencias específico y volver a la misma fase del proceso. DQS proporciona estadísticas sobre los datos de origen, las reglas de coincidencia y los resultados de búsqueda de coincidencias que permiten tomar decisiones fundadas sobre la búsqueda de coincidencias y sobre cómo refinar este proceso.  
  
 Para preparar la búsqueda de coincidencias, debe crear una directiva de coincidencia con una o varias reglas de coincidencia y ejecutar dicha directiva con los datos de ejemplo. El proceso del proyecto de búsqueda de coincidencias es independiente del proceso de la directiva de coincidencia, lo que significa que una base de conocimiento no se rellena con el conocimiento de coincidencia obtenido del proyecto de búsqueda de coincidencias. Para obtener más información acerca de cómo crear una directiva de coincidencia, vea [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe haber creado una base de conocimiento con una directiva de coincidencia que conste de una o varias reglas de coincidencia.  
  
-   Si los datos de origen implicados en el proceso de búsqueda de coincidencias están en un archivo de Excel, es necesario tener instalado Microsoft Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . De lo contrario, no podrá seleccionar dicho archivo en la fase de asignación. Los archivos creados por Microsoft Excel pueden tener la extensión .xlsx, .xls o .csv. Si se utiliza la versión de 64 bits de Excel, solo se admitirán los archivos de Excel 2003 (.xls); los archivos de Excel 2007 o 2010 (.xlsx) no son compatibles. Si utiliza la versión de 64 bits de Excel 2007 o 2010, guarde el archivo como un archivo .xls o .csv, o instale una versión de 32 bits de Excel en su lugar.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para ejecutar un proyecto de búsqueda de coincidencias.  
  
##  <a name="StartingaMatchingProject"></a> Primer paso: iniciar un proyecto de búsqueda de coincidencias  
 Realizará la actividad de búsqueda de coincidencias en un proyecto de calidad de datos que creará en la aplicación cliente DQS.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Nuevo proyecto de calidad de datos** para realizar la búsqueda de coincidencias en un proyecto de calidad de datos nuevo. Escriba un nombre y una descripción para el proyecto de calidad de datos y seleccione la base de conocimiento que desea utilizar para la búsqueda de coincidencias en **Usar base de conocimiento**. Haga clic en **Coincidencia** para la actividad. Haga clic en **Siguiente** para pasar a la fase de asignación.  
  
3.  Haga clic en **Abrir proyecto de calidad de datos** para realizar la búsqueda de coincidencias en un proyecto de calidad de datos existente. Seleccione el proyecto y haga clic en **Siguiente**. (También puede hacer clic en un proyecto en **Proyecto de calidad de datos reciente**). Si abre un proyecto de búsqueda de coincidencias que está cerrado, continuará en la fase en la que se hallaba la actividad de proyecto de búsqueda de coincidencias en el momento en que se cerró; esta fase aparece indicada en la columna **Estado** de la tabla del proyecto o en el nombre del proyecto, debajo de **Proyecto de calidad de datos reciente**. Si abre un proyecto de búsqueda de coincidencias finalizado, irá a la página **Exportar** (no podrá modificar las pantallas anteriores).  
  
##  <a name="MappingStage"></a> Fase de asignación  
 En la fase de asignación, deberá identificar el origen de los datos en el que ejecutará el análisis de coincidencia y asignará columnas de origen a los dominios para ponerlos a disposición de la actividad de coincidencia.  
  
1.  Para ejecutar la búsqueda de coincidencias en una base de datos, en la página **Asignación** , deje **Origen de datos** como **SQL Server**, seleccione la base de datos en la que desea ejecutar la búsqueda de coincidencias y, a continuación, seleccione la tabla. La base de datos de origen debe encontrarse en la misma instancia de SQL Server que el servidor DQS. En caso contrario, no aparecerá en la lista desplegable.  
  
2.  Para ejecutar la búsqueda de coincidencias en los datos de una hoja de cálculo de Excel, seleccione **Archivo de Excel** en **Origen de datos**, haga clic en **Examinar** , seleccione el archivo Excel y deje seleccionado **Usar la primera fila como encabezado** , si procede. En **Hoja de cálculo**, seleccione la hoja de cálculo del archivo de Excel que será el origen de los datos. Es necesario tener instalado Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para seleccionar un archivo de Excel. Si Excel no está instalado en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , el botón **Examinar** no estará disponible, y aparecerá una notificación debajo de este cuadro de texto indicándole que Excel no está instalado.  
  
3.  En **Asignaciones**, seleccione un campo del origen de datos para **Columna de origen**y, continuación, seleccione el dominio correspondiente. Repita este procedimiento con todos los dominios que utilice en el proceso de búsqueda de coincidencias. Cada dominio definido en la directiva de coincidencia debe asignarse a la columna de origen correspondiente. En el panel derecho de la página Asignación aparecen los dominios que se han definido en la directiva de coincidencia y las reglas existentes en dicha directiva.  
  
    > [!NOTE]  
    >  Solo puede asignar los datos de origen para un dominio DQS si el tipo de datos de origen se admiten en DQS y coincide con el tipo de datos de dominio DQS. Para obtener información acerca de los tipos de datos admitidos en DQS, vea [Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
4.  Haga clic en el control **más (+)** para agregar una fila a la tabla Asignaciones o en el control **menos (–)** para eliminarla.  
  
5.  Haga clic en **Vista previa del origen de datos** para ver los datos de la tabla o vista de SQL Server que ha seleccionado, o para ver la hoja de cálculo de Excel que ha seleccionado.  
  
6.  Haga clic en **Ver o seleccionar dominios compuestos** para ver una lista de los dominios compuestos disponibles en la base de conocimiento y seleccionar el que corresponda para la asignación.  
  
7.  Haga clic en **Siguiente** para pasar a la fase de coincidencia.  
  
    > [!NOTE]  
    >  Haga clic en **Cerrar** para guardar la fase del proyecto de búsqueda de coincidencias y volver a la página de inicio de DQS. La próxima vez que abra este proyecto, se iniciará en la misma fase. Haga clic en **Cancelar** para finalizar la actividad de búsqueda de coincidencias, perder los cambios realizados y volver a la página de inicio de DQS.  
  
##  <a name="MatchingStage"></a> Fase de coincidencia  
 En esta fase, realizará un proceso de búsqueda de coincidencias asistido por PC que mostrará el número de coincidencias existentes en los datos de origen basándose en las reglas de coincidencia. Este proceso generará una tabla con los resultados de búsqueda de coincidencias que mostrará los clústeres que DQS ha identificado, cada uno de los registros del clúster con su identificador de registro y su puntuación de coincidencia, y el registro inicial del clúster. El registro inicial del clúster se selecciona aleatoriamente. Para determinar el registro que permanece, seleccione la regla de permanencia en la página **Exportar** cuando ejecute el proyecto de búsqueda de coincidencias. Cada fila adicional de un clúster se considera una coincidencia; su puntuación de coincidencia (comparada con la del registro inicial) se muestra en la tabla de resultados. El número de clúster es el mismo que el identificador de registro del registro inicial del clúster.  
  
 En los resultados de búsqueda de coincidencias, podrá filtrar los datos que desee y rechazar las coincidencias que estime oportuno. Podrá mostrar datos de generación de perfiles para el proceso de búsqueda de coincidencias en su conjunto, detalles sobre las reglas de coincidencia aplicadas, y estadísticas globales de los resultados de búsqueda de coincidencias. El proceso de búsqueda de coincidencias puede identificar clústeres superpuestos y no superpuestos y, si se ejecuta varias veces, se puede ejecutar con los datos copiados del origen y reindizados, o con los datos anteriores.  
  
1.  En la página **Coincidencia**, seleccione **Clústeres superpuestos** en la lista desplegable para mostrar los registros dinámicos y los registros siguientes de todos los clústeres cuando se ejecute la búsqueda de coincidencias, incluso si los grupos de clústeres tienen registros en común. Seleccione **Clústeres no superpuestos** para mostrar, como un solo clúster, los clústeres que tienen registros en común cuando se ejecute la búsqueda de coincidencias.  
  
2.  Haga clic en **Volver a cargar los datos del origen** (valor predeterminado) para copiar los datos del origen de datos en la tabla de ensayo y volverlos a indizar cuando se ejecute el proyecto de búsqueda de coincidencias. Haga clic en **Ejecutar con los datos anteriores** para ejecutar un proyecto de búsqueda de coincidencias sin copiar los datos en la tabla de ensayo ni volver a indizarlos. **Ejecutar con los datos anteriores** aparece deshabilitado la primera vez que se ejecuta el proyecto de búsqueda de coincidencias, o si cambia la asignación en la página **Asignación** y, a continuación, presiona **Sí** en el cuadro emergente. En ambos casos, es necesario volver a indizar. No será necesario volver a indizar si el proyecto de búsqueda de coincidencias no ha sufrido cambios. La ejecución con los datos anteriores puede mejorar el rendimiento.  
  
3.  Haga clic en **Iniciar** para ejecutar la búsqueda de coincidencias en el origen de datos seleccionado.  
  
4.  Haga clic en **Detener** si desea detener el proyecto de búsqueda de coincidencias y descartar los resultados.  
  
5.  Cuando el proceso de búsqueda de coincidencias haya finalizado, compruebe que los clústeres de la tabla **Resultados de búsqueda de coincidencias** son los adecuados y vea las estadísticas de las pestañas **Generador de perfiles** y **Resultados de búsqueda de coincidencias** para asegurarse de que ha obtenido los resultados esperados. Para ver los registros coincidentes, seleccione **Coincidente** en **Filtro** ; para ver los registros no coincidentes, seleccione **Sin coincidencia**.  
  
6.  Si la directiva de coincidencia tiene varias reglas de coincidencia, haga clic en la pestaña **Reglas de coincidencia** para identificar el icono de cada regla y, a continuación, compruebe qué regla ha identificado un registro como coincidente; para ello, busque la regla en la columna **Regla** de la tabla **Resultados de búsqueda de coincidencias** .  
  
7.  Si selecciona un registro no dinámico en la tabla y hace clic en el icono **Ver detalles** (o hace doble clic en el registro), DQS mostrará el cuadro emergente **Detalles de puntuación de coincidencia** , en el que aparecen el registro en el que ha hecho doble clic y su registro dinámico (y los valores de todos los campos), la puntuación existente entre ellos y detalles acerca de la contribución de cada campo a la puntuación de coincidencia. Cuando se hace doble clic en un registro dinámico, no aparece el cuadro emergente.  
  
8.  Haga clic en el icono **Contraer todo** para contraer los registros de la tabla **Resultados de búsqueda de coincidencias** y mostrar solo el registro dinámico, no los registros duplicados. Haga clic en **Expandir todo** para expandir los registros de la tabla Resultados de búsqueda de coincidencias y mostrar todos los registros duplicados.  
  
9. Para rechazar un registro de los resultados de búsqueda de coincidencias, haga clic en la casilla **Rechazado** del registro.  
  
10. Para cambiar la puntuación de coincidencia mínima que determina el nivel de coincidencia que debe tener un registro para que se muestre, seleccione el icono **Puntuación de coincidencia mínima**, situado sobre el lado derecho de la tabla, y escriba un número mayor. De forma predeterminada, la puntuación de coincidencia mínima se establece en un 80%. Haga clic en **Actualizar** para cambiar el contenido de la tabla.  
  
11. Una vez que se haya completado el análisis, el botón **Iniciar** se convertirá en el botón **Reiniciar** . Haga clic en **Reiniciar** para volver a ejecutar el proceso de análisis. Sin embargo, tenga en cuenta que los resultados del análisis anterior aún no se han guardado, por lo que, si hace clic en **Reiniciar** , los perderá. Para continuar, haga clic en **Sí** en el cuadro emergente. Mientras se ejecuta el análisis, no abandone la página o el proceso de análisis se terminará.  
  
12. Haga clic en **Siguiente** para continuar con la fase de permanencia y exportación.  
  
##  <a name="SurvivorshipandExportStage"></a> Fase de permanencia y exportación  
 En el proceso de permanencia, Data Quality Services determina el registro que permanece para cada clúster; este registro reemplazará a los registros que coinciden con él en el clúster. A continuación, exporta los resultados de búsqueda de coincidencias y/o permanencia a una tabla de la base de datos de SQL Server, a un archivo .csv o a un archivo de Excel.  
  
 La permanencia es opcional. Puede exportar los resultados sin ejecutar la permanencia, en cuyo caso DQS utilizará el registro dinámico que designó en el análisis de coincidencia. Si dos o más registros de un clúster cumplen la regla de permanencia, el proceso de permanencia seleccionará como el registro que permanece aquel cuyo identificador de registro sea más bajo. Puede exportar los registros que permanecen a varios archivos o tablas usando reglas de permanencia diferentes.  
  
1.  En la página **Exportar** , seleccione el destino al que desea exportar los datos coincidentes en **Tipo de destino**: **SQL Server**, **Archivo CSV**o **Archivo de Excel**.  
  
    > [!IMPORTANT]  
    >  Si utiliza la versión de 64 bits de Excel, no puede exportar los datos coincidentes en un archivo de Excel; puede exportar únicamente a una base de datos de SQL Server o un archivo .csv.  
  
2.  Si seleccionó **SQL Server** en **Tipo de destino**, seleccione la base de datos a la que desea exportar los resultados en **Nombre de base de datos**.  
  
    > [!IMPORTANT]  
    >  La base de datos de destino debe encontrarse en la misma instancia de SQL Server que el servidor DQS. En caso contrario, no aparecerá en la lista desplegable.  
  
3.  Active la casilla **Resultados de búsqueda de coincidencias** si desea exportar los resultados de búsqueda de coincidencias (vea la explicación más arriba) a la tabla designada de una base de datos de SQL Server, o al archivo de Excel o archivo .csv designado. Active la casilla **Resultados de permanencia** si desea exportar los resultados de permanencia (vea la explicación más arriba) a la tabla designada de una base de datos de SQL Server, o al archivo de Excel o archivo .csv designado.  
  
     Si selecciona Resultados de búsqueda de coincidencias, se exportará lo siguiente:  
  
    -   Una lista de clústeres y los registros coincidentes de cada clúster, incluido el nombre de la regla y la puntuación. El registro dinámico se marcará como “Dinamización”. Los clústeres aparecerán en primer lugar en la lista de exportación.  
  
    -   Una lista de registros no coincidentes, con el valor “NULL” en las columnas Puntuación y Nombre de la regla. Estos registros se anexarán a la lista de exportación a continuación de los clústeres.  
  
     Si selecciona Resultados de permanencia, se exportará lo siguiente:  
  
    -   Una lista de los registros que permanecen tal y como lo determina el proceso de permanencia de acuerdo con la regla de permanencia. Estos registros aparecen en primer lugar en la lista de exportación.  
  
    -   Una lista de los registros no coincidentes que no están incluidos en los clústeres de registros coincidentes. Estos registros se anexan a continuación de los resultados de permanencia.  
  
4.  Si seleccionó **SQL Server** en **Tipo de destino**, escriba en **Nombre de la tabla**los nombres de las tablas a las que desea exportar los resultados. Si exporta tanto los resultados de búsqueda de coincidencias como los resultados de permanencia, las tablas de destino deberán tener nombres diferentes que sean únicos en la base de datos.  
  
5.  Si seleccionó **Archivo CSV** en **Tipo de destino**, escriba en **Nombre de archivo CSV**el nombre y la ruta de acceso del archivo CSV al que desea exportar.  
  
6.  Si seleccionó **Archivo de Excel** en **Tipo de destino**, escriba en **Nombre del archivo de Excel**el nombre y la ruta de acceso del archivo de Excel al que desea exportar. No puede exportar a un archivo de Excel si utiliza la versión de 64 bits de Excel.  
  
7.  Seleccione la regla de permanencia de la siguiente manera:  
  
    -   Seleccione **Registro dinámico** (valor predeterminado) para identificar el registro que permanece como el registro dinámico inicial elegido arbitrariamente por DQS.  
  
    -   Seleccione **Registro más completo y más largo** para identificar el registro que permanece como el registro con el mayor número de campos rellenos y con el mayor número de términos en cada campo. Se comprueban todos los campos de origen, incluidos los que no se asignaron a ningún dominio en la página **Asignación** .  
  
    -   Seleccione **Registro más completo** para identificar el registro que permanece como el registro con el mayor número de campos rellenos. Un campo está relleno si contiene al menos un valor (cadena, número o ambos). Se comprueban todos los campos de origen, incluidos los que no se asignaron a ningún dominio en la página Asignación. Un campo está relleno si contiene al menos un valor (cadena, número o ambos).  
  
    -   Seleccione **Registro más largo** para identificar el registro que permanece como el registro con el mayor número de términos en sus campos de origen. Para determinar la longitud de cada registro, DQS comprueba la longitud de los términos en todos los campos de origen, incluidos los campos que no se asignaron a ningún dominio en la página **Asignación** .  
  
8.  Vea las estadísticas de la pestaña **Generador de perfiles** para asegurarse de que ha obtenido los resultados esperados.  
  
9. Haga clic en **Exportar** para exportar los resultados. Al hacerlo, aparece un cuadro de diálogo Exportación de coincidencia que muestra el progreso y los resultados de la exportación.  
  
    -   Si seleccionó **SQL Server** como destino de los datos, se creará una nueva tabla con el nombre especificado en la base de datos seleccionada.  
  
    -   Si seleccionó **Archivo CSV** como destino de los datos, se creará un archivo .csv en la ubicación del equipo de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con el nombre de archivo especificado anteriormente en el cuadro **Nombre de archivo csv** .  
  
    -   Si seleccionó **Archivo de Excel** como destino de los datos, se creará un archivo .xlsx en la ubicación del equipo de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con el nombre de archivo especificado anteriormente en el cuadro **Nombre del archivo de Excel** .  
  
10. Compruebe que la exportación se ha realizado correctamente y, a continuación, haga clic en **Cerrar**.  
  
11. Haga clic en **Finalizar** para completar el proyecto de búsqueda de coincidencias.  
  
    > [!NOTE]  
    >  Si finaliza un proyecto de búsqueda de coincidencias y, más adelante, lo vuelve a utilizar, este usará la base de conocimiento que tenía cuando se publicó. No usará ninguno de los cambios realizados en la base de conocimiento desde la finalización del proyecto. Para utilizar estos cambios, o para utilizar una base de conocimiento nueva, tendrá que crear un proyecto de búsqueda de coincidencias nuevo. Por otro lado, si ha creado, pero no finalizado, un proyecto de búsqueda de coincidencias, los cambios que haya publicado en la directiva de coincidencia se utilizarán si ejecuta la búsqueda de coincidencias en el proyecto.  
  
##  <a name="FollowUp"></a> Seguimiento: después de ejecutar un proyecto de búsqueda de coincidencias  
 Después de ejecutar un proyecto de búsqueda de coincidencias, puede cambiar la directiva de coincidencia en la base de conocimiento y crear y ejecutar otro proyecto de búsqueda de coincidencias basado en la directiva de coincidencia actualizada. Para obtener más información, consulte [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Profiler"></a> Pestañas Generador de perfiles y Resultados  
 Las pestañas Generador de perfiles y Resultados contienen las estadísticas del proceso de búsqueda de coincidencias.  
  
### <a name="profiler-tab"></a>Pestaña Generador de perfiles  
 Haga clic en la pestaña **Generador de perfiles** para mostrar las estadísticas de la base de datos de origen y de cada campo de la regla de directiva. Las estadísticas se actualizarán mientras se ejecuta la regla de directiva. La función de generación de perfiles le ayudará a evaluar la eficacia del proceso de eliminación de datos duplicados, lo que le permitirá determinar en qué medida dicho proceso puede mejorar la calidad de los datos. La precisión en el proceso de generación de perfiles no es importante en un proyecto de búsqueda de coincidencias.  
  
 Las estadísticas de la base de datos de origen incluyen:  
  
-   **Registros**: el número total de registros existentes en la base de datos  
  
-   **Valores totales**: el número total de valores existentes en los campos  
  
-   **Nuevos valores**: el número total de valores que son nuevos desde la ejecución anterior y su porcentaje del total  
  
-   **Valores únicos**: el número total de valores únicos existentes en los campos y su porcentaje del total  
  
-   **Nuevos valores únicos**: el número total de valores únicos que son nuevos en los campos y su porcentaje del total  
  
 Las estadísticas del campo incluyen las siguientes:  
  
-   **Campo**: nombre del campo incluido en las asignaciones  
  
-   **Dominio**: nombre del dominio asignado al campo  
  
-   **Nuevo**: el número de nuevas coincidencias encontradas y su porcentaje del total  
  
-   **Único**: el número de registros únicos del campo y su porcentaje sobre el total  
  
-   **Integridad**: el porcentaje de la regla que se ha ejecutado  
  
### <a name="matching-policy-notifications"></a>Notificaciones de directiva de coincidencia  
 En la actividad de directiva de coincidencia, se producen notificaciones cuando se dan las condiciones siguientes:  
  
-   El campo está vacío en todos los registros; se recomienda eliminarlo de la asignación.  
  
-   La puntuación de integridad del campo es muy baja; puede que desee eliminarlo de la asignación.  
  
-   Ninguno de los valores de un campo es válido; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
-   Hay un nivel bajo de valores válidos en el campo; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
-   Existe un alto grado de singularidad en el campo. El uso de este campo en la directiva de coincidencia puede disminuir los resultados de búsqueda de coincidencias.  
  
### <a name="matching-rules-tab"></a>Pestaña Reglas de coincidencia  
 Haga clic en esta pestaña para mostrar una lista de las reglas existentes en la directiva de coincidencia y las condiciones de una regla.  
  
 **Lista de reglas**  
 Muestra una lista de todas las reglas de coincidencia existentes en la directiva de coincidencia. Seleccione una de las reglas para mostrar sus condiciones en la tabla Regla de coincidencia.  
  
 **Tabla Regla de coincidencia**  
 Muestra todas las condiciones de la regla seleccionada, incluidos el dominio, el valor de similitud, la ponderación y la selección de requisitos previos.  
  
### <a name="matching-results-tab"></a>Pestaña Resultados de búsqueda de coincidencias  
 Haga clic en la pestaña **Resultados de búsqueda de coincidencias** para mostrar las estadísticas del análisis del origen de datos usando el conocimiento seleccionado para el proyecto y la regla o reglas de coincidencia de la base de conocimiento. Las estadísticas incluyen:  
  
-   El número total de registros existentes en la base de datos  
  
-   El número total de registros coincidentes existentes en la base de datos  
  
-   El número de registros existentes en la base de datos que no se consideran duplicados  
  
-   El número de clústeres descubiertos  
  
-   El promedio de tamaño de clúster (el número de registros duplicados dividido por el número de clústeres)  
  
-   El menor número de duplicados existentes en un clúster  
  
-   El mayor número de duplicados existentes en un clúster  
  
  
