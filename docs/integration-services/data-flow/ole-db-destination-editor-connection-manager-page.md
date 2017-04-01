---
title: "Editor de destino de OLE DB (p&#225;gina Administrador de conexiones) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbdestadapter.connection.f1"
helpviewer_keywords: 
  - "Editor de destino OLE DB"
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
caps.latest.revision: 81
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 81
---
# Editor de destino de OLE DB (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de OLE DB** para seleccionar la conexión OLE DB del destino. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
> [!NOTE]  
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, el origen de datos requiere un administrador de conexiones distinto al de las versiones anteriores de Excel. Para más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del destino de OLE DB no está disponible en el **Editor de destino de OLE DB**, pero se puede establecer mediante el **Editor avanzado**. Además, ciertas opciones de carga rápida solo están disponibles en el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el destino de OLE DB en [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
 Para obtener más información acerca del destino de OLE DB, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## Opciones estáticas  
 **OLE DB, administrador de conexiones**  
 Seleccione un administrador de conexiones de la lista o haga clic en **Nuevo** para crear una conexión.  
  
 **Nuevo**  
 Cree un administrador de conexiones con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB**.  
  
 **Modo de acceso a datos**  
 Especifique el método para cargar los datos en el destino. Para cargar datos del juego de caracteres de doble byte (DBCS), es necesario que utilice una de las opciones de carga rápida. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
|Opción|Description|  
|------------|-----------------|  
|Tabla o vista|Carga los datos en una tabla o vista del destino OLE DB.|  
|Carga rápida de tabla o vista|Carga los datos en una tabla o vista del destino OLE DB y utiliza la opción de carga rápida. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Variable de nombre de tabla o nombre de vista|Especifique el nombre de la tabla o vista de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Carga rápida de variable de nombre de tabla o nombre de vista|Especifica el nombre de la tabla o la vista en una variable y utiliza la opción de carga rápida para cargar los datos. Para obtener más información acerca de los modos de acceso a datos de carga rápida, optimizados para inserciones masivas, vea [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).|  
|Comando SQL|Carga los datos en el destino OLE DB mediante una consulta SQL.|  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta**. La vista previa puede mostrar hasta 200 filas.  
  
## Opciones dinámicas del modo de acceso a datos  
 Cada uno de los valores de **Modo de acceso a datos** muestra un conjunto dinámico de opciones específico de ese valor. En las secciones siguientes se describe cada una de las opciones dinámicas disponibles para cada valor de **Modo de acceso a datos** .  
  
### Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
 **Nuevo**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla**.  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
### Modo de acceso a datos = Carga rápida de tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione una tabla o una vista de la base de datos con esta lista, o bien haga clic en **Nuevo** para crear una tabla.  
  
 **Nuevo**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla**.  
  
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
  
 Si proporciona un valor en esta propiedad, el destino confirma las filas en lotes con el tamaño menor de (a) el **Tamaño máximo de confirmación de inserción** o (b) las filas restantes del búfer que se está procesando.  
  
> [!NOTE]  
>  Los errores de restricciones en el destino provocan el error del lote completo de las filas definidas por **Tamaño máximo de confirmación de inserción**.  
  
### Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
### Modo de acceso a datos = Carga rápida de variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
 **Nuevo**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla**.  
  
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
  
### Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, haga clic en **Generar consulta** para generar la consulta, o bien haga clic en **Examinar** para buscar el archivo que contiene el texto de la consulta.  
  
> [!NOTE]  
>  El destino de OLE DB no admite parámetros. Si tiene que ejecutar una instrucción INSERT con parámetros, puede usar la transformación Comando de OLE DB. Para más información, consulte [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de OLE DB &#40;página Asignaciones&#41;](../../integration-services/data-flow/ole-db-destination-editor-mappings-page.md)   
 [Editor de destino de OLE DB &#40;página Salida de error&#41;](../../integration-services/data-flow/ole-db-destination-editor-error-output-page.md)   
 [Cargar datos mediante el destino de OLE DB](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  