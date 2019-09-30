---
title: Origen ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19a234b8c2939730a6c5a815885606dac15d0a0a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298169"
---
# <a name="odbc-source"></a>Origen ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El origen ODBC extrae los datos de una base de datos con ODBC mediante una tabla de base de datos, una vista o una instrucción SQL.  
  
 El origen ODBC tiene los modos de acceso a datos siguientes para extraer datos:  
  
-   Una tabla o vista.  
  
-   Los resultados de una instrucción SQL.  
  
 El origen utiliza un administrador de conexiones ODBC, que especifica el proveedor que usar.  
  
 Un origen ODBC incluye las columnas de salida de datos de origen. Cuando las columnas de salida se asignan en el destino ODBC a las columnas de destino, pueden aparecer errores si no se ha asignado ninguna columna de salida a las columnas de destino. Se pueden asignar columnas de tipos diferentes, sin embargo, si los datos de salida no son compatibles con el destino, se produce un error en tiempo de ejecución. En función de la opción de comportamiento del error, se omitirá el error, se producirá un error o la fila se enviará a la salida de error.  
  
 El origen ODBC tiene una salida normal y una salida de error.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 El origen ODBC tiene una salida de error. La salida de error del componente incluye las columnas de salida siguientes:  
  
-   **Código de error**: número que corresponde al error actual. Vea la documentación de la base de datos con ODBC que usa para obtener una lista de errores. Para obtener una lista de códigos de errores de SSIS, vea la referencia Código de errores y mensajes de SSIS.  
  
-   **Columna de error**: la columna de origen que produce el error (para los errores de conversión).  
  
