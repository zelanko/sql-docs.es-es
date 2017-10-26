---
title: "Realizar la detección de conocimiento | Microsoft Docs"
ms.custom: 
ms.date: 06/04/2013
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.kb.kbterms.f1
- sql13.dqs.kb.viewselectcd.f1
- sql13.dqs.kb.kbanalyze.f1
- sql13.dqs.kb.kbmap.f1
ms.assetid: 34a0ea16-02e6-46ed-90bc-dede68687f63
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4b98bfc1ffb87a23817ce01380de2f62113e4748
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="perform-knowledge-discovery"></a>Realizar la detección de conocimiento
  En este tema se describe cómo crear una base de conocimiento mediante la detección de conocimiento. Durante el proceso de detección, [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) analiza los datos de un origen de datos de ejemplo mediante un proceso asistido por PC, y agrega el conocimiento adquirido a la base de conocimiento. Este conocimiento se puede modificar y mejorar en el paso **Administrar valores del dominio** de la actividad de detección de conocimiento, o en la actividad de administración de dominios.  
  
 La detección de conocimiento es un proceso asistido por PC que consta de tres pasos que deben completarse obligatoriamente.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Es necesario tener instalado Microsoft Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] si los datos de origen en los que se ejecuta la detección están en un archivo de Excel. De lo contrario, no podrá seleccionar dicho archivo en la fase de asignación. Los archivos creados por Microsoft Excel pueden tener la extensión .xlsx, .xls o .csv. Si se utiliza la versión de 64 bits de Excel, solo se admitirán los archivos de Excel 2003 (.xls); los archivos de Excel 2007 o 2010 (.xlsx) no son compatibles. Si utiliza la versión de 64 bits de Excel 2007 o 2010, guarde el archivo como un archivo .xls o .csv, o instale una versión de 32 bits de Excel en su lugar.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para crear una base de conocimiento, debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="FirstStep"></a> Primer paso: iniciar la detección de conocimiento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Si desea realizar la detección de conocimiento en una nueva base de conocimiento, haga clic en **Nueva base de conocimiento**, escriba el nombre y la descripción, y especifique en qué basará la base de conocimiento, si procede. Si desea realizar la detección de conocimiento en una base de conocimiento existente, haga clic en **Abrir base de conocimiento**y, a continuación, seleccione una base de conocimiento.  
  
3.  Seleccione **Detección de conocimiento** como actividad y, a continuación, haga clic en **Crear** para crear la nueva base de conocimiento o en **Abrir** para abrir una ya existente.  
  
##  <a name="Mapping"></a> Fase de asignación  
  
1.  En el campo **Origen de datos** , seleccione **SQL Server** (el valor predeterminado) o **Archivo de Excel**.  
  
    > [!NOTE]  
    >  En esta página, podrá realizar una conexión con un origen de datos de SQL Server o de Excel, y después realizar la asignación entre cada las columnas del origen de datos y los dominios de la base de conocimiento. La tabla Asignaciones muestra todas las columnas de la base de datos de origen que se analizarán para agregar conocimiento a los dominios correspondientes. Cada asignación se realiza entre una de las columnas del origen de datos y un dominio de la base de conocimiento.  
  
