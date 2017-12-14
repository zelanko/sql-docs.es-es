---
title: Origen de Excel | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: "60"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 61e28171171a822f25da6979340785bc5c114e1c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="excel-source"></a>Origen de Excel
  El origen de Excel extrae datos de hojas de cálculo o de rangos de libros de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 El origen de Excel ofrece cuatro modos de acceso a datos distintos para extraer datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
-   Los resultados de una instrucción SQL, almacenados en una variable.  
  
> [!IMPORTANT]  
>  En Excel, una hoja o un rango equivalen a una tabla o vista. La lista de tablas disponibles en los editores de Origen y Destino de Excel muestra las hojas de cálculo existentes (identificadas con el signo $ anexado al nombre de la hoja de cálculo, como, por ejemplo, Hoja1$) y rangos con nombre (identificados por la falta del signo $, como por ejemplo, MiRango). Para obtener más información, vea la sección Consideraciones de uso.  
  
 El origen de Excel usa un Administrador de conexiones con Excel para conectar con un origen de datos y el Administrador de conexiones especifica el archivo de libro que se debe usar. Para más información, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 El origen de Excel tiene una salida normal y una salida de error.  
  
## <a name="usage-considerations"></a>Consideraciones de uso  
 El Administrador de conexiones con Excel usa el Proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para Jet 4.0 y el controlador ISAM (Método de acceso secuencial indexado) de Excel asociado para conectar con orígenes Excel de datos y leer y escribir datos en ellos.  
  
 Muchos artículos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base documentan el comportamiento de este proveedor y el controlador. Aunque estos artículos no son específicos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ni de Servicios de transformación de datos (su predecesor), posiblemente le interese conocer determinados comportamientos que pueden provocar resultados inesperados. Para obtener información general sobre el uso y el comportamiento del controlador de Excel, vea [Cómo usar ADO con datos de Excel procedentes de Visual Basic o VBA](http://support.microsoft.com/kb/257819).  
  
 Los siguientes comportamientos del proveedor Jet con el controlador de Excel pueden provocar resultados inesperados al leer datos de un origen de datos de Excel.  
  
-   **Orígenes de datos**. El origen de datos de un libro de Excel puede ser una hoja de cálculo, a cuyo nombre debe agregarse el signo $ (por ejemplo, Hoja1$), un rango con nombre (por ejemplo, MiRango). En una instrucción SQL, el nombre de la hoja debe estar delimitado (por ejemplo [Hoja1$]) para evitar un error de sintaxis producido por el signo $. El Generador de consultas agrega automáticamente estos delimitadores. Al especificar una hoja de cálculo o un rango, el controlador lee los bloques contiguos de celdas, comenzando con la primera celda no vacía en la esquina superior izquierda de la hoja de cálculo o rango. Por tanto, no deben dejarse filas vacías en los datos de origen, ni una fila vacía entre las filas de título o de cabecera y las filas de datos.  
  
-   **Valores que faltan**. Este controlador lee un cierto número de filas (de forma predeterminada, 8) en el origen especificado para elegir el tipo de datos de cada columna. Cuando una columna parece contener varios tipos de datos, especialmente numéricos y de texto, el controlador elige el tipo más usado y devuelve valores NULL en las celdas que contienen datos de los demás tipos. (En caso de empate, el tipo numérico tiene prioridad.) La mayoría de las opciones de formato en las hojas Excel parecen no afectar a esta determinación de tipos de datos. Para modificar este comportamiento del controlador de Excel, especifique el modo de importación. Para especificar el modo de importación, agregue **IMEX=1** al valor de Propiedades extendidas en la cadena de conexión del Administrador de conexiones con Excel en la ventana **Propiedades** . Para obtener más información, vea [PRB: valores de Excel devueltos como NULL usando DAO OpenRecordset](http://support.microsoft.com/kb/194124).  
  
-   **Texto truncado**. Cuando el controlador determina que una columna de Excel contiene datos de texto, el controlador selecciona el tipo de datos (cadena o memorando) en función del valor más largo que muestrea. Si el controlador no descubre valores de más de 255 caracteres en las filas que muestrea, trata a la columna como una columna de cadena de 255 caracteres en lugar de una columna memorando. Así, es posible que se trunquen las cadenas con más de 255 caracteres. Para importar datos de una columna memorando sin que se trunquen, debe asegurarse de que la columna memo contenga, en al menos una de las filas muestreadas, un valor superior a los 255 caracteres, o tendrá que incrementar el número de filas muestreadas por el controlador para que se incluya dicha fila. Puede aumentar el número de filas muestreadas al incrementar el valor de **TypeGuessRows** en la clave del registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** . Para más información, vea [PRB: transferencia de datos del origen de OLEDB de Jet 4.0 con error](http://support.microsoft.com/kb/281517).  
  
-   **Tipos de datos**. El controlador de Excel reconoce solo un conjunto limitado de tipos de datos. Por ejemplo, todas las columnas numéricas se interpretan como dobles (DT_R8) y todas las columnas de cadena (a excepción de las columnas memorando) se interpretan como cadenas Unicode de 255 caracteres (DT_WSTR). [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] asigna los tipos de datos de Excel de la siguiente manera:  
  
    -   Numérico: flotante de doble precisión (DT_R8)  
  
    -   Moneda: moneda (DT_CY)  
  
    -   Booleano: booleano (DT_BOOL)  
  
    -   Fecha y hora: **datetime** (DT_DATE)  
  
    -   Cadena: cadena Unicode, longitud de 255 caracteres (DT_WSTR)  
  
    -   Memorando: flujo de texto Unicode (DT_NTEXT)  
  
-   **Conversiones de tipo de datos y de longitud**. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no convierte tipos de datos de forma implícita. Como resultado, probablemente necesite utilizar las transformaciones Columna derivada o Conversión de datos para convertir datos de Excel de forma explícita antes de cargarlos en un destino diferente de Excel, o para convertir datos que no son de Excel antes de cargarlos en un destino de Excel. En este caso, puede resultar útil crear el paquete inicial a través del Asistente para importación y exportación, que le configura las conversiones necesarias. Entre algunos ejemplos de las conversiones que se pueden requerir, figuran:  
  
    -   Conversión entre columnas de cadena de Excel Unicode y columnas de cadena no Unicode con páginas de códigos específicas  
  
    -   Conversión entre columnas de cadena de Excel de 255 caracteres y columnas de cadena de diferentes longitudes  
  
    -   Conversión entre columnas numéricas de Excel de doble precisión y columnas numéricas de otros tipos  
  
## <a name="excel-source-configuration"></a>Configuración del origen de Excel  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica todas las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para más información sobre cómo crear bucles entre un grupo de archivos de Excel, vea [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Asignar parámetros de consulta a variables en un componente de flujo de datos](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles ForEach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
## <a name="excel-source-editor-connection-manager-page"></a>Editor de origen de Excel (página Administrador de conexiones)
  Utilice el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel** para seleccionar el libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] que utilizará el origen. El origen de Excel lee los datos de una hoja de cálculo o un rango con nombre de un libro existente.  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de Excel no está disponible en el **Editor de origen de Excel**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **OLE DB, administrador de conexiones**  
 Seleccione un administrador de conexiones de Excel en la lista o cree una nueva conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Value|Description|  
|-----------|-----------------|  
|Tabla o vista|Recupera los datos de una hoja de cálculo o un rango con nombre del archivo Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada** [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Recupera datos del archivo Excel mediante una consulta SQL. |  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el libro de Excel.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien examine el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Parámetros**  
 Si ha escrito una consulta con parámetros mediante ? como marcador de posición de parámetro en el texto de la consulta, utilice el cuadro de diálogo **Establecer parámetros de consulta** para asignar los parámetros de entrada de las consultas a las variables del paquete.  
  
 **Build query**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Modo de acceso a datos = Comando SQL de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene el texto de la consulta SQL.  
  
## <a name="excel-source-editor-columns-page"></a>Editor de origen de Excel (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de origen de Excel** para asignar una columna de salida a cada columna externa (origen).  
  
### <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Vea las columnas externas (origen) en el orden en que la tarea las leerá. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla anterior y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="excel-source-editor-error-output-page"></a>Editor de origen de Excel (página Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de origen de Excel** para seleccionar opciones de control de errores y establecer las propiedades en las columnas de salida de errores.  
  
### <a name="options"></a>Opciones  
 **Entrada o salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Permite ver las columnas externas (origen) seleccionadas en la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel**.  
  
 **Error**  
 Permite especificar qué debe ocurrir cuando se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Temas relacionados:** [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 Permite especificar qué debe ocurrir cuando se produce un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Description**  
 Muestra la descripción del error.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Entrada de blog sobre cómo [importar datos de Excel de 64 bits en SSIS](http://go.microsoft.com/fwlink/?LinkId=217673)en hrvoje.piasevoli.com  
  
-   Entrada de blog, [Excel en Integration Services, parte 1 de 3: conexiones y componentes](http://go.microsoft.com/fwlink/?LinkId=217674), en dougbert.com  
  
-   Entrada de blog, [Excel en Integration Services, parte 2 de 3: tablas y tipos de datos](http://go.microsoft.com/fwlink/?LinkId=217675), en dougbert.com.  
  
-   Entrada de blog, [Excel en Integration Services, parte 3 de 3: problemas y alternativas](http://go.microsoft.com/fwlink/?LinkId=217676), en dougbert.com.  
  
  
