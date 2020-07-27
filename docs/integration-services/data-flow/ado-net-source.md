---
title: Origen de ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: acbf13282531e22c37acd247a42f4f346fa6b393
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922811"
---
# <a name="ado-net-source"></a>Origen de ADO NET

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El origen de ADO NET consume datos de un proveedor .NET y hace que los datos estén disponibles para el flujo de datos.  
  
 Puede usar el origen de ADO NET para conectarse a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. No se admite la conexión a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mediante OLE DB. Para más información sobre [!INCLUDE[ssSDS](../../includes/sssds-md.md)], consulte [Instrucciones y limitaciones generales (Azure SQL Database)](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Compatibilidad con tipos de datos  
 El origen convierte cualquier tipo de datos que no se asigna a un tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] específico en el tipo de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] DT_NTEXT. Esta conversión se produce aunque el tipo de datos sea **System.Object**.  
  
 Puede cambiar el tipo de datos DT_NTEXT a DT_WSTR, o el tipo de datos DT_WSTR a DT_NTEXT. Para cambiar los tipos de datos, establezca la propiedad **DataType** en el cuadro de diálogo **Editor avanzado** del origen de ADO NET. Para más información, consulte [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 El tipo de datos DT_NTEXT también se puede convertir en el tipo de datos DT_BYTES o DT_STR utilizando una transformación de conversión de datos después del origen de ADO NET. Para más información, consulte [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
 En [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], los tipos de datos de fecha, DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 y DT_DBTIMESTAMPOFFSET, se asignan a ciertos tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede configurar el origen de ADO NET de modo que se conviertan los tipos de datos de fecha de los datos que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para configurar el origen de ADO NET de modo que se conviertan estos tipos de datos de fecha, establezca la propiedad **Type System Version** del administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] en **Latest**. (La propiedad **Type System Version** está en la página **Todo** del cuadro de diálogo **Administrador de conexiones** . Para abrir el cuadro de diálogo **Administrador de conexiones** , haga clic con el botón derecho en el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] y, después, elija **Editar**).  
  
> [!NOTE]  
>  Si la propiedad **Type System Version** del administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] se establece en **SQL Server 2005**, el sistema convierte los tipos de datos de fecha de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en DT_WSTR.  
  
 El sistema convierte los tipos de datos definidos por el usuario (UDT) en objetos binarios grandes (BLOB) de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cuando el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] especifica el proveedor como Proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient). El sistema aplica las reglas siguientes cuando convierte el tipo de datos UDT:  
  
-   Si los datos son de un tipo UDT que no es grande, el sistema los convierte en DT_BYTES.  
  
-   Si los datos son de un tipo UDT que no es grande y la propiedad **Length** de la columna de la base de datos se establece en -1 o en un valor mayor que 8000 bytes, el sistema convierte los datos en DT_IMAGE.  
  
-   Si los datos son de un tipo UDT grande, el sistema los convierte en DT_IMAGE.  
  
    > [!NOTE]  
    >  Si el origen de ADO NET no está configurado para utilizar la salida de errores, el sistema pasa el flujo de datos a la columna DT_IMAGE en fragmentos de 8.000 bytes. Si el origen de ADO NET está configurado para utilizar la salida de errores, el sistema pasa la matriz entera de bytes a la columna DT_IMAGE. Para más información sobre cómo configurar los componentes para que se use la salida de errores, vea [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Para más información sobre los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , las conversiones de tipos de datos admitidas y la asignación de tipo de datos en bases de datos específicas (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Para más información sobre cómo asignar tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a tipos de datos administrados, vea [Trabajar con tipos de datos del flujo de datos](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Solución de problemas del origen de ADO NET  
 Puede registrar las llamadas que el origen de ADO NET realiza a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar los problemas relacionados con la carga de datos de orígenes de datos externos que realiza el origen de ADO NET. Para registrar las llamadas realizadas por el origen de ADO NET a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>Configuración del origen de ADO NET  
 Para configurar el origen de ADO NET, debe proporcionar la instrucción SQL que define el conjunto de resultados. Por ejemplo, un origen de ADO NET que se conecta a la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] y utiliza la instrucción SQL `SELECT * FROM Production.Product` extrae todas las filas de la tabla **Production.Product** y proporciona el conjunto de datos a un componente de nivel inferior.  
  
> [!NOTE]  
>  Cuando use una instrucción SQL para invocar un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
> [!NOTE]  
>  Si usa una instrucción SQL para ejecutar un procedimiento almacenado y el paquete genera el error siguiente, es posible que pueda solucionar el error si agrega la instrucción **SET FMTONLY OFF** antes de la instrucción EXEC.  
>   
>  **La columna <column_name> no se encuentra en el origen de datos.**  
  
 Este origen de ADO NET utiliza un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para conectarse a un origen de datos. El administrador de conexiones especifica el proveedor .NET. Para más información, consulte [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 El origen de ADO NET tiene una salida normal y una salida de errores.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>Editor de orígenes de ADO NET (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de orígenes de ADO NET** para seleccionar el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del origen de ADO NET, vea [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tiene el origen de ADO NET.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de ADO NET.  
  
3.  En el **Editor de orígenes de ADO NET**, haga clic en **Administrador de conexiones**.  
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones de ADO.NET**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Recupera datos de una tabla o vista del origen de datos [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .|  
|Comando SQL|Recupera datos del origen de datos [!INCLUDE[vstecado](../../includes/vstecado-md.md)] mediante una consulta SQL.|  
  
 **Versión preliminar**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<value too big to display> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] y el último, cuando se utiliza el proveedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
### <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Browse**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
## <a name="ado-net-source-editor-columns-page"></a>Editor de orígenes de ADO NET (página Columnas)
  Use la página **Columnas** del cuadro de diálogo **Editor de orígenes de ADO NET** para asignar una columna de salida a cada columna externa (origen).  
  
 Para obtener más información acerca del origen de ADO NET, vea [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir la página Columnas**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tiene el origen de ADO NET.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de ADO NET.  
  
3.  En el **Editor de orígenes de ADO NET**, haga clic en **Columnas**.  
  
### <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Muestra las columnas externas (origen) en el orden en que se verán cuando configure componentes que utilizan datos de este origen.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre proporcionado se mostrará en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="ado-net-source-editor-error-output-page"></a>Editor de orígenes de ADO NET (página Salida de error)
  Utilice la página **Salida de error** del cuadro de diálogo **Editor de orígenes de ADO NET** para seleccionar las opciones de control de errores y para establecer las propiedades en las columnas de salida de errores.  
  
 Para obtener más información acerca del origen de ADO NET, vea [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir la página Salida de error**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tiene el origen de ADO NET.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de ADO NET.  
  
3.  En el **Editor de orígenes de ADO NET**, haga clic en **Salida de error**.  
  
### <a name="options"></a>Opciones  
 **Entrada/salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Muestra las columnas externas (origen) que se han seleccionado en la página **Administrador de conexiones** del cuadro de diálogo **Editor de orígenes de ADO NET** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Destino de DataReader](../../integration-services/data-flow/datareader-destination.md)   
 [Destino de ADO NET](../../integration-services/data-flow/ado-net-destination.md)   
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  
