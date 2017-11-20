---
title: Crear una directiva de coincidencia | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.kb.kbmatchingmap.f1
- sql13.dqs.kb.kbmatchingpolicy.f1
- sql13.dqs.kb.kbmatchingresults.f1
ms.assetid: cce77a06-ca31-47b6-8146-22edf001d605
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fe1c8b25d8309d3984c70c31f5949a9724599a3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="create-a-matching-policy"></a>Crear una directiva de coincidencia
  En este tema se describe cómo crear una directiva de coincidencia en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). El proceso de búsqueda de coincidencias se prepara en DQS ejecutando la actividad Directiva de coincidencia con los datos de ejemplo. En esta actividad creará y probará una o varias reglas de coincidencia en la directiva y después publicará la base de conocimiento para poner a disposición pública las reglas de coincidencia. Solo puede haber una directiva de coincidencia en cada base de conocimiento, pero esta directiva puede contener varias reglas de coincidencia.  
  
 La creación de directivas de coincidencia se realiza en tres etapas: un proceso de asignación en el que se identifica el origen de datos y se asignan dominios a las columnas, un proceso de directiva de coincidencia en el que se pueden crear una o varias reglas de coincidencia y probar cada regla de coincidencia por separado, y un proceso de resultados de búsqueda de coincidencias en el que se ejecutan todas las reglas de coincidencia juntas y, si se está satisfecho con ellas, se agrega la directiva a la base de conocimiento. Cada uno de estos procesos se realiza en una página distinta del asistente para la actividad Directiva de coincidencia, lo que le permite desplazarse de una página a otra, volver a ejecutar el proceso y cerrar un proceso de directiva de coincidencia específico y volver a la misma fase del proceso. Después de comprobar todas las reglas juntas, si lo desea puede volver a la página **Directiva de coincidencia** , modificar una de las reglas, probarla de nuevo por separado y, a continuación, volver a la página **Resultados de búsqueda de coincidencias** para volver a ejecutar todas las reglas juntas. DQS proporciona estadísticas sobre los datos de origen, las reglas de coincidencia y los resultados de búsqueda de coincidencias que permiten tomar decisiones fundadas sobre la directiva de coincidencia para poder mejorarla.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Si los datos de origen están en un archivo de Excel, es necesario tener instalado Microsoft Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . De lo contrario, no podrá seleccionar dicho archivo en la fase de asignación. Los archivos creados por Microsoft Excel pueden tener la extensión .xlsx, .xls o .csv. Si se utiliza la versión de 64 bits de Excel, solo se admitirán los archivos de Excel 2003 (.xls); los archivos de Excel 2007 o 2010 (.xlsx) no son compatibles. Si utiliza la versión de 64 bits de Excel 2007 o 2010, guarde el archivo como un archivo .xls o .csv, o instale una versión de 32 bits de Excel en su lugar.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para crear una directiva de coincidencia.  
  
##  <a name="MatchingRules"></a> Cómo establecer parámetros para las reglas de coincidencia  
 La creación de una regla de coincidencia es un proceso iterativo en el que se especifican los factores utilizados para determinar si un registro coincide con otro. Puede especificar condiciones para cualquier dominio de una tabla. Cuando DQS realiza el proceso de búsqueda de coincidencias con dos registros, comparará los valores de los campos asignados a los dominios que están incluidos en la regla de coincidencia. DQS analiza los valores de cada campo de la regla y, a continuación, utiliza los factores especificados en la regla para cada dominio con objeto de calcular una puntuación de coincidencia final. Si la puntuación de coincidencia para los dos registros comparados es mayor que la puntuación de coincidencia mínima, los dos campos se consideran coincidencias.  
  
 En una regla de coincidencia se especifican los factores siguientes:  
  
-   Ponderación: para cada dominio de la regla, especifique una ponderación numérica que determina el modo en que el análisis de coincidencia para el dominio se comparará con el de los demás dominios de la regla. La ponderación indica la contribución de la puntuación del campo a la puntuación de coincidencia total entre dos registros. Las puntuaciones calculadas asignadas a cada campo de origen se suman para obtener la puntuación de coincidencia compuesta de los dos registros. Para cada campo que no sea un requisito previo (con una similitud de Exacto o Similar), establezca la ponderación entre 10 y 100. La suma de las ponderaciones de los dominios que no son requisitos previos debe ser igual a 100. Si el valor es un requisito previo, la ponderación se establece en 0 y no se puede cambiar.  
  
