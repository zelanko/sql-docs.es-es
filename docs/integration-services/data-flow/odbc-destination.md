---
title: Destino ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 153cbd447fa84087b50501005d0ea457f47d1eda
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298212"
---
# <a name="odbc-destination"></a>Destino ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El destino ODBC carga de forma masiva los datos en tablas de base de datos que admiten ODBC. El destino ODBC usa un administrador de conexiones ODBC para conectarse al origen de datos.  
  
 Un destino ODBC incluye asignaciones entre las columnas de entrada y las columnas en el origen de datos de destino. No es necesario asignar columnas de entrada a todas las columnas de destino pero, según las propiedades de las columnas de destino, pueden producirse errores si no se asignan columnas de entrada a las columnas de destino. Por ejemplo, si una columna de destino no permite valores NULL, se debe asignar una columna de entrada a esa columna. Además, se pueden asignar columnas de tipos diferentes, sin embargo, si los datos de entrada no son compatibles con el tipo de las columnas de destino, se produce un error en tiempo de ejecución. En función de la opción de comportamiento del error, se omitirá el error, se producirá un error o la fila se enviará a la salida de error.  
  
 El destino ODBC tiene una salida normal y una salida de error.  
  
##  <a name="load-options"></a><a name="BKMK_odbcdestination_loadoptions"></a> Opciones de carga  
 El destino ODBC puede usar uno de dos módulos de de carga de acceso. Establezca el modo en el [Editor de orígenes ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md). Los dos modos son:  
  
-   **Lote**: en este modo, el destino ODBC intenta usar el método más eficaz de inserción en función de las capacidades del proveedor ODBC percibidas. Para la mayoría de los proveedores ODBC modernos, esto significaría preparar una instrucción INSERT con parámetros y usar después un enlace de parámetros de matriz en las filas (donde el tamaño de la matriz está controlado por la propiedad **BatchSize** ). Si selecciona **Lote** y el proveedor no admite este método, el destino ODBC cambia automáticamente los modificadores al modo **Fila a fila** .  
  
-   **Fila a fila**: en este modo, el destino ODBC prepara una instrucción INSERT con parámetros y usa **Execute de SQL** para insertar las filas de una en una.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El destino ODBC tiene una salida de error. La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: número que corresponde al error actual. Vea la documentación de la base de datos de origen para obtener una lista de errores. Para obtener una lista de códigos de errores de SSIS, vea la referencia Código de errores y mensajes de SSIS.  
  
-   **Columna de error**: columna de origen que produce el error (para los errores de conversión).  
  
