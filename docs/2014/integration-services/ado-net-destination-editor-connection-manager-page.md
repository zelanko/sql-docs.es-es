---
title: Editor de destinos de ADO NET (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.connection.f1
ms.assetid: a3b11286-32c8-40e1-8ae7-090e2590345a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 611436db1ea4a69a5c33c7bc2c3c9e92f2a350a3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62772306"
---
# <a name="ado-net-destination-editor-connection-manager-page"></a>Editor de destinos de ADO NET (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destinos de ADO NET** para seleccionar la conexión [!INCLUDE[vstecado](../includes/vstecado-md.md)] del destino. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del destino de ADO NET, vea [ADO NET Destination](data-flow/ado-net-destination.md).  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que tiene el destino de ADO NET.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de ADO NET.  
  
3.  En el **Editor de destinos de ADO NET**, haga clic en **Administrador de conexiones**.  
  
## <a name="static-options"></a>Opciones estáticas  
 **Connection manager**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Configurar el administrador de conexiones ADO.NET** .  
  
 **Usar una tabla o una vista**  
 Seleccione una tabla o vista de la lista o cree una tabla haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree un tabla o una vista mediante el cuadro de diálogo **Crear tabla** .  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . La vista previa puede mostrar hasta 200 filas.  
  
 **Usar inserción masiva cuando esté disponible**  
 Especifique si se debe usar la interfaz <xref:System.Data.SqlClient.SqlBulkCopy> para mejorar el rendimiento de las operaciones de inserción masiva.  
  
 Solamente los proveedores ADO.NET que devuelven un objeto <xref:System.Data.SqlClient.SqlConnection> admiten el uso de la interfaz <xref:System.Data.SqlClient.SqlBulkCopy> . El Proveedor de datos .NET para SQL Server (SqlClient) devuelve un objeto <xref:System.Data.SqlClient.SqlConnection> y, por otra parte, un proveedor personalizado puede devolver un objeto <xref:System.Data.SqlClient.SqlConnection> .  
  
 Puede usar el proveedor de datos .NET para SQL Server (SqlClient) para conectarse a [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)].  
  
 Si selecciona **Use bulk insert when available**(Usar la inserción masiva cuando esté disponible) y establece la opción **Error** en **Redirect the row**(Redirigir la fila), el lote de datos que el destino redirige a la salida de error puede incluir filas correctas. Para obtener más información sobre cómo administrar errores en operaciones masivas, vea [Control de errores en los datos](data-flow/error-handling-in-data.md). Para obtener más información sobre la opción **Error** , vea [ADO NET Destination Editor &#40;Error Output Page&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md).  
  
> [!NOTE]  
>  Si una tabla de origen de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o de Sybase incluye una columna de identidad, es necesario que use las tareas Ejecutar SQL para ejecutar una instrucción SET IDENTITY_INSERT antes y después del destino de ADO NET. La propiedad de la columna de identidad especifica un valor incremental de la columna. La instrucción SET IDENTITY_INSERT permite insertar valores explícitos en la columna de identidad. Para ejecutar las instrucciones CREATE TABLE y SET IDENTITY en la misma conexión de bases de datos, establezca en `RetainSameConnection` la propiedad `True` del administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)]. Asimismo, use el mismo administrador de conexiones [!INCLUDE[vstecado](../includes/vstecado-md.md)] para las tareas Ejecutar SQL y el destino de ADO NET.  
>   
>  Para obtener más información, vea [SET IDENTITY_INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-identity-insert-transact-sql) y [IDENTITY &#40;propiedad de Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property).  
  
## <a name="external-resources"></a>Recursos externos  
 Artículo técnico, sobre cómo [cargar datos en Windows Azure SQL Database de la forma más rápida](https://go.microsoft.com/fwlink/?LinkId=244333), en sqlcat.com  
  
## <a name="see-also"></a>Vea también  
 [Editor de destinos de ADO NET &#40;página Asignaciones&#41;](../../2014/integration-services/ado-net-destination-editor-mappings-page.md)   
 [Editor de destinos de ADO NET &#40;página Salida de error&#41;](../../2014/integration-services/ado-net-destination-editor-error-output-page.md)   
 [Administrador de conexiones ADO.NET](connection-manager/ado-net-connection-manager.md)   
 [Tarea Ejecutar SQL](control-flow/execute-sql-task.md)  
  
  