-   Similitud de Exacto: seleccione **Exacto** si los valores del mismo campo de dos registros diferentes deben ser idénticos para que los valores se consideren una coincidencia. Si son idénticos, la puntuación de coincidencia para ese dominio se establecerá en “100” y DQS utilizará dicha puntuación y las puntuaciones de los demás dominios de la regla para determinar la puntuación de coincidencia global. Si no son idénticos, la puntuación de coincidencia para ese dominio se establecerá en “0“ y el procesamiento de la regla continuará con la siguiente condición. Si está configurando una regla de coincidencia para un dominio numérico y selecciona **Similar**, puede especificar una tolerancia en forma de porcentaje o de número entero. Para un dominio del tipo fecha, puede especificar una tolerancia en días, meses o años (enteros) si selecciona **Similar**; la tolerancia para un dominio de fecha no puede expresarse en forma de porcentaje. Si selecciona **Exacto**, no tiene esta opción.  
  
-   Similitud de Similar: seleccione **Similar** si se puede considerar que los dos valores del mismo campo de dos registros distintos son una coincidencia aunque los valores no sean idénticos. Cuando DQS ejecute la regla, calculará una puntuación de coincidencia para ese dominio y utilizará la puntuación y las puntuaciones de los demás dominios de la regla para determinar la puntuación de coincidencia global. La similitud mínima entre los valores de un campo es del 60%. Si la puntuación de coincidencia calculada para un mismo campo de dos registros es menor que 60, la puntuación de similitud se establece automáticamente en 0. Si está configurando una regla de coincidencia para un campo numérico y selecciona **Similar**, puede especificar una tolerancia en forma de porcentaje o de número entero. Si está configurando una regla de coincidencia para un campo de fecha y selecciona **similar**, puede especificar una tolerancia numérica.  
  
