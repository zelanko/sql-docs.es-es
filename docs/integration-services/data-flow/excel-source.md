---
title: Origen de Excel | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelsource.f1
- sql13.dts.designer.excelsourceadapter.connection.f1
- sql13.dts.designer.excelsourceadapter.columns.f1
- sql13.dts.designer.excelsourceadapter.erroroutput.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
caps.latest.revision: 60
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 34a6c0953afad881e80138dd3306f386e98702f1
ms.sourcegitcommit: b3bb41424249de198f22d9c6d40df4996f083aa6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
---
# <a name="excel-source"></a>Origen de Excel
  El origen de Excel extrae datos de hojas de cálculo o de rangos de libros de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

## <a name="access-modes"></a>Modos de acceso
 El origen de Excel ofrece cuatro modos de acceso a datos distintos para extraer datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
-   Los resultados de una instrucción SQL, almacenados en una variable.  
  
 El origen de Excel usa un Administrador de conexiones con Excel para conectar con un origen de datos y el Administrador de conexiones especifica el archivo de libro que se debe usar. Para más información, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 El origen de Excel tiene una salida normal y una salida de error.  
  
## <a name="excel-source-configuration"></a>Configuración del origen de Excel  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica todas las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para más información sobre cómo crear bucles entre un grupo de archivos de Excel, vea [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md).  
  
## <a name="excel-source-editor-connection-manager-page"></a>Editor de origen de Excel (página Administrador de conexiones)
  Utilice el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel** para seleccionar el libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] que utilizará el origen. El origen de Excel lee los datos de una hoja de cálculo o un rango con nombre de un libro existente.  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de Excel no está disponible en el **Editor de origen de Excel**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OLE DB**  
 Seleccione un Administrador de conexiones con Excel en la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Valor|Descripción|  
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
  
 **Descripción**  
 Muestra la descripción del error.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="related-content"></a>Contenido relacionado  
[Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
[Destino de Excel](excel-destination.md)  
[Administrador de conexiones de Excel](../connection-manager/excel-connection-manager.md)