-   Columnas estándar de datos de salida.  
  
 Según la configuración del comportamiento de los errores, el destino ODBC permite devolver los errores (conversión de datos, truncamiento) que aparecerán durante el proceso de extracción en la salida de error. Para obtener más información, vea [Editor de origen de ODBC &#40;página Salida de error&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Paralelismo  
 No hay límite en el número de componentes de destino ODBC que se pueden ejecutar en paralelo en la misma tabla o en tablas diferentes, en el mismo equipo o en equipos diferentes (que no sean los límites normales de la sesión global).  
  
 Sin embargo, las limitaciones del proveedor ODBC que se usa pueden restringir el número de conexiones simultáneas a través del proveedor. Estas limitaciones limitan el número de instancias en paralelo admitidas posibles para el destino ODBC. El desarrollador de SSIS debe tener en cuenta las limitaciones de cualquier proveedor ODBC que se vaya a usar y tomarlas en cuenta al generar paquetes SSIS.  
  
 También debe tener en cuenta que la carga simultánea en la misma tabla puede reducir el rendimiento debido al bloqueo de registros estándar. Esto depende de los datos que se cargan y de la organización de las tablas.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Solucionar problemas del destino ODBC  
 Puede registrar las llamadas que el origen ODBC realiza a proveedores de datos externos. Puede usar esta nueva capacidad de registro para solucionar los problemas que tengan que ver con guardar datos en orígenes de datos externos que realiza el destino ADO NET. Para registrar las llamadas realizadas por el destino ODBC a proveedores de datos externos, habilite el seguimiento del administrador de controladores ODBC. Para obtener más información, vea la documentación de Microsoft sobre *cómo generar un seguimiento ODBC con el administrador de orígenes de datos*.  
  
## <a name="configuring-the-odbc-destination"></a>Configuración del destino ODBC  
 Puede configurar el destino ODBC mediante programación o mediante el Diseñador SSIS  
  
 Para obtener más información, vea uno de los siguientes temas:  
  
-   [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de ODBC &#40;página Asignaciones&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Editor de destinos de ODBC &#40;página Salida de error&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el destino ODBC y seleccione **Mostrar editor avanzado**.  
  
 Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo Editor avanzado, vea [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Cargar datos mediante el destino de ODBC](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [Propiedades personalizadas de los destinos de ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>Editor de destino de ODBC (página Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de ODBC** para seleccionar el administrador de conexiones de ODBC para el destino. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 **Para abrir la página Administrador de conexiones del Editor de destino de ODBC**  
  
### <a name="task-list"></a>Lista de tareas  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el destino de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el destino de ODBC.  
  
-   En el **Editor de destino de ODBC**, haga clic en **Administrador de conexiones**.  
  
### <a name="options"></a>Opciones  
  
#### <a name="connection-manager"></a>Administrador de conexiones  
 Seleccione un administrador de conexiones de ODBC existente en la lista o haga clic en Nueva para crear una nueva conexión. La conexión puede ser a cualquier base de datos compatible con ODBC.  
  
#### <a name="new"></a>Nuevo  
 Haga clic en **Nueva**. Se abrirá el cuadro de diálogo **Configurar el administrador de conexiones ODBC** , donde puede crear un administrador de conexiones nuevo.  
  
#### <a name="data-access-mode"></a>Modo de acceso a datos  
 Seleccione el método para cargar datos en el destino. Las opciones se muestran en la tabla siguiente:  
  
|Opción|Descripción|  
|------------|-----------------|  
|Nombre de la tabla - Lote|Seleccione esta opción para configurar el destino de ODBC de manera que funcione en modo por lotes. Cuando seleccione esta opción, aparecerán las opciones siguientes:|  
||**Nombre de la tabla o la vista**: seleccione una tabla o vista disponible en la lista.<br /><br /> Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el carácter comodín (\*) para escribir cualquier parte del nombre con el fin de mostrar las tablas que quiere usar.<br /><br /> **Tamaño del lote**: escriba el tamaño del lote para la carga masiva. Es el número de filas cargadas como un lote.|  
|Nombre de la tabla - Fila a fila|Seleccione esta opción para configurar el destino de ODBC de manera que se inserte cada una de las filas en la tabla de destino de una en una. Cuando seleccione esta opción, aparecerá la opción siguiente:|  
||**Nombre de la tabla o la vista**: seleccione en la lista una tabla o vista disponible en la base de datos.<br /><br /> Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.|  
  
#### <a name="preview"></a>Vista previa  
 Haga clic en **Vista previa** para ver hasta 200 filas de datos para la tabla que ha seleccionado.  
  
## <a name="odbc-destination-editor-mappings-page"></a>Editor de destino de ODBC (página Asignaciones)
  Use la página **Asignaciones** del cuadro de diálogo **Editor de destino de ODBC** para asignar columnas de entrada a columnas de destino.  
  
### <a name="options"></a>Opciones  
  
#### <a name="available-input-columns"></a>Columnas de entrada disponibles  
 Lista de columnas de entrada disponibles. Arrastre y coloque una columna de entrada en una columna de destino disponible para asignar las columnas.  
  
#### <a name="available-destination-columns"></a>Columnas de destino disponibles  
 Lista de columnas de destino disponibles. Arrastre y coloque una columna de destino en una columna de entrada disponible para asignar las columnas.  
  
#### <a name="input-column"></a>Columna de entrada  
 Permite ver las columnas de entrada seleccionadas. Para quitar asignaciones, seleccione **\<ignore>** con el fin de excluir columnas de la salida.  
  
#### <a name="destination-column"></a>Columna de destino  
 Muestra todas las columnas de destino disponibles, tanto las asignadas como las no asignadas.  
  
## <a name="odbc-destination-editor-error-output-page"></a>Editor de destinos de ODBC (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de destinos de ODBC** para seleccionar las opciones de control de errores.  
  
 **Para abrir la página Salida de error del Editor de destinos de ODBC**  
  
### <a name="task-list"></a>Lista de tareas  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el destino de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el destino de ODBC.  
  
-   En el **Editor de destinos de ODBC**, haga clic en **Salida de error**.  
  
### <a name="options"></a>Opciones  
  
#### <a name="inputoutput"></a>Entrada/salida  
 Muestra el nombre del origen de datos.  
  
#### <a name="column"></a>Columna  
 No se usa.  
  
#### <a name="error"></a>Error  
 Seleccione la forma en la que el destino de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="truncation"></a>Truncamiento  
 Seleccione la forma en la que el destino de ODBC debe controlar los truncamientos en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="description"></a>Descripción  
 Muestra una descripción del error.  
  
#### <a name="set-this-value-to-selected-cells"></a>Establecer este valor en las celdas seleccionadas  
 Seleccione la forma en la que el destino de ODBC controla todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="apply"></a>Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
### <a name="error-handling-options"></a>Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el destino de ODBC controla errores y truncamientos.  
  
#### <a name="fail-component"></a>Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Este es el comportamiento predeterminado.  
  
#### <a name="ignore-failure"></a>Omitir error  
 Se omite el error o el truncamiento.  
  
#### <a name="redirect-flow"></a>Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del destino de ODBC. Para obtener más información, vea Destino de ODBC.  
  
