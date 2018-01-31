---
title: Destino de OLE DB | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 32e0ce09ff9c804a3d7beac5e1ba251a5bc8105e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="ole-db-destination"></a>Destino de OLE DB
  El destino de OLE DB carga datos en una serie de bases de datos compatibles con OLE DB que usan una tabla o vista de base de datos o un comando SQL. Por ejemplo, un origen de OLE DB puede cargar datos en tablas en bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, el origen de datos requiere un administrador de conexiones distinto al de las versiones anteriores de Excel. Para más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 El destino de OLE DB proporciona cinco modos diferentes de acceso a los datos para cargar datos:  
  
-   Una tabla o vista. Puede especificar una tabla o vista existentes, o puede crear una nueva tabla.  
  
-   Una tabla o vista usando opciones de carga rápida. Puede especificar una tabla existente, o puede crear una nueva tabla.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Una tabla o vista especificada en una variable usando opciones de carga rápida.  
  
-   Los resultados de una instrucción SQL.  
  
> [!NOTE]  
>  El destino de OLE DB no admite parámetros. Si tiene que ejecutar una instrucción INSERT con parámetros, puede usar la transformación Comando de OLE DB. Para más información, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 Cuando el destino de OLE DB carga datos que utilizan un juego de caracteres de doble byte (DBCS), los datos se pueden dañar si el modo del acceso a datos no usa la opción de carga rápida y si el administrador de conexiones OLE DB utiliza el proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Para garantizar la integridad de datos de DBCS es necesario configurar el administrador de conexiones OLE DB para que use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client o uno de los modos de acceso de carga rápida: **Carga rápida de tabla o vista** o **Carga rápida de variable de nombre de tabla o nombre de vista**. Ambas opciones están disponibles en el cuadro de diálogo **Editor de destino de OLE DB** . Al programar el modelo de objetos [!INCLUDE[ssIS](../../includes/ssis-md.md)] , es necesario configurar la propiedad AccessMode en **OpenRowset con FastLoad**o en **OpenRowset con FastLoad desde variable**.  
  
> [!NOTE]  
>  Si usa el cuadro de diálogo **Editor de destino de OLE DB** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para crear la tabla de destino en la que el destino de OLE DB inserta los datos, puede tener que seleccionar la tabla nueva manualmente. La necesidad de selección manual se produce cuando un proveedor OLE DB, como el proveedor OLE DB para DB2 agrega automáticamente identificadores de esquema al nombre de la tabla.  
  
