---
title: Origen OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 37c720096cb27f19617744512c212c415373612b
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639622"
---
# <a name="ole-db-source"></a>Origen de OLE DB
  El origen de OLE DB extrae datos de varias bases de datos relacionales compatibles con OLE DB mediante una tabla de base de datos, una vista o un comando SQL. Por ejemplo, el origen de OLE DB puede extraer datos de tablas de bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Si el origen de datos es [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, el origen de datos requiere un administrador de conexiones distinto al de las versiones anteriores de Excel. Para más información, vea [Conectarse a un libro de Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 El origen de OLE DB proporciona cuatro modos de acceso distintos para extraer datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
-   Los resultados de una instrucción SQL, almacenados en una variable.  
  
> [!NOTE]  
>  Cuando use una instrucción SQL para invocar un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
 Si utiliza una consulta con parámetros, puede asignar variables a parámetros para especificar los valores para parámetros individuales en las instrucciones SQL.  
  
 Este origen utiliza un administrador de conexiones OLE DB para conectar con el origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para más información, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también proporciona el objeto de origen de datos a partir del que se puede crear un administrador de conexiones OLE DB, haciendo que los orígenes de datos y las vistas de orígenes de datos estén disponibles para el origen de OLE DB.  
  
 Dependiendo del proveedor OLE DB, el origen de OLE DB podría tener algunas limitaciones:  
  
-   El proveedor [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB para Oracle no admite los tipos de datos BLOB, CLOB, NCLOB, BFILE y UROWID de Oracle, y el origen de OLE DB no puede extraer los datos de tablas que contengan columnas asociadas a estos tipos de datos.  
  
-   Los proveedores IBM OLE DB DB2 y [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 no admiten el uso de un comando SQL para llamar a un procedimiento almacenado. Cuando se usa este tipo de comandos, el origen de OLE DB no puede crear la columna de metadatos y, como consecuencia, los componentes de flujo de datos que siguen al origen de OLE DB en el flujo de datos no tienen ninguna columna disponible y se produce un error en la ejecución del flujo de datos.  
  
 El origen de OLE DB tiene una salida normal y una salida de error.  
  
## <a name="using-parameterized-sql-statements"></a>Usar instrucciones SQL con parámetros  
 El origen de OLE DB puede utilizar una instrucción SQL para extraer datos. Esta instrucción puede ser una instrucción SELECT o EXEC.  
  
 El origen de OLE DB utiliza un administrador de conexiones OLE DB para conectar con el origen de datos del que extrae los datos. Según el proveedor que utiliza el administrador de conexiones OLE DB y el sistema de administración de bases de datos relacionales (RDBMS) al que se conecta el administrador de conexiones, se aplican reglas diferentes a la asignación de nombres y enumeración de los parámetros. Si los nombres de los parámetros se devuelven de RDBMS, puede usar estos nombres para asignar parámetros de una lista de parámetros a parámetros de una instrucción SQL; de lo contrario, los parámetros se asignan al parámetro de la instrucción SQL por la posición ordinal que ocupan en la lista de parámetros. Los tipos de nombres de parámetros que se admiten dependen del proveedor. Por ejemplo, algunos proveedores requieren que utilice los nombres de variable o columna, mientras que otros proveedores requieren que utilice nombres simbólicos como 0 o Param0. Consulte la documentación específica del proveedor para obtener información sobre los nombres de parámetros que se utilizan en las instrucciones SQL.  
  
 Cuando se usa un administrador de conexiones OLE DB, no se pueden utilizar subconsultas con parámetros, ya que el origen de OLE DB no puede derivar información de parámetros a través del proveedor OLE DB. Pero puede usar una expresión para concatenar los valores de parámetros en la cadena de consulta y establecer la propiedad SqlCommand del origen. En el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , puede configurar un origen de OLE DB mediante el cuadro de diálogo **Editor de origen de OLE DB** y asignar los parámetros a las variables del cuadro de diálogo **Establecer parámetros de consulta** .  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>Especificar parámetros mediante posiciones ordinales  
 Si no se devuelven nombres de parámetros, el orden en el que se enumeran los parámetros en la lista **Parámetros** del cuadro de diálogo **Establecer parámetros de consulta** determina el marcador de parámetro al que se asignan en tiempo de ejecución. El primer parámetro de la lista se asigna al primer signo ? de la instrucción SQL, el segundo parámetro al segundo signo ?, y así sucesivamente.  
  
 La siguiente instrucción SQL selecciona filas de la tabla **Products** de la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] . El primer parámetro de la lista **Asignaciones** se asigna al primer parámetro de la columna **Color** , y el segundo parámetro a la columna **Size** .  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 Los nombres de parámetro no tienen ningún efecto. Por ejemplo, si el parámetro tiene el mismo nombre que el de la columna a la que se aplica, pero no está ubicado en la posición ordinal correcta en la lista **Parámetros** , la asignación de parámetros que se produce en tiempo de ejecución utilizará la posición ordinal del parámetro, en lugar del nombre del parámetro.  
  
 El comando EXEC generalmente requiere que utilice los nombres de las variables que proporcionan valores de parámetros en el procedimiento como nombres de parámetros.  
  
### <a name="specifying-parameters-by-using-names"></a>Especificar parámetros a través de nombres  
 Si los nombres de parámetros reales se devuelven de RDBMS, los parámetros que utilizan las instrucciones SELECT y EXEC se asignan por nombre. Los nombres de parámetros deben coincidir con los nombres que espera el procedimiento almacenado, ejecutado por las instrucciones SELECT o EXEC.  
  
 La siguiente instrucción SQL ejecuta el procedimiento almacenado **uspGetWhereUsedProductID** , disponible en la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] .  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 El procedimiento almacenado espera las variables `@StartProductID` y `@CheckDate`para proporcionar valores de parámetros. El orden en el que los parámetros aparecen en la lista **Asignaciones** es irrelevante. El único requisito es que los nombres de parámetros coincidan con los nombres de variables en el procedimiento almacenado, incluido el signo \@.  
  
### <a name="mapping-parameters-to-variables"></a>Asignar parámetros a variables  
 Los parámetros se asignan a variables que proporcionan los valores de parámetros en tiempo de ejecución. Las variables son generalmente variables definidas por el usuario, aunque también puede usar variables del sistema que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si utiliza variables definidas por el usuario, asegúrese de establecer el tipo de datos en un tipo que sea compatible con el tipo de datos de la columna a la que hace referencia el parámetro asignado. Para más información, vea [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Solucionar problemas del origen de OLE DB  
 Puede registrar las llamadas realizadas por el origen de OLE DB a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con la carga de datos desde orígenes de datos externos que realiza el origen de OLE DB. Para registrar las llamadas realizadas por el origen de OLE DB a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Configurar el origen de OLE DB  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Extraer datos mediante el origen de OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Asignar parámetros de consulta a variables en un componente de flujo de datos](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo wiki, sobre [SSIS con conectores Oracle](https://go.microsoft.com/fwlink/?LinkId=220670), en social.technet.microsoft.com.  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>Editor de origen de OLE DB (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de OLE DB** para seleccionar el administrador de conexiones OLE DB para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
> [!NOTE]  
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, use un origen de OLE DB. No puede usar un origen de Excel para cargar datos desde un origen de datos de Excel 2007. Para más información, consulte [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 o anterior, use un origen de Excel. Para más información, vea [Editor de origen de Excel &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de OLE DB no está disponible en el **Editor de origen de OLE DB**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Abrir el Editor de origen de OLE DB (página Administrador de conexiones)  
  
1.  Agregue el origen de OLE DB al paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente de origen y, después, haga clic en **Editar**.  
  
3.  Haga clic en **Administrador de conexiones**.  
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Obtenga datos de una tabla o vista en el origen de datos OLE DB.|  
|Variable de nombre de tabla o nombre de vista|Especifique el nombre de la tabla o vista de una variable.<br /><br /> **Información relacionada:** [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Obtenga datos del origen de datos OLE DB mediante una consulta SQL.|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<value too big to display> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor SQL OLE DB y el último, cuando se utiliza el proveedor Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
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
  
## <a name="ole-db-source-editor-columns-page"></a>Editor de origen de OLE DB (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de origen de OLE DB** para asignar una columna de salida a cada columna externa (origen).  
  
### <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Muestra las columnas externas (origen) en el orden en que se verán cuando configure componentes que utilizan datos de este origen. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador SSIS.  
  
## <a name="ole-db-source-editor-error-output-page"></a>Editor de origen de OLE DB (página Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de origen de OLE DB** para seleccionar opciones de control de errores y establecer propiedades en columnas de salida de errores.  
  
### <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Muestra las columnas externas (origen) que se han seleccionado en la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de OLE DB**.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Destino de OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