2.  Si el origen de datos es **SQL Server**, haga lo siguiente:  
  
    1.  En el campo **Base de datos** , seleccione la base de datos de origen que desea analizar para crear la base de conocimiento. El cuadro de texto desplegable mostrará las bases de datos disponibles. La base de datos de origen debe encontrarse en la misma instancia de SQL Server que [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. En caso contrario, no aparecerá en la lista desplegable.  
  
    2.  En el campo **Tabla/vista** , seleccione la tabla o vista que desea analizar para crear la base de conocimiento. Esta tabla o vista debe estar formada por datos de ejemplo, no por una base de datos de origen completa en la que esté realizando operaciones de limpieza o de búsqueda de coincidencias. El cuadro de texto desplegable mostrará las tablas y vistas disponibles para la base de datos seleccionada.  
  
3.  Si el origen de datos es **Excel**, haga lo siguiente:  
  
    1.  Haga clic en **Examinar** y seleccione el archivo de Excel que desea analizar para crear la base de conocimiento. Es necesario tener instalado Excel en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para seleccionar un archivo de Excel. Si Excel no está instalado en el equipo de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , el botón Examinar no estará disponible, y aparecerá una notificación debajo de este cuadro de texto indicándole que Excel no está instalado.  
  
    2.  Active la casilla **Usar la primera fila como encabezado** si la primera fila del archivo de Excel contiene datos de encabezado.  
  
4.  En la tabla **Asignaciones** , asigne cada una de las columnas de origen en las que desea realizar la detección de conocimiento a un dominio de la base de conocimiento, de la manera siguiente:  
  
    1.  Para crear una asignación, seleccione una columna de origen en la lista desplegable de la columna **Columna de origen** de una fila vacía y, a continuación, seleccione un dominio (si lo hay) en la lista desplegable de la columna **Dominio** de la misma fila. Si no existe ningún dominio, haga clic en **Crear un dominio** o en **Crear un dominio compuesto** para crear uno. Para obtener más información, consulte [Create a Domain Rule](../data-quality-services/create-a-domain-rule.md) o [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md).  
  
    2.  Repita el paso anterior para cada asignación. Para cambiar el número de filas de la tabla, haga clic en **Agregar una asignación de columna**, o seleccione una fila y haga clic en **Quitar la asignación de columna seleccionada**. Si hace clic en **Quitar la asignación de columna seleccionada** cuando está seleccionada una fila rellena, la fila seleccionada se eliminará aunque haya una fila vacía.  
  
        > [!NOTE]  
        >  Solo puede asignar los datos de origen para un dominio DQS a fin de realizar la detección de conocimiento si el tipo de datos de origen se admiten en DQS y coincide con el tipo de datos de dominio DQS. Para obtener más información acerca de los tipos de datos admitidos, vea [Supported SQL Server and SSIS Data Types for DQS Domains](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
    3.  Haga clic en **Ver o seleccionar dominios compuestos** para mostrar los dominios compuestos definidos. Si no se ha definido ningún dominio compuesto, el control no estará disponible.  
  
    4.  Haga clic en **Vista previa del origen de datos** para mostrar en un cuadro emergente todos los datos del origen de datos que ha seleccionado en el cuadro de texto **Tabla/vista** o **Archivo de Excel** .  
  
5.  Haga clic en **Siguiente** para continuar en la página **Detectar** del Asistente para la detección de conocimiento. También puede seleccionar lo siguiente:  
  
    -   Haga clic en **Cancelar** para terminar la actividad Detección de conocimiento, perdiendo los cambios realizados, y volver a la página de inicio de DQS.  
  
    -   Haga clic en **Cerrar** para guardar los cambios realizados y volver a la página de inicio de DQS. La base de conocimiento se bloqueará, y su estado en la tabla de bases de conocimiento de la pantalla **Abrir base de conocimiento** será **Detección de conocimiento: asignar**. Para realizar la actividad Administración de dominios, después de hacer clic en **Cerrar**, tendría que hacer clic en **Detección de conocimiento** en la pantalla **Abrir base de conocimiento** , continuar en la pantalla **Administración de la base de conocimiento: administrar términos del dominio** , hacer clic en **Finalizar**y, por último, hacer clic en **Sí** para publicar la base de conocimiento o en **No** para guardar el trabajo en la base de conocimiento y salir.  
  
##  <a name="Discover"></a> Fase de detección  
  
1.  Haga clic en **Iniciar** para analizar el origen de datos.  
  
    > [!NOTE]  
    >  La detección se realiza en las columnas especificadas en la tabla **Asignaciones** de la página **Asignación** . El dominio asignado a cada columna se rellenará con el conocimiento extraído de la detección. Si el dominio es un dominio compuesto, el conocimiento se agregará a los dominios individuales que lo forman.  
  
2.  Mientras se ejecuta el proceso de detección, compruebe el estado de finalización mostrado para cada paso de la detección: **Procesamiento previo de registros**, **Se están ejecutando las reglas de dominio**y **Se está ejecutando la detección**. Se mostrará tanto el porcentaje completado como el estado de finalización para cada una de estas fases.  
  
3.  Una vez completado el análisis, compruebe que la línea de estado situada debajo de las estadísticas de finalización indica que ha finalizado correctamente.  
  
    > [!NOTE]  
    >  Si abandona la pantalla antes de que se cargue el archivo, el proceso de carga del archivo terminará.  
  
4.  Una vez completado el análisis, compruebe las estadísticas de la pestaña **Generador de perfiles** para ver el estado de los datos. Para obtener más información, vea **Generación de perfiles de datos y notificaciones de DQS**.  
  
5.  Una vez que se haya completado el análisis, el botón **Iniciar** se convertirá en el botón **Reiniciar** . Haga clic en **Reiniciar** para ejecutar de nuevo el proceso de análisis. Sin embargo, tenga en cuenta que los resultados del análisis anterior aún no se han guardado, por lo que, si hace clic en **Reiniciar** , los perderá. Para continuar, haga clic en **Sí** en el cuadro emergente. Mientras se ejecuta el análisis, no abandone la página o el proceso de análisis se terminará.  
  
6.  Haga clic en **Siguiente** para continuar en la página **Administrar valores del dominio** del Asistente para la detección de conocimiento. En esta página podrá modificar el conocimiento agregado a los dominios de la base de conocimiento. También puede seleccionar lo siguiente:  
  
    -   Haga clic en **Cancelar** para terminar la actividad Detección de conocimiento, perdiendo los cambios realizados, y volver a la página de inicio de DQS.  
  
    -   Haga clic en **Cerrar** para guardar los cambios realizados y volver a la página de inicio de DQS. La base de conocimiento se bloqueará y su estado en la tabla de bases de conocimiento de la pantalla **Abrir base de conocimiento** será **Detección – Detectar**. Para realizar la actividad Administración de dominios, después de hacer clic en **Cerrar**, tendría que hacer clic en **Detección de conocimiento** en la pantalla **Abrir base de conocimiento** , continuar en la pantalla **Administración de la base de conocimiento: administrar términos del dominio** , hacer clic en **Finalizar**y, por último, hacer clic en **Sí** para publicar la base de conocimiento o en **No** para guardar el trabajo en la base de conocimiento y salir.  
  
    -   Haga clic en esta opción para volver a la página **Detectar** .  
  
##  <a name="Manage"></a> Fase de administración de resultados de la detección de datos  
 Después de realizar la actividad de detección de conocimiento, puede cambiar los valores realizando las acciones siguientes:  
  
-   Agregar un valor de dominio a la lista de valores, o seleccionar un valor y eliminarlo de la lista  
  
-   Cambiar a correcto, erróneo o no válido el estado asignado a un valor de dominio por el proceso de detección de DQS  
  
-   Especificar un valor de reemplazo para un valor erróneo o no válido  
  
-   Establecer dos o más valores como sinónimos y cambiar el valor inicial definido por el proceso de detección, con lo que el valor inicial reemplazará el valor del sinónimo si se estableció la propiedad **Usar valores iniciales** al crear el dominio  
  
-   Importar valores de dominio desde un archivo de Excel.  
  
 La tabla **Valor** muestra el conocimiento agregado a la base de conocimiento para un dominio individual. Puede seleccionar dicho dominio en la lista de dominios que aparece en el panel de la izquierda. Las columnas del campo son las siguientes:  
  
-   La columna **Valor** muestra todos los valores que el proceso de detección agregó al dominio seleccionado desde un campo de la muestra de datos. Cualquier valor proyectado como erróneo se mostrará como sinónimo de un valor proyectado como correcto.  
  
-   La columna **Frecuencia** muestra el número de instancias del valor del campo de la base de datos de ejemplo a las que se ha asignado el dominio. En un dominio compuesto, solo aquellos valores con una frecuencia mayor o igual que 20 se muestran. Los datos de frecuencia están disponibles porque el proceso de detección de conocimiento todavía tiene una conexión con la base de datos de muestra. Los datos de frecuencia no están disponibles en la tabla de dominios de la pestaña Valores del dominio de la pantalla Administración de dominios porque el proceso de administración de dominios no tiene conexión con la base de datos de muestra.  
  
-   La columna **Tipo** muestra el estado del valor, tal como lo determina el proceso de detección. Una marca verde indica que el valor es correcto o se ha corregido; una cruz roja indica que el valor es erróneo; un triángulo naranja con un signo de exclamación indica que el valor no es válido. Un valor que no es válido no cumple los requisitos de los datos para el dominio. Un valor erróneo puede ser válido, pero no es el valor correcto a causa de los datos.  
  
-   La columna **Corregir a** muestra el valor correcto por el que se cambiará el valor original, marcado como erróneo o no válido. DQS puede proponer el valor correcto como resultado del proceso de detección.  
  
 Administre los resultados de la detección de la manera siguiente:  
  
1.  En el panel **Lista de dominios** de la izquierda, seleccione el dominio para el que desea establecer los valores de dominio. Puede hacer lo siguiente para modificar los valores mostrados.  
  
    -   Mostrar los resultados que desea en la tabla, en función de su estado, seleccionando este en la lista **Filtro** .  
  
    -   Buscar los datos que desea comprobar o modificar especificando las letras que desea buscar en el cuadro de texto Buscar. Esto resaltará dichas letras dondequiera que aparezcan en los valores mostrados.  
  
    -   Haga clic en **Mostrar solo nuevo** para restringir los valores mostrados en la tabla a aquellos que se detectaron en la sesión actual, no en las sesiones anteriores.  
  
    -   Haga clic en el botón **Expandir todo** para mostrar todos los valores de todos los grupos de sinónimos si el estado actual es Contraído, o en el botón **Contraer todo** para ocultar todos los valores excepto el inicial en todos los grupos de sinónimos si el estado actual es Expandido.  
  
    -   Haga clic en el botón **Mostrar/Ocultar el panel de historial de cambios de valores de dominio** para mostrar una vista previa emergente en la parte inferior de la tabla de valores con los cambios recientes en la colección de valores de dominio.  
  
2.  Busque las correcciones que haya propuesto Data Quality Services; para ello, establezca **Filtro** en **Error**. Compruebe que el valor es realmente erróneo y que el valor de la columna **Corregir a** es el apropiado.  
  
3.  Establezca **Filtro** en **Todos los valores** y compruebe que el estado de los valores es el adecuado. Para cambiar el estado de un valor, seleccione este y haga clic en el botón **Establecer como corregidos los valores de dominio seleccionados** (marca de comprobación), **Establecer como errores los valores de dominio seleccionados** (cruz) o **Establecer como no válidos los valores de dominio seleccionados** (triángulo).  
  
4.  Para cambiar el estado de un valor, haga lo siguiente:  
  
    1.  **Establecer como corregidos los valores de dominio seleccionados**: para cambiar el estado de un valor de Error o No válido a Correcto, seleccione el valor y, a continuación, haga clic en el icono **Establecer como corregidos los valores de dominio seleccionados** (marca de comprobación) en la flecha hacia abajo de la barra de iconos o en la lista desplegable Tipo. Si el valor erróneo o no válido está agrupado con un valor correcto, elimine ese valor después de la operación.  
  
    2.  **Establecer como errores los valores de dominio seleccionados**: para cambiar el estado de un valor de Correcto o No válido a Error, seleccione el valor y, a continuación, haga clic en el icono **Establecer como errores los valores de dominio seleccionados** (cruz) en la flecha hacia abajo de la barra de iconos o en la lista desplegable Tipo. Si lo desea, puede escribir una corrección en la columna **Corregir a** , o dejarla en blanco.  
  
    3.  **Establecer como no válidos los valores de dominio seleccionados**: para cambiar el estado de un valor de Correcto o Error a No válido, seleccione el valor y, a continuación, haga clic en el icono **Establecer como no válidos los valores de dominio seleccionados** (triángulo) en la flecha hacia abajo de la barra de iconos o en la lista desplegable Tipo. Si lo desea, puede escribir una corrección en la columna **Corregir a** , o dejarla en blanco.  
  
    4.  **Corregir a**: después de establecer un valor como erróneo o no válido, escriba un nuevo valor en la columna **Corregir a** . DQS agregará una nueva fila para el valor de reemplazo, lo designará como correcto y, a continuación, agrupará los dos valores. El nuevo valor se mostrará como el valor inicial, con el valor inicial en negrita y el valor erróneo o no válido con una sangría aplicada.  
  
5.  Para designar valores como un grupo de sinónimos, seleccione varios valores que sean correctos y haga lo siguiente:  
  
    -   **Establecer como sinónimos los valores de dominio seleccionados**: haga clic aquí para establecer los valores seleccionados como sinónimos. DQS designará uno de los valores como el valor inicial con el que se reemplazarán los otros.  
  
        > [!NOTE]  
        >  Si selecciona dos o más valores de un grupo y otro valor fuera de este y, a continuación, los establece como sinónimos, obtendrá un mensaje de error. Después de cerrar el cuadro emergente del mensaje de error, los valores se establecerán correctamente como sinónimos.  
  
    -   **Romper la relación entre los sinónimos seleccionados**: haga clic aquí para deshacer la designación de sinónimos.  
  
    -   **Establecer el valor de dominio seleccionado como valor principal de su grupo**: para cambiar el valor inicial del grupo, seleccione un valor de este que no se haya designado como valor inicial y, a continuación, haga clic en el botón **Establecer el valor de dominio seleccionado como valor principal de su grupo** .  
  
6.  **Corrector ortográfico**: si ha habilitado el corrector ortográfico en la página Propiedades de dominio, busque los valores que aparezcan subrayados con una línea ondulada de color rojo, lo que indicará que el corrector ortográfico sugiere una corrección. Haga clic con el botón secundario en el valor subrayado y seleccione una corrección si es necesario. El tipo de valor pasará a ser (o permanecerá como) erróneo, y la corrección se agregará a la columna **Corregir a** . Haga clic en la flecha abajo para ver correcciones propuestas adicionales. Escriba manualmente una corrección para agregarla al diccionario del corrector ortográfico y poder seleccionarla como corrección. Para obtener más información, consulte [Use the DQS Speller](../data-quality-services/use-the-dqs-speller.md) y [Set Domain Properties](../data-quality-services/set-domain-properties.md).  
  
    > [!NOTE]  
    >  Para utilizar el corrector ortográfico, puede habilitarlo en la página **Propiedades del dominio** o, si está deshabilitado en la página **Propiedades del dominio** , puede hacer clic en el icono **Habilitar o deshabilitar el corrector ortográfico** de la página **Administrar resultados de detección de datos** para habilitarlo en esta página.  
  
7.  **Agregar un nuevo valor de dominio**: para agregar un nuevo valor al dominio, haga clic en el botón **Agregar un nuevo valor de dominio** para agregar una fila al final de la tabla. Después de agregar un valor, la fila se colocará de nuevo en orden alfabético.  
  
8.  **Importar valores de dominio de Excel**: para agregar nuevos valores desde una hoja de cálculo de Excel, haga clic en la flecha abajo del icono **Importar valores** y, a continuación, seleccione **Importar valores de dominio de Excel**. Escriba el nombre del archivo, seleccione **Usar la primera fila como encabezado** si procede y, a continuación, haga clic en **Aceptar**. Para obtener más información, consulte [Import Values from an Excel File into a Domain](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md).  
  
9. **Importar valores de proyecto**: para agregar nuevos valores desde un proyecto de calidad de datos, haga clic en la flecha abajo del icono **Importar valores** y, a continuación, seleccione **Importar valores de proyecto**. Escriba el nombre del archivo, seleccione **Usar la primera fila como encabezado** si procede y, a continuación, haga clic en **Aceptar**. Seleccione el proyecto del que desee importar los valores y, a continuación, haga clic en **Aceptar**. Se mostrarán los valores importados. Haga clic en **Finalizar**. Para obtener más información, vea Importar valores de un proyecto de limpieza en un dominio.  
  
10. **Eliminar los valores de dominio seleccionados**: para quitar uno o varios valores del dominio, selecciónelos y haga clic en el botón **Eliminar los valores de dominio seleccionados** . Las entradas de DQS_NULL no se pueden eliminar, por lo que si opta por eliminar varios valores entre los que hay una de estas entradas, se producirá un error en la operación.  
  
11. Haga clic en **Finalizar** para completar la actividad de detección de conocimiento. Se mostrará un cuadro emergente si no ha revisado cada uno de los dominios. Haga clic en **Sí** para seguir con la revisión o en **No** para continuar. Si hace clic en No, aparecerá un cuadro emergente con las opciones siguientes:  
  
    1.  **Publicar**: se publicará la base de conocimiento para que pueda utilizarla el usuario actual u otros usuarios. La base de conocimiento no se bloqueará, su estado se establecerá en "vacía" (en la tabla de bases de conocimiento), y las actividades Administración de dominios y Detección de conocimiento estarán disponibles. Volverá a la página de inicio. Para completar el proceso, haga clic en **Sí** en el menú emergente.  
  
    2.  **No**: se guardarán los cambios realizados, la base de conocimiento permanecerá bloqueada y su estado se establecerá en Trabajando. Las actividades Administración de dominios y Detección de conocimiento estarán disponibles. Volverá a la página de inicio.  
  
    3.  **Cancelar**: se cerrará el cuadro emergente y permanecerá en la página **Administrar valores del dominio** .  
  
12. También puede hacer clic en las opciones siguientes:  
  
    -   **Cancelar** para terminar la actividad Detección de conocimiento, perder los cambios realizados y volver a la página de inicio de DQS.  
  
    -   **Cerrar** para guardar los cambios realizados y volver a la página de inicio de DQS. La base de conocimiento se bloqueará, y su estado en la tabla de bases de conocimiento de la pantalla **Abrir base de conocimiento** será **Detección – Administración de valores**.  
  
    -   Haga clic en **Atrás** para volver a la página **Detectar** . Para realizar la actividad Administración de dominios, después de hacer clic en **Cerrar**, tendría que hacer clic en **Detección de conocimiento** en la pantalla **Abrir base de conocimiento** , continuar en la pantalla **Administración de la base de conocimiento: administrar términos del dominio** , hacer clic en **Finalizar**y, por último, hacer clic en **Sí** para publicar la base de conocimiento o en **No** para guardar el trabajo en la base de conocimiento y salir.  
  
##  <a name="FollowUp"></a> Seguimiento: después de realizar la detección de conocimiento  
 Una vez agregado el conocimiento a la base de conocimiento durante el proceso de detección de conocimiento asistido por PC, puede utilizar la base de conocimiento para un proyecto de limpieza de forma inmediata, o puede realizar antes la administración de dominios. Para más información sobre la limpieza de datos o la administración de dominios, vea [Limpieza de datos](../data-quality-services/data-cleansing.md) o [Administrar un dominio](../data-quality-services/managing-a-domain.md).  
  
##  <a name="Meaning"></a> El significado de los valores Correcto, Error y No válido  
 A cada valor de la tabla **Valor** de la página **Valores del dominio** se le asigna un **Tipo** : **Correcto**, **Error**o **No válido**. La actividad de detección de conocimiento es la que genera inicialmente el tipo del valor, y puede cambiarlo de acuerdo con sus necesidades. La actividad de limpieza es la que genera el tipo final, en función de los cambios interactivos y de detección. Estos valores tienen los significados siguientes:  
  
-   **Correcto:** es un valor que pertenece al dominio y no tiene ningún error de sintaxis. Por ejemplo, “Chicago” en un dominio City es un valor correcto.  
  
-   **Error:** es un valor que pertenece al dominio, pero es incorrecto. Por ejemplo, “Shicago” en lugar de “Chicago” en un dominio City es un valor erróneo. DQS designa un valor como erróneo si detecta un error de sintaxis y una corrección asociada en el proceso de detección. Los errores de sintaxis incluyen los errores de ortografía.  
  
-   **No válido:** es un valor que no pertenece al dominio y que no tiene una corrección. Por ejemplo, el valor “12345" en un dominio City es un valor no válido. DQS designa un valor como no válido cuando no cumple una regla de dominio.  
  
 Puede cambiar manualmente el tipo de un valor a cualquiera de los otros dos valores. DQS no aplica la semántica de errores y de validez en las operaciones manuales. Puede especificar una corrección para un valor no válido sin cambiar su estado. Puede designar un valor como no válido aunque haya cumplido las reglas de dominio. Puede designar un valor como erróneo aunque el proceso de detección no haya indicado que tiene un error de sintaxis. También puede quitar una corrección de un valor de error, que está marcado como correcto, sin cambiar su estado.  
  
 Cuando se realiza la limpieza de datos interactiva en la página **Administrar y ver resultados** de la actividad **Limpieza** , tanto los valores no válidos como los erróneos se incluyen en la pestaña **No válido** de la página **Administrar y ver resultados** .  
  
##  <a name="Display"></a> How to Display the Appropriate Values  
 Puede modificar la presentación de la manera siguiente:  
  
-   **Filtre** los resultados que desea en la tabla, en función de su estado, seleccionando este en la lista desplegable **Filtro** .  
  
-   **Busque** los datos que desea comprobar o modificar especificando las letras que desea buscar en el cuadro de texto **Buscar** . Esto resaltará dichas letras dondequiera que aparezcan en los valores mostrados.  
  
-   Haga clic en **Mostrar solo nuevo** para restringir los valores mostrados en la tabla a aquellos que se detectaron en la sesión actual, no en las sesiones anteriores.  
  
-   Haga clic en el botón **Expandir todo** para mostrar todos los valores de los grupos de sinónimos cuando el estado actual es Contraído.  
  
-   Haga clic en el botón **Contraer todo** para ocultar todos los valores excepto el inicial en los grupos de sinónimos cuando el estado actual es Expandido.  
  
-   Haga clic en el botón **Mostrar/Ocultar el panel de historial de cambios de valores de dominio** para mostrar una vista previa emergente en la parte inferior de la tabla de valores con los cambios recientes en la colección de valores de dominio.  
  
##  <a name="Profiler"></a> Estadísticas del generador de perfiles  
 La pestaña Generador de perfiles proporciona estadísticas que indican la calidad de los datos de origen. Estas estadísticas no miden la calidad de la base de conocimiento. La generación de perfiles en la detección de conocimiento proporciona nuevas perspectivas sobre la integridad y la unicidad. La generación de perfiles en la detección de conocimiento no mide la precisión. La generación de perfiles para la administración del conocimiento le ayuda a evaluar hasta qué punto el origen de datos es importante para generar y mejorar el conocimiento de una base de conocimiento.  
  
 La pestaña **Generador de perfiles** proporciona las estadísticas siguientes para el proceso de detección, por campo y dominio:  
  
-   **Registros**: el número de registros que se han detectado en la muestra de datos  
  
-   **Valores totales**: el número de valores totales que se encontraron para cada campo y en total  
  
-   **Nuevos valores**: el número de valores totales para cada campo y para todos los campos asignados que son nuevos desde el último proceso de detección, y su porcentaje sobre los valores totales  
  
-   **Valores únicos**: el número de valores totales para cada campo y para todos los campos asignados que son únicos, y su porcentaje sobre los valores totales  
  
-   **Nuevos valores únicos**: el número de valores únicos para cada campo y para todos los campos asignados que son nuevos desde el último proceso de detección, y su porcentaje sobre los valores totales  
  
-   **Válido en valores de dominio**: el número de valores totales para cada campo y para todos los campos asignados que son válidos, y su porcentaje sobre los valores totales  
  
 Las estadísticas del campo incluyen las siguientes:  
  
-   **Campo**: nombre del campo de la base de datos de origen  
  
-   **Dominio**: nombre del dominio que se asigna al campo  
  
-   **Nuevo:**: el número de valores nuevos y el porcentaje de estos comparado con los valores existentes en el campo  
  
-   **Único**: el número de registros únicos del campo y su porcentaje sobre el total  
  
-   **Válido en el dominio**: el número de valores de dominio que son válidos y su porcentaje sobre el total  
  
-   **Integridad**: la integridad de cada campo de origen que se ha asignado para el ejercicio de búsqueda de coincidencias  
  
 La generación de perfiles en la detección de conocimiento proporciona nuevas perspectivas sobre la integridad. Si la generación de perfiles le indica que un campo está relativamente incompleto, puede que desee quitarlo de la base de conocimiento de un proyecto de calidad de datos. La generación de perfiles no puede proporcionar estadísticas de integridad confiables para los dominios compuestos. Si necesita estadísticas de integridad, utilice dominios individuales en lugar de dominios compuestos. Si desea utilizar dominios compuestos, puede crear una base de conocimiento con dominios individuales para generar los perfiles y determinar la integridad, y crear otro dominio con un dominio compuesto para el proceso de limpieza. Por ejemplo, la generación de perfiles podría mostrar una integridad del 95% para los registros de direcciones utilizando un dominio compuesto, pero podría haber un nivel mucho más alto de falta de integridad en una de las columnas, por ejemplo, una columna de código postal (zip). En este ejemplo, podría medir la integridad de la columna de código postal con un dominio individual. La generación de perfiles probablemente proporcione estadísticas precisas y confiables para los dominios compuestos porque permite medir la precisión de varias columnas al mismo tiempo. El valor de estos datos está en la agregación compuesta, por lo que puede ser conveniente medir la precisión con un dominio compuesto.  
  
 Las estadísticas se muestran en la pestaña Generador de perfiles en las fases siguientes:  
  
-   En la fase **Procesamiento previo de registros** , DQS carga los datos y los indiza. Esto se realiza registro por registro o lote por lote, de modo que los registros puedan mostrar el progreso. Durante la ejecución de este paso, es posible generar la mayoría de los datos de generación de perfiles, salvo los valores **Válido en el dominio** .  
  
-   En la fase **Se están ejecutando las reglas de dominio** , se rellena la columna **Válido en el dominio** mientras todas las reglas de dominio se ejecutan como una unidad atómica de cada valor de dominio.  
  
-   En la fase **Se está ejecutando la detección** , no se actualiza ningún nuevo dato en la pestaña Generador de perfiles. Los errores de sintaxis encontrados se pueden ver en el paso siguiente del asistente, la fase **Administrar valores del dominio**.  
  
 En la actividad de detección de conocimiento, las condiciones siguientes producen notificaciones:  
  
-   No existen nuevos valores en un campo; se recomienda eliminarlo de la asignación.  
  
-   Hay pocos valores nuevos en un campo; es posible que desee eliminarlo de la asignación.  
  
-   Un campo está vacío; se recomienda eliminarlo de la asignación.  
  
-   La puntuación de integridad del campo es muy baja; puede que desee eliminarlo de la asignación.  
  
-   Ninguno de los valores de un campo es válido; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
-   Hay un nivel bajo de valores válidos en el campo; debe comprobar la asignación y la pertinencia de las reglas de dominio para el contenido del campo.  
  
 Para obtener más información sobre la generación de perfiles, vea [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  