> [!NOTE]  
>  La instrucción CREATE TABLE que genera el cuadro de diálogo **Editor de destino de OLE DB** puede requerir una modificación, en función del tipo de destino. Por ejemplo, algunos destinos no admiten tipos de datos que utiliza la instrucción CREATE TABLE.  
  
 Este destino usa un administrador de conexiones OLE DB para conectarse a un origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para más información, vea [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también proporciona el objeto de origen de datos desde el que puede crear un administrador de conexiones OLE DB para poner los orígenes de datos y las vistas del origen de datos a disposición del destino de OLE DB.  
  
 Un destino de OLE DB incluye asignaciones entre columnas de entrada y columnas en el origen de datos de destino. No es necesario asignar columnas de entrada a todas las columnas de destino, pero, según las propiedades de las columnas de destino, pueden producirse errores si no se asignan columnas de entrada a las columnas de destino. Por ejemplo, si una columna de destino no permite valores NULL, se debe asignar una columna de entrada a esa columna. Además, los tipos de datos de las columnas asignadas deben ser compatibles. Por ejemplo, no se puede asignar una columna de entrada que tiene un tipo de datos de cadena a una columna de destino con un tipo de datos numérico.  
  
 El destino de OLE DB tiene una entrada normal y una salida de error.  
  
 Para obtener más información acerca de los tipos de datos, vea [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Opciones de carga rápida  
 Si el destino de OLE DB usa el modo de acceso a datos de carga rápida, puede especificar las siguientes opciones de carga rápida en la interfaz de usuario del **Editor de destino de OLE DB**para el destino:  
  
-   Mantener los valores de identidad del archivo de datos importado o usar valores exclusivos asignados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Conservar un valor NULL durante la operación de carga masiva.  
  
-   Comprobar las restricciones en la tabla o vista de destino durante la operación de importación masiva.  
  
-   Adquirir un bloqueo de nivel de tabla durante la operación de carga masiva.  
  
-   Especificar la cantidad de filas del lote y el tamaño de confirmación.  
  
 Algunas opciones de carga rápida están almacenadas en propiedades específicas del destino de OLE DB. Por ejemplo, FastLoadKeepIdentity especifica si se mantienen los valores de identificación, FastLoadKeepNulls especifica si se mantienen los valores nulos y FastLoadMaxInsertCommitSize especifica el número de filas que se confirmarán como un lote. Otras opciones de carga rápida se almacenan en una lista separada por comas, en la propiedad FastLoadOptions. Si el destino de OLE DB usa todas las opciones de carga rápida que se almacenan en FastLoadOptions y que se muestran en el cuadro de diálogo **Editor de destino de OLE DB** , el valor de la propiedad se establece en **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**. El valor 1000 indica que el destino se configura para usar lotes de 1000 filas.  
  
> [!NOTE]  
>  Los errores de restricciones en el destino provocan el error del lote completo de las filas definidas por FastLoadMaxInsertCommitSize.  
  
 Además de las opciones de carga rápida que se muestran en el cuadro de diálogo **Editor de destino de OLE DB** , puede configurar el destino de OLE DB para usar las siguientes opciones de carga masiva al escribir las opciones en la propiedad FastLoadOptions del cuadro de diálogo **Editor avanzado** .  
  
|Opción de carga rápida|Description|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Especifica el tamaño en kilobytes para insertar. La opción tiene el formato **KILOBYTES_PER_BATCH** = \<valor de entero positivo**>**.|  
|FIRE_TRIGGERS|Especifica si se activan los desencadenadores en la tabla de inserción. La opción tiene la forma **FIRE_TRIGGERS**. La presencia de la opción indica que se activan los desencadenadores.|  
|ORDER|Especifica cómo se ordenan los datos de entrada. La opción tiene el formato ORDER \<nombre de columna> ASC&#124;DESC. Se puede enumerar cualquier cantidad de columnas (el orden es opcional). Si se omite el orden, la operación de inserción presupone que los datos no están ordenados.<br /><br /> Nota: El rendimiento puede mejorar si se utiliza la opción ORDER para ordenar los datos de entrada según el índice agrupado de la tabla.|  
  
 Las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] se suelen escribir en mayúsculas, aunque las palabras clave no distinguen entre mayúsculas y minúsculas.  
  
 Para más información sobre las opciones de carga rápida, vea [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Solucionar problemas del destino de OLE DB  
 Puede registrar las llamadas realizadas por el destino OLE DB a proveedores de datos externos. Puede utilizar esta nueva capacidad de registro para solucionar problemas relacionados con el almacenamiento de datos en orígenes de datos externos que realiza el destino OLE DB. Para registrar las llamadas realizadas por el destino OLE DB a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Configurar el destino de OLE DB  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Cargar datos mediante el destino de OLE DB](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>Editor de destino de OLE DB (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de OLE DB** para seleccionar la conexión OLE DB del destino. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
> [!NOTE]  
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, el origen de datos requiere un administrador de conexiones distinto al de las versiones anteriores de Excel. Para más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del destino de OLE DB no está disponible en el **Editor de destino de OLE DB**, pero se puede establecer mediante el **Editor avanzado**. Además, ciertas opciones de carga rápida solo están disponibles en el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el destino de OLE DB en [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Modo de acceso a datos**  
 Especifique el método para cargar los datos en el destino. Para cargar datos del juego de caracteres de doble byte (DBCS), es necesario que utilice una de las opciones de carga rápida. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
|Opción|Description|  
|------------|-----------------|  
|Tabla o vista|Carga los datos en una tabla o vista del destino OLE DB.|  
|Carga rápida de tabla o vista|Carga los datos en una tabla o vista del destino OLE DB y utiliza la opción de carga rápida. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Variable de nombre de tabla o nombre de vista|Especifique el nombre de la tabla o vista de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Carga rápida de variable de nombre de tabla o nombre de vista|Especifica el nombre de la tabla o la vista en una variable y utiliza la opción de carga rápida para cargar los datos. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Comando SQL|Carga los datos en el destino OLE DB mediante una consulta SQL.|  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . La vista previa puede mostrar hasta 200 filas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
 Cada uno de los valores de **Modo de acceso a datos** muestra un conjunto dinámico de opciones específico de ese valor. En las secciones siguientes se describe cada una de las opciones dinámicas disponibles para cada valor de **Modo de acceso a datos** .  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
 **Nuevo**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla** .  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
#### <a name="data-access-mode--table-or-view--fast-load"></a>Modo de acceso a datos = Carga rápida de tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione una tabla o una vista de la base de datos con esta lista, o bien haga clic en **Nuevo**para crear una tabla.  
  
 **Nueva**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla** .  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantener valores de identidad**  
 Especifique si se copian los valores de identidad cuando se cargan los datos. Esta propiedad solo está disponible con la opción de carga rápida. El valor predeterminado de esta propiedad es **false**.  
  
 **Mantener valores NULL**  
 Especifique si se copian los valores NULL cuando se cargan los datos. Esta propiedad solo está disponible con la opción de carga rápida. El valor predeterminado de esta propiedad es **false**.  
  
 **Bloqueo de tabla**  
 Especifique si la tabla se bloquea durante la carga. El valor predeterminado de esta propiedad es **true**.  
  
 **Restricciones CHECK**  
 Especifique si el destino comprueba restricciones cuando carga datos. El valor predeterminado de esta propiedad es **true**.  
  
 **Filas por lote**  
 Especifique el número de filas de un lote. El valor predeterminado de esta propiedad es **-1**, lo que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de OLE DB** para indicar que no quiere asignar un valor personalizado a esta propiedad.  
  
 **Tamaño máximo de confirmación de inserción**  
 Especifique el tamaño de lote que el destino OLE DB intenta confirmar en operaciones de carga rápida. El valor de **0** indica que todos los datos se han confirmado en un solo lote después de procesar todas las filas.  
  
> [!NOTE]  
>  El valor **0** podría hacer que el paquete en ejecución deje de responder si el destino de OLE DB y otro componente de flujo de datos están actualizando la misma tabla de origen. Para evitar que el paquete se detenga, establezca la opción **Tamaño máximo de confirmación de inserción** en **2147483647**.  
  
 Si proporciona un valor en esta propiedad, el destino confirma las filas en lotes con el tamaño menor de (a) el **Tamaño máximo de confirmación de inserción**o (b) las filas restantes del búfer que se está procesando.  
  
> [!NOTE]  
>  Los errores de restricciones en el destino provocan el error del lote completo de las filas definidas por **Tamaño máximo de confirmación de inserción** .  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable--fast-load"></a>Modo de acceso a datos = Carga rápida de variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
 **Nueva**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla** .  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantener valores de identidad**  
 Especifique si se copian los valores de identidad cuando se cargan los datos. Esta propiedad solo está disponible con la opción de carga rápida. El valor predeterminado de esta propiedad es **false**.  
  
 **Mantener valores NULL**  
 Especifique si se copian los valores NULL cuando se cargan los datos. Esta propiedad solo está disponible con la opción de carga rápida. El valor predeterminado de esta propiedad es **false**.  
  
 **Bloqueo de tabla**  
 Especifique si la tabla se bloquea durante la carga. El valor predeterminado de esta propiedad es **false**.  
  
 **Restricciones CHECK**  
 Especifique si la tarea comprueba restricciones. El valor predeterminado de esta propiedad es **false**.  
  
 **Filas por lote**  
 Especifique el número de filas de un lote. El valor predeterminado de esta propiedad es **-1**, lo que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de OLE DB** para indicar que no quiere asignar un valor personalizado a esta propiedad.  
  
 **Tamaño máximo de confirmación de inserción**  
 Especifique el tamaño de lote que el destino OLE DB intenta confirmar en operaciones de carga rápida. El valor predeterminado **2147483647** indica que todos los datos se confirman en un solo lote, tras el procesamiento de todas las filas.  
  
> [!NOTE]  
>  El valor **0** podría hacer que el paquete en ejecución deje de responder si el destino de OLE DB y otro componente de flujo de datos están actualizando la misma tabla de origen. Para evitar que el paquete se detenga, establezca la opción **Tamaño máximo de confirmación de inserción** en **2147483647**.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
> [!NOTE]  
>  El destino de OLE DB no admite parámetros. Si tiene que ejecutar una instrucción INSERT con parámetros, puede usar la transformación Comando de OLE DB. Para más información, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
## <a name="ole-db-destination-editor-mappings-page"></a>Editor de destino de OLE DB (página Asignaciones)
  Utilice la página **Asignaciones** del cuadro de diálogo **Editor de destino de OLE DB** para asignar columnas de entrada a columnas de destino.  
  
### <a name="options"></a>.  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de entrada disponibles de la tabla a columnas de destino.  
  
 **Columnas de destino disponibles**  
 Muestra la lista de columnas de destino disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de destino disponibles de la tabla a columnas de entrada.  
  
 **Columna de entrada**  
 Permite ver las columnas de entrada seleccionadas. Para quitar asignaciones, seleccione **\<ignore>** con el fin de excluir columnas de la salida.  
  
 **Columna de destino**  
 Muestra todas las columnas de destino disponibles, tanto si están asignadas como si no lo están.  
  
## <a name="ole-db-destination-editor-error-output-page"></a>Editor de destino de OLE DB (página Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de destino de OLE DB** para especificar las opciones de control de errores.  
  
### <a name="options"></a>.  
 **Entrada/salida**  
 Muestra el nombre de la entrada.  
  
 **Columna**  
 No se usa.  
  
 **Error**  
 Permite especificar qué debe ocurrir cuando se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Temas relacionados:** [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 No se usa.  
  
 **Descripción**  
 Muestra la descripción de la operación.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Origen de OLE DB](../../integration-services/data-flow/ole-db-source.md)  
  
 [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