-   Requisito previo: seleccione **Requisito previo** para especificar que los valores del mismo campo de dos registros distintos deben devolver una coincidencia del 100%; en caso contrario, los registros no se consideran una coincidencia y las demás cláusulas de la regla no se tienen en cuenta. Cuando se selecciona **Requisito previo** , se quita el campo de ponderación para el dominio de modo que no puede definir una ponderación para el dominio. Debe restablecer una o varias ponderaciones del dominio de modo que la suma de todas ellas sea igual a 100. Los dominios de requisito previo no contribuyen a la puntuación de coincidencia de los registros. La puntuación de coincidencia de los registros se determina comparando los valores de los campos cuya similitud se establece en Similar o Exacto. Cuando un campo es un requisito previo, la similitud para ese dominio se establece automáticamente en Exacto.  
  
 La puntuación de coincidencia mínima es el umbral que, una vez alcanzado o superado, hace que dos registros se consideren una coincidencia (el estado de los registros se establece en “Coincidente”). Especifique un valor entero en incrementos de “1” o haga clic en la flecha arriba o abajo para aumentar o disminuir el valor en incrementos de “10”. El valor mínimo es 80. Si la puntuación de coincidencia se encuentra por debajo de 80, los dos registros no se consideran una coincidencia. No puede cambiar el intervalo de puntuación de coincidencia mínima en esta página. La puntuación de coincidencia mínima es de 80. Puede, no obstante, cambiar la puntuación de coincidencia mínima más baja en la página Administración (si es un administrador de DQS).  
  
 La creación de una regla de coincidencia es un proceso iterativo porque puede que necesite cambiar las ponderaciones relativas de los dominios de la regla, la similitud o la propiedad de requisito previo de un dominio o la puntuación de coincidencia mínima para la regla con la finalidad de obtener los resultados que precisa. También puede darse el caso de que necesite crear varias reglas, que se ejecutarán sucesivamente para crear la puntuación de coincidencia. Puede que le resulte difícil obtener el resultado que necesita con una sola regla. El uso de varias reglas proporcionará distintas vistas de una coincidencia necesaria. Con varias reglas, quizá pueda incluir menos dominios en cada regla, utilizar ponderaciones mayores para cada dominio y lograr mejores resultados. Si los datos son menos precisos y completos, puede que necesite más reglas para buscar las coincidencias necesarias. Si los datos son más precisos y completos, necesitará menos reglas.  
  
 La generación de perfiles proporciona nuevas perspectivas sobre la integridad y la unicidad. Considere que la integridad y la unicidad forman un tándem. Utilice los datos de integridad y unicidad para determinar qué ponderación debe tener un campo en el proceso de búsqueda de coincidencias. Si hay un nivel alto de unicidad en un campo, utilizar ese campo en una directiva de coincidencia puede reducir los resultados de búsqueda de coincidencias, por lo que puede establecer la ponderación de ese campo en un valor relativamente pequeño. Si tiene un bajo nivel de unicidad en una columna, pero la integridad es baja, es posible que no desee incluir un dominio para esa columna. Si el nivel de unicidad es bajo, pero el nivel de integridad es alto, puede que desee incluir el dominio. Algunas columnas, como sexo, pueden tener un nivel bajo de unicidad intrínseco. Para obtener más información, consulte [Pestañas Generador de perfiles y Resultados](#Tabs).  
  
##  <a name="Starting"></a> Primer paso: iniciar una directiva de coincidencia  
 La actividad de directiva de coincidencia se realiza en el área de administración de la base de conocimiento de la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Nueva base de conocimiento** para crear una directiva de coincidencia en una nueva base de conocimiento. Escriba un nombre para la base de conocimiento, escriba una descripción y seleccione lo que desee en **Crear base de conocimiento a partir de** . Haga clic en **Directiva de coincidencia** para la actividad. Haga clic en **Siguiente** para continuar.  
  
3.  Haga clic en **Abrir base de conocimiento** para crear o modificar la directiva de coincidencia de una base de conocimiento existente. Seleccione la base de conocimiento, seleccione **Directiva de coincidencia**y, a continuación, haga clic en **Siguiente**. También puede hacer clic en una base de conocimiento en **Base de conocimiento reciente**. Si abre una base de conocimiento que se cerró mientras se trabajaba en una directiva de coincidencia, continuará en la fase en la que se cerró la actividad de la directiva de coincidencia (indicada por la columna **Estado** para la base de conocimiento en la tabla de bases de conocimiento o en el nombre de la base de conocimiento en **Base de conocimiento reciente**). Si abre una base de conocimiento que incluye una directiva de coincidencia y que se había finalizado, irá a la página **Directiva de coincidencia** . Si abre una base de conocimiento que no incluye una directiva de coincidencia y que se había finalizado, irá a la página **Asignación** .  
  
##  <a name="MatchingStage"></a> Fase de asignación  
 En la fase de asignación, deberá identificar el origen de los datos para el que creará la directiva de coincidencia y asignará columnas de origen a los dominios para ponerlos a disposición de la actividad de directiva de coincidencia.  
  
1.  En la página **Asignación** , para crear una directiva para una base de datos, deje **Origen de datos** como **SQL Server**, seleccione la base de datos para la que desea crear la directiva en **Base de datos**y, a continuación, seleccione la tabla o la vista en **Tabla/vista**. La base de datos de origen debe encontrarse en la misma instancia de SQL Server que [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. En caso contrario, no aparecerá en la lista desplegable.  
  
2.  Para crear una directiva para los datos de una hoja de cálculo de Excel, seleccione **Archivo de Excel** en **Origen de datos**, haga clic en **Examinar** y seleccione el archivo de Excel y deje seleccionado **Usar la primera fila como encabezado** si procede. En **Hoja de cálculo**, seleccione la hoja de cálculo del archivo de Excel que será el origen de los datos. Para seleccionar un archivo de Excel, es necesario tener instalado Microsoft Excel en el equipo de Data Quality Client. De lo contrario, el botón Examinar no estará disponible y se le notificará debajo de este cuadro de texto que Microsoft Excel no está instalado.  
  
3.  En **Asignaciones**, seleccione un campo para la **Columna de origen**y, a continuación, haga clic en el icono **Crear dominio** .  
  
4.  En **Asignaciones**, seleccione un campo del origen de datos para **Columna de origen**y, continuación, seleccione el dominio correspondiente. Repita este procedimiento con todos los dominios que utilice en el proceso de búsqueda de coincidencias. Cree los dominios necesarios haciendo clic en **Crear un dominio** o en **Crear un dominio compuesto**.  
  
    > [!NOTE]  
    >  Solo puede asignar los datos de origen para un dominio DQS mientras crea una directiva de coincidencia si el tipo de datos de origen se admite en DQS y coincide con el tipo de datos de dominio DQS. Para obtener información acerca de los tipos de datos admitidos en DQS, vea [Compatibilidad con los tipos de datos en SQL Server y SSIS para dominios DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
5.  Haga clic en el control **más (+)** para agregar una fila a la tabla Asignaciones o en el control **menos (–)** para eliminarla.  
  
6.  Haga clic en **Vista previa del origen de datos** para ver los datos de la tabla o vista de SQL Server que ha seleccionado, o para ver la hoja de cálculo de Excel que ha seleccionado.  
  
7.  Haga clic en **Ver o seleccionar dominios compuestos** para ver una lista de los dominios compuestos disponibles en la base de conocimiento y seleccionar el que corresponda para la asignación.  
  
8.  Haga clic en **Siguiente** para pasar a la fase de directiva de coincidencia.  
  
    > [!NOTE]  
    >  Haga clic en **Cerrar** para guardar la fase del proyecto de búsqueda de coincidencias y volver a la página de inicio de DQS. La próxima vez que abra este proyecto, se iniciará en la misma fase. Haga clic en **Cancelar** para finalizar la actividad de búsqueda de coincidencias, perder los cambios realizados y volver a la página de inicio de DQS.  
  
##  <a name="MatchingPolicyStage"></a> Fase de directiva de coincidencia  
 Las reglas de coincidencia se crean y se prueban por separado en la página Directiva de coincidencia. Cuando se prueba una regla de coincidencia en la página **Directiva de coincidencia** , se ve una tabla de resultados de búsqueda de coincidencias que muestra los clústeres que DQS ha identificado para la regla seleccionada. La tabla muestra cada registro del clúster con los valores de los dominios de asignación y la puntuación de coincidencia, junto con el registro dinámico inicial para el clúster. También es posible mostrar datos de generación de perfiles para el proceso de búsqueda de coincidencias en conjunto, las condiciones de cada regla de coincidencia y las estadísticas de los resultados para cada regla de coincidencia por separado. Puede utilizar como filtro los datos de la regla maestra que desee.  
  
 Para obtener más información sobre cómo funcionan las reglas de coincidencia, vea [Cómo establecer parámetros para las reglas de coincidencia](#MatchingRules).  
  
1.  En la página **Directiva de coincidencia** , haga clic en el icono **Crear una regla de coincidencia** .  
  
2.  Escriba un nombre y una descripción para la regla.  
  
3.  Aumente el valor de **Puntuación de coincidencia mínima** si desea que los requisitos de coincidencia sean más estrictos. Para obtener más información sobre la puntuación de coincidencia mínima, vea [Cómo establecer parámetros para las reglas de coincidencia](#MatchingRules).  
  
4.  Haga clic en el icono **Agregar un nuevo elemento de dominio** .  
  
5.  Seleccione un dominio o dominio compuesto cuyos los valores de regla desea especificar.  
  
    > [!NOTE]  
    >  Puede seleccionar un dominio compuesto solo si cada dominio individual del dominio compuesto tiene asignada una columna de origen.  
  
6.  En **Similitud**, seleccione **Similar** si se puede considerar que los dos valores del mismo campo de dos registros distintos son una coincidencia aunque los valores no sean idénticos. Seleccione **Exacto** si los dos valores del mismo campo de dos registros diferentes deben ser idénticos para que se consideren una coincidencia. (Para obtener más información, consulte [Cómo establecer parámetros para las reglas de coincidencia](#MatchingRules).)  
  
7.  En **Ponderación**, escriba un valor que determina la contribución de la puntuación de coincidencia de un dominio a la puntuación de coincidencia total de dos registros.  
  
    > [!NOTE]  
    >  Cuando se define una ponderación para un dominio compuesto, se puede especificar una ponderación distinta para cada dominio individual del dominio compuesto, en cuyo caso no se asigna una ponderación independiente al dominio compuesto, o se puede especificar una ponderación para el dominio compuesto, en cuyo caso no se asignan ponderaciones distintas a los dominios individuales del dominio compuesto.  
  
8.  Seleccione **Requisito previo** para especificar que los valores del campo de los dos registros deben devolver una coincidencia del 100%; en caso contrario, los registros no se consideran una coincidencia y las demás cláusulas de la regla no se tienen en cuenta. Si **Similitud** es **Similar**, cambiará a **Exacto**, y la ponderación se quitará porque la coincidencia debe ser del 100%.  
  
9. Repita los pasos del 4 al 8 para todos los demás dominios que formarán parte de la regla de coincidencia. Asegúrese de que la suma de las ponderaciones de todos los dominios de la regla es igual a 100.  
  
10. Seleccione **Clústeres superpuestos** en la lista desplegable para mostrar los registros dinámicos y los registros siguientes para todos los clústeres cuando se ejecute la búsqueda de coincidencias, incluso si los grupos de clústeres tienen registros en común. Seleccione **Clústeres no superpuestos** para mostrar, como un solo clúster, los clústeres que tienen registros en común cuando se ejecute la búsqueda de coincidencias.  
  
11. Haga clic en **Volver a cargar los datos del origen** para copiar los datos del origen de datos en la tabla de ensayo y volverlos a indizar cuando se ejecute la directiva de coincidencia. Haga clic en **Ejecutar con los datos anteriores** para ejecutar una directiva de coincidencia sin copiar los datos en la tabla de ensayo ni volver a indizarlos. **Ejecutar con los datos anteriores** aparece deshabilitado la primera vez que se ejecuta la directiva de coincidencia, o si cambia la asignación en la página **Asignación** y, a continuación, presiona **Sí** en el cuadro emergente. En ambos casos, es necesario volver a indizar. No será necesario volver a indizar si la directiva de coincidencia no ha sufrido cambios. La ejecución con los datos anteriores puede mejorar el rendimiento.  
  
12. Haga clic en **Iniciar** para ejecutar el proceso de búsqueda de coincidencias para la regla seleccionada. Cuando finaliza el proceso, la tabla muestra el identificador, el número del clúster y las columnas de datos del registro (incluyendo las que no están en la regla de coincidencia) para cada registro del clúster. La fila dinámica del clúster se considera el candidato principal a permanecer tras el proceso de eliminación de datos duplicados. Cada fila adicional de un clúster se considera un duplicado; su puntuación de coincidencia (comparada con la del registro dinámico) se muestra en la tabla de resultados. El número de clúster es el mismo que el identificador de registro del registro dinámico del clúster.  
  
13. Puede trabajar con los datos de la tabla **Resultados de búsqueda de coincidencias** como sigue:  
  
    -   En **Filtro**, seleccione **Coincidente** para mostrar todas las filas coincidentes y su puntuación. Las filas que no se consideran coincidencias (cuya puntuación de coincidencia es menor que la puntuación de coincidencia mínima) no se muestran en la tabla de resultados de búsqueda de coincidencias. Seleccione **Sin coincidencia** para mostrar todas las filas no coincidentes y no las filas coincidentes.  
  
    -   En el **Cuadro desplegable de porcentaje**, seleccione un porcentaje en la lista desplegable, en incrementos de “5”. Todas las filas cuya puntuación de coincidencia sea mayor o igual que ese porcentaje se mostrarán en la tabla de resultados de búsqueda de coincidencias.  
  
    -   Si hace doble clic en un registro en la tabla de resultados de búsqueda de coincidencias, DQS muestra un cuadro emergente **Detalles de puntuación de coincidencia** que muestra el registro dinámico y el registro de origen (y los valores de todos sus campos), la puntuación entre ellos y una exploración en profundidad de la coincidencia de registros. La exploración en profundidad muestra los valores de cada campo del registro dinámico y del registro de origen para que pueda compararlos, y muestra la puntuación de coincidencia con la que cada campo contribuye a la puntuación de coincidencia total de los dos registros.  
  
14. Vea las estadísticas en la pestaña **Generador de perfiles** y **Resultados de búsqueda de coincidencias** para asegurarse de que ha obtenido los resultados esperados. Para obtener más información, consulte [Pestañas Generador de perfiles y Resultados](#Tabs).  
  
15. Si es necesario cambiar la regla, cámbiela en el Editor de reglas y haga clic en **Reiniciar**.  
  
    > [!NOTE]  
    >  Una vez que se haya completado el primer análisis, el botón **Iniciar** se convertirá en el botón **Reiniciar** . Si los resultados del análisis anterior aún no se han guardado y hace clic en **Reiniciar** , los perderá. Mientras se ejecuta el análisis, no abandone la página o el proceso de análisis se terminará.  
  
16. La pestaña **Resultados de búsqueda de coincidencias** muestra las estadísticas de las dos últimas ejecuciones de la regla. Si ha ejecutado la regla de coincidencia más de una vez con valores distintos, compare las estadísticas de la regla actual y la regla anterior. Si observa que los resultados de la regla anterior eran mejores, haga clic en **Restaurar regla anterior** para restaurar las condiciones de la regla anterior y hacer que la regla recupere el estado que tenía antes de modificarla. Las condiciones actuales de la regla se perderán. Esto le permite ajustar la directiva basándose en las dos últimas ejecuciones y reducir el tiempo empleado en la optimización de la directiva de coincidencia.  
  
17. Si desea agregar otra regla a la directiva de coincidencia, repita el proceso desde el paso 1.  
  
18. Haga clic en **Siguiente** para pasar a la fase de resultados de búsqueda de coincidencias.  
  
##  <a name="MatchingResultsStage"></a> Fase de resultados de búsqueda de coincidencias  
 En la página **Resultados de búsqueda de coincidencias** puede probar todas las reglas de coincidencia juntas. Antes de hacerlo, puede especificar si desea que la ejecución de prueba de la regla identifique clústeres superpuestos o no superpuestos. Si ejecuta las reglas varias veces, puede hacerlo volviendo a cargar los datos desde el origen o con los datos anteriores.  
  
 Cuando se prueban las reglas de coincidencia en la página **Resultados de búsqueda de coincidencias** , se ve una tabla de resultados de coincidencia que muestra los clústeres que DQS ha identificado para todas las reglas. La tabla muestra cada registro del clúster con los valores de los dominios de asignación y la puntuación de coincidencia, junto con el registro dinámico inicial para el clúster. También puede mostrar los datos de generación de perfiles para todas las reglas de coincidencia, las condiciones de cada regla de coincidencia y las estadísticas sobre los resultados de todas las reglas de coincidencia.  
  
1.  En la página **Resultados de búsqueda de coincidencias** , seleccione **Clústeres superpuestos** en la lista desplegable para mostrar los registros dinámicos y los registros siguientes para todos los clústeres cuando se ejecute la búsqueda de coincidencias, incluso si los grupos de clústeres tienen registros en común. Seleccione **Clústeres no superpuestos** para mostrar, como un solo clúster, los clústeres que tienen registros en común cuando se ejecute la búsqueda de coincidencias.  
  
2.  Haga clic en **Volver a cargar los datos del origen** para copiar los datos del origen de datos en la tabla de ensayo y volverlos a indizar cuando se ejecute la directiva de coincidencia. Haga clic en **Ejecutar con los datos anteriores** para ejecutar una directiva de coincidencia sin copiar los datos en la tabla de ensayo ni volver a indizarlos. **Ejecutar con los datos anteriores** aparece deshabilitado la primera vez que se ejecuta la directiva de coincidencia, o si cambia la asignación en la página **Asignación** y, a continuación, presiona **Sí** en el cuadro emergente. En ambos casos, es necesario volver a indizar. No será necesario volver a indizar si la directiva de coincidencia no ha sufrido cambios. La ejecución con los datos anteriores puede mejorar el rendimiento.  
  
3.  Haga clic en **Iniciar** para ejecutar el proceso de búsqueda de coincidencias para todas las reglas que ha definido. La tabla **Resultados de búsqueda de coincidencias** muestra el identificador, el número del clúster y las columnas de datos del registro (incluyendo las que no están en la regla de coincidencia) para cada registro de un clúster. El registro inicial del clúster se selecciona aleatoriamente. (Para determinar el registro que permanece, seleccione la regla de permanencia en la página **Exportar** cuando ejecute el proyecto de búsqueda de coincidencias). Cada fila adicional de un clúster se considera un duplicado; su puntuación de coincidencia (comparada con la del registro dinámico) se muestra en la tabla de resultados.  
  
4.  Puede trabajar con los datos de la tabla **Resultados de búsqueda de coincidencias** como sigue:  
  
    -   En **Filtro**, seleccione **Coincidente** para mostrar todas las filas coincidentes y su puntuación. Las filas que no se consideran coincidencias (cuya puntuación de coincidencia es menor que la puntuación de coincidencia mínima) no se muestran en la tabla de resultados de búsqueda de coincidencias. Seleccione **Sin coincidencia** para mostrar todas las filas no coincidentes y no las filas coincidentes.  
  
    -   En el **Cuadro desplegable de porcentaje**, seleccione un porcentaje en la lista desplegable, en incrementos de “5”. Todas las filas cuya puntuación de coincidencia sea mayor o igual que ese porcentaje se mostrarán en la tabla de resultados de búsqueda de coincidencias.  
  
    -   Si hace doble clic en un registro en la tabla de resultados de búsqueda de coincidencias, DQS muestra un cuadro emergente **Detalles de puntuación de coincidencia** que muestra el registro dinámico y el registro de origen (y los valores de todos sus campos), la puntuación entre ellos y una exploración en profundidad de la coincidencia de registros. La exploración en profundidad muestra los valores de cada campo del registro dinámico y del registro de origen para que pueda compararlos, y muestra la puntuación de coincidencia con la que cada campo contribuye a la puntuación de coincidencia total de los dos registros.  
  
5.  Vea las estadísticas en la pestaña **Generador de perfiles** y **Resultados de búsqueda de coincidencias** para asegurarse de que ha obtenido los resultados esperados. Haga clic en la pestaña **Reglas de coincidencia** para ver cuál es la configuración de dominio para cada regla. Para obtener más información, consulte [Pestañas Generador de perfiles y Resultados](#Tabs).  
  
6.  Si no está satisfecho con los resultados de todas las reglas, haga clic en **Atrás** para volver a la página **Directiva de coincidencia** , modifique una o varias reglas según sea necesario, vuelva a la página **Resultados de búsqueda de coincidencias** y, a continuación, haga clic en **Reiniciar**.  
  
    > [!NOTE]  
    >  Una vez que se haya completado el análisis, el botón **Iniciar** se convertirá en el botón **Reiniciar** . Si los resultados del análisis anterior aún no se han guardado y hace clic en **Reiniciar** , los perderá.  
  
7.  Si está satisfecho con los resultados de todas las reglas, haga clic en **Finalizar** para completar el proceso de directiva de coincidencia y, a continuación, haga clic en una de las opciones siguientes:  
  
    -   **Sí – Publicar la base de conocimiento y salir**: se publicará la base de conocimiento para que pueda utilizarla el usuario actual u otros usuarios. La base de conocimiento no se bloqueará, su estado se establecerá en "vacía" (en la tabla de bases de conocimiento), y las actividades Administración de dominios y Detección de conocimiento estarán disponibles. Volverá a la pantalla Abrir base de conocimiento.  
  
    -   **No – Guardar el trabajo en la base de conocimiento y salir**: se guardarán los cambios realizados, la base de conocimiento permanecerá bloqueada y su estado se establecerá en **Trabajando**. Las actividades Administración de dominios y Detección de conocimiento estarán disponibles. Volverá a la página de inicio.  
  
    -   **Cancelar – Permanecer en la pantalla actual**: se cerrará el cuadro emergente y se volverá a la pantalla Administración de dominios.  
  
8.  Haga clic en **Cerrar** para guardar los cambios realizados y volver a la página de inicio de DQS. El estado de la base de conocimiento mostrará la cadena “Directiva de coincidencia – ” y el estado actual. Si hizo clic en **Cerrar** mientras estaba en la pantalla **Resultados de búsqueda de coincidencias** , el estado mostrará: “Directiva de coincidencia: resultados”. Si hizo clic en Cerrar mientras estaba en la pantalla **Directiva de coincidencia** , el estado mostrará: “Directiva de coincidencia: directiva de coincidencia”. Después de hacer clic en **Cerrar**, para realizar la actividad **Detección de conocimiento** tendría que volver a la actividad **Directiva de coincidencia** , hacer clic en **Finalizar**y, por último, hacer clic en **Sí** para publicar la base de conocimiento o en **No** para guardar el trabajo en la base de conocimiento y salir.  
  
    > [!NOTE]  
    >  Si hace clic en **Cerrar** mientras se está ejecutando un proceso de búsqueda de coincidencias, el proceso de búsqueda de coincidencias no finalizará al hacer clic en **Cerrar**. Puede volver a abrir la base de conocimiento y ver cómo el proceso se sigue ejecutando o, si ha finalizado, comprobar que se muestran los resultados. Si el proceso no ha finalizado, la pantalla mostrará el progreso.  
  
9. Haga clic en **Cancelar** para finalizar la actividad Directiva de coincidencia, perdiendo los cambios realizados, y volver a la página de inicio de DQS.  
  
##  <a name="FollowUp"></a> Seguimiento: después de crear una directiva de coincidencia  
 Después de crear una directiva de coincidencia, puede ejecutar un proyecto de búsqueda de coincidencias basándose en la base de conocimiento que contiene la directiva de coincidencia. Para obtener más información, consulte [Ejecutar un proyecto de coincidencia](../data-quality-services/run-a-matching-project.md).  
  
##  <a name="Tabs"></a> Pestañas Generador de perfiles y Resultados  
 Las pestañas Generador de perfiles y Resultados contienen estadísticas para las páginas Directiva de coincidencia y Resultados de búsqueda de coincidencias.  
  
###  <a name="Profiler"></a> Pestaña Generador de perfiles  
 Haga clic en la pestaña **Generador de perfiles** para mostrar las estadísticas de la base de datos de origen y de cada campo de la regla de directiva. Las estadísticas se actualizarán mientras se ejecuta la regla de directiva.  
  
 Para obtener más información sobre cómo interpretar las estadísticas siguientes, vea [Cómo establecer parámetros para las reglas de coincidencia](#MatchingRules).  
  
 Las estadísticas de la base de datos de origen incluyen:  
  
-   **Registros**: el número total de registros existentes en la base de datos de origen  
  
-   **Valores totales**: el número total de valores existentes en los campos del origen de datos  
  
-   **Nuevos valores**: el número total de valores que son nuevos desde la ejecución anterior y su porcentaje del total  
  
-   **Valores únicos**: el número total de valores únicos existentes en los campos y su porcentaje del total  
  
-   **Nuevos valores únicos**: el número total de valores únicos que son nuevos en los campos y su porcentaje del total  
  
 Las estadísticas del campo incluyen las siguientes:  
  
-   **Nombre de campo**  
  
-   **Nombre del dominio**  
  
-   **Nuevo**: el número de valores nuevos y el porcentaje de estos comparado con los valores existentes en el dominio  
  
-   **Único**: el número de registros únicos del campo y su porcentaje sobre el total  
  
-   **Integridad**: la integridad de cada campo de origen que se ha asignado para el ejercicio de búsqueda de coincidencias  
  
###  <a name="Notifications"></a> Notificaciones de directiva de coincidencia  
 En la actividad de directiva de coincidencia, se producen notificaciones cuando se dan las condiciones siguientes:  
  
-   El campo está vacío en todos los registros; se recomienda eliminarlo de la asignación.  
  
-   La puntuación de integridad del campo es muy baja; puede que desee eliminarlo de la asignación.  
  
-   Ninguno de los valores de un campo es válido; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
-   Hay un nivel bajo de valores válidos en el campo; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
-   Existe un alto grado de singularidad en el campo. El uso de este campo en la directiva de coincidencia puede disminuir los resultados de búsqueda de coincidencias.  
  
###  <a name="ResultsTab"></a> Pestaña Resultados de búsqueda de coincidencias  
 Haga clic en la pestaña **Resultados de búsqueda de coincidencias** para mostrar las estadísticas para la ejecución de la regla de directiva de coincidencia y la ejecución anterior de la regla. Si ha ejecutado la misma regla más de una vez con parámetros diferentes, la tabla de resultados de búsqueda de coincidencias mostrará las estadísticas para ambas ejecuciones, lo que le permitirá compararlas. También puede restaurar la regla anterior si lo desea.  
  
 Las estadísticas incluyen:  
  
-   El número total de registros existentes en la base de datos  
  
-   El número total de registros coincidentes existentes en la base de datos  
  
-   El número de registros existentes en la base de datos que no se consideran duplicados  
  
-   El número de clústeres descubiertos  
  
-   El promedio de tamaño de clúster (el número de registros duplicados dividido por el número de clústeres)  
  
-   El menor número de duplicados existentes en un clúster  
  
-   El mayor número de duplicados existentes en un clúster  
  
  