-   Columnas estándar de datos de salida.  
  
 Según la configuración del comportamiento de los errores, el origen ODBC permite devolver los errores (conversión de datos, truncamiento) que aparecerán durante el proceso de extracción en la salida de error. Para obtener más información, vea [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Compatibilidad con tipos de datos  
 Para obtener información sobre los tipos de datos admitidos por el origen ODBC, vea Conector para conectividad abierta de base de datos (ODBC).  
  
## <a name="extract-options"></a>Opciones de extracción  
 El origen ODBC funciona en modo **Lote** o **Fila a fila** . La propiedad **FetchMethod** determina el modo usado. En la lista siguiente, se describen los modos.  
  
-   **Lote**: el componente intenta usar el método más eficaz de búsqueda en función de las funcionalidades del proveedor ODBC percibidas. Para la mayoría de los proveedores ODBC modernos, es SQLFetchScroll con enlace de matriz (donde el tamaño de la matriz se determina mediante la propiedad **BatchSize** ). Si selecciona **Lote** y el proveedor no admite este método, el destino ODBC cambia automáticamente los modificadores al modo **Fila a fila** .  
  
-   **Fila a fila**: el componente usa SQLFetch para recuperar las filas de una en una.  
  
 Para obtener más información acerca de la la propiedad **FetchMethod** , vea [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Parallelism  
 No hay límite en el número de componentes de origen ODBC que se pueden ejecutar en paralelo en la misma tabla o en tablas diferentes, en el mismo equipo o en equipos diferentes (que no sean los límites normales de la sesión global).  
  
 Sin embargo, las limitaciones del proveedor ODBC que se usa pueden restringir el número de conexiones simultáneas a través del proveedor. Estas limitaciones limitan el número de instancias en paralelo admitidas posibles para el origen ODBC. El desarrollador de SSIS debe tener en cuenta las limitaciones de cualquier proveedor ODBC que se vaya a usar y tomarlas en cuenta al generar paquetes SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Solucionar problemas del origen de ODBC  
 Puede registrar las llamadas que el origen ODBC realiza a proveedores de datos externos. Puede usar esta capacidad de registro para solucionar los problemas relacionados con la carga de datos de orígenes de datos externos que realiza el origen ODBC. Para registrar las llamadas realizadas por el origen ODBC a proveedores de datos externos, habilite el seguimiento del administrador de controladores ODBC. Para obtener más información, vea la documentación de Microsoft sobre *cómo generar un seguimiento ODBC con el administrador de orígenes de datos.*  
  
## <a name="configuring-the-odbc-source"></a>Configurar el origen ODBC  
 Puede configurar el origen ODBC mediante programación o través del Diseñador SSIS.  
  
 El cuadro de diálogo **Editor avanzado** contiene las propiedades que se pueden establecer mediante programación.  
  
 Para abrir el cuadro de diálogo **Editor avanzado** :  
  
-   En la pantalla **Flujo de datos** del proyecto de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , haga clic con el botón secundario en el origen ODBC y seleccione **Mostrar editor avanzado**.  
  
 Para obtener más información acerca de las propiedades que se pueden establecer en el cuadro de diálogo Editor avanzado, vea [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Extraer datos mediante el origen ODBC](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [Propiedades personalizadas del origen ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>Editor de origen de ODBC (página Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de ODBC** para seleccionar el administrador de conexiones de ODBC para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
### <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Administrador de conexiones del Editor de origen de ODBC**  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el origen de ODBC.  
  
### <a name="options"></a>Opciones  
  
#### <a name="connection-manager"></a>Administrador de conexiones  
 Seleccione un administrador de conexiones de ODBC existente en la lista o haga clic en **Nueva** para crear una nueva conexión. La conexión puede ser a cualquier base de datos compatible con ODBC.  
  
#### <a name="new"></a>Nuevo  
 Haga clic en **Nueva**. Se abrirá el cuadro de diálogo **Configurar el administrador de conexiones ODBC** , donde puede crear un administrador de conexiones ODBC nuevo.  
  
#### <a name="data-access-mode"></a>Modo de acceso a datos  
 Elija el método para la selección de datos desde el origen. Las opciones se muestran en la tabla siguiente:  
  
|Opción|Descripción|  
|------------|-----------------|  
|Nombre de tabla|Recupera datos de una tabla o vista del origen de datos de ODBC. Cuando seleccione esta opción, seleccione un valor de la lista para lo siguiente:|  
||**Nombre de la tabla o la vista**: seleccione una tabla o vista disponible en la lista o escriba una expresión regular para identificar la tabla.|  
||Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.|  
|Comando SQL|Recupera datos del origen de datos de ODBC mediante una consulta SQL. Debe escribir la consulta con la sintaxis de la base de datos de origen con la que está trabajando. Cuando seleccione esta opción, escriba una consulta de una de las siguientes maneras:|  
||Escriba el texto de la consulta SQL en el campo de **Texto de comando SQL** .|  
||Haga clic en **Examinar** para cargar la consulta SQL desde un archivo de texto.|  
||Haga clic en **Analizar consulta** para comprobar la sintaxis del texto de la consulta.|  
  
#### <a name="preview"></a>Vista previa  
 Haga clic en **Vista previa** para ver hasta las 200 primeras filas de los datos extraídos de la tabla o la vista seleccionada.  
  
## <a name="odbc-source-editor-columns-page"></a>Editor de origen de ODBC (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de orígenes ODBC** para asignar una columna de salida a cada columna externa (origen).  
  
### <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Columnas del Editor de origen de ODBC**  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen ODBC.  
  
3.  En el **Editor de origen de ODBC**, haga clic en **Columnas**.  
  
### <a name="options"></a>Opciones  
  
#### <a name="available-external-columns"></a>Columnas externas disponibles  
 Lista de las columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas. Seleccione las columnas que se van a usar desde el origen. Las columnas seleccionadas se agregan a la lista **Columna externa** en el orden en que se seleccionan.  
  
 Active la casilla **Seleccionar todas** para seleccionar todas las columnas.  
  
#### <a name="external-column"></a>Columna externa  
 Vista de las columnas externas (origen) en el orden en que se verán cuando configure los componentes que usan datos del origen de ODBC.  
  
#### <a name="output-column"></a>Columna de salida  
 Especifique un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre especificado se muestra en el Diseñador de SSIS.  
  
## <a name="odbc-source-editor-error-output-page"></a>Editor de origen de ODBC (página Salida de error)
  Use la página **Salida de error** del cuadro de diálogo **Editor de origen de ODBC** para seleccionar las opciones de control de errores.  
  
### <a name="task-list"></a>Lista de tareas  
 **Para abrir la página Salida de error del Editor de origen de ODBC**  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
-   En la pestaña **Flujo de datos** , haga doble clic en el origen de ODBC.  
  
-   En el **Editor de origen de ODBC**, haga clic en **Salida de error**.  
  
### <a name="options"></a>Opciones  
  
#### <a name="inputoutput"></a>Entrada/salida  
 Muestra el nombre del origen de datos.  
  
#### <a name="column"></a>columna  
 No se usa.  
  
#### <a name="error"></a>Error  
 Seleccione la forma en la que el origen de ODBC debe controlar errores en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="truncation"></a>Truncamiento  
 Seleccione la forma en la que el origen de ODBC debe controlar el truncamiento en un flujo: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="description"></a>Descripción  
 No se usa.  
  
#### <a name="set-this-value-to-selected-cells"></a>Establecer este valor en las celdas seleccionadas  
 Seleccione cómo el origen de ODBC va a controlar todas las celdas seleccionadas cuando se produzca un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
#### <a name="apply"></a>Aplicar  
 Aplica las opciones de control de errores a las celdas seleccionadas.  
  
### <a name="error-handling-options"></a>Opciones de control de errores  
 Use las opciones siguientes para configurar la forma en la que el origen de ODBC controla errores y truncamientos.  
  
#### <a name="fail-component"></a>Error de componente  
 La tarea Flujo de datos genera un error cuando se produce un error o truncamiento. Éste es el comportamiento predeterminado.  
  
#### <a name="ignore-failure"></a>Omitir error  
 Se omite el error o el truncamiento.  
  
#### <a name="redirect-flow"></a>Redirigir fila  
 La fila que está produciendo el error o el truncamiento se dirige a la salida de error del origen de ODBC.  
  
  
