---
title: Destino de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdest.f1
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: a0227cd8-6944-4547-87e8-7b2507e26442
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 818f78cd0b38aba0a7201eb28f49eb573ba32672
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770730"
---
# <a name="sql-server-destination"></a>SQL Server, destino
  El destino de SQL Server se conecta a una base de datos local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y realiza una carga masiva de datos en tablas y vistas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No se puede usar el destino de SQL Server en paquetes con acceso a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor remoto. En su lugar, los paquetes deben utilizar el destino de OLE DB. Para más información, consulte [OLE DB Destination](ole-db-destination.md).  
  
## <a name="permissions"></a>Permisos  
 Los usuarios que ejecutan paquetes que incluyen el destino de SQL Server deben tener el permiso Crear objetos globales. Para otorgar este permiso a los usuarios, utilice la herramienta Directiva de seguridad local que se abre desde el menú **Herramientas administrativas** . Si recibe un mensaje de error al ejecutar un paquete que utiliza el destino de SQL Server, asegúrese de que la cuenta que ejecuta el paquete tiene el permiso Crear objetos globales.  
  
## <a name="bulk-inserts"></a>Inserciones masivas  
 Si se intenta usar el destino de SQL Server para realizar una carga masiva de datos en una base de datos remota de SQL Server, puede recibir un mensaje de error similar al siguiente: "Hay un registro OLE DB disponible". Origen : "Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client" Hresult: 0x80040E14 Descripción: "No se pudo realizar la carga masiva porque el objeto de asignación de archivos "Global\DTSQLIMPORT" no se pudo abrir. Código de error del sistema operativo 2 (El sistema no encuentra el archivo especificado). Asegúrese de que tiene acceso a un servidor local mediante Seguridad de Windows."".  
  
 El destino de SQL Server ofrece la misma inserción de datos de alta velocidad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que proporciona la tarea Inserción masiva. En cambio, al usar el destino de SQL Server, un paquete puede aplicar transformaciones a los datos de las columnas antes de que estos se carguen en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para cargar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es recomendable usar el destino de SQL Server en lugar del destino de OLE DB.  
  
### <a name="bulk-insert-options"></a>Opciones de inserción masiva  
 Si el destino de SQL Server usa el modo de acceso de datos de carga rápida, puede especificar las siguientes opciones de carga rápida:  
  
-   Mantener los valores de identidad del archivo de datos importado o usar valores exclusivos asignados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Conservar los valores NULL durante la operación de carga masiva.  
  
-   Comprobar las restricciones en la tabla o vista de destino durante la operación de importación masiva.  
  
-   Adquirir un bloqueo de nivel de tabla durante la operación de carga masiva.  
  
-   Ejecutar desencadenadores de inserción definidos en la tabla de destino durante la operación de carga masiva.  
  
-   Especificar el número de la primera fila en la entrada que se debe cargar durante la operación de inserción masiva.  
  
-   Especificar el número de la última fila en la entrada que se debe cargar durante la operación de inserción masiva.  
  
-   Especificar el número máximo de errores que pueden producirse antes de que se cancele la operación de carga masiva. Cada fila que no puede importarse se cuenta como un error.  
  
-   Especificar las columnas de la entrada que contienen datos ordenados.  
  
 Para obtener más información sobre las opciones de carga masiva, vea [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
#### <a name="performance-improvements"></a>Mejoras de rendimiento  
 Para mejorar el rendimiento de una inserción masiva y el acceso a los datos de tablas durante la operación de inserción masiva, se deben cambiar las opciones predeterminadas de la manera siguiente:  
  
-   No comprobar las restricciones en la tabla o vista de destino durante la operación de importación masiva.  
  
-   No ejecutar desencadenadores de inserción definidos en la tabla de destino durante la operación de carga masiva.  
  
-   No aplicar un bloqueo a la tabla. De esta manera, la tabla sigue disponible para otros usuarios y aplicaciones durante la operación de inserción masiva.  
  
## <a name="configuration-of-the-sql-server-destination"></a>Configuración del destino de SQL Server  
 Puede configurar el destino de SQL Server de las maneras siguientes:  
  
-   Especificar la tabla o vista en la que se debe realizar la carga masiva de los datos.  
  
-   Personalizar la operación de carga masiva especificando opciones tales como si se deben comprobar restricciones.  
  
-   Especificar si todas las filas se confirman en un lote o establecer el número máximo de filas que se confirman como un lote.  
  
-   Especificar un tiempo de espera para la operación de carga masiva.  
  
 Este destino usa un administrador de conexiones de OLE DB para conectarse a un origen de datos y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también proporciona el objeto de origen de datos desde el que se puede crear un administrador de conexiones de OLE DB. Esto hace que los orígenes de datos y vistas del origen de datos queden a disposición del destino de SQL Server.  
  
 El destino de SQL Server tiene una entrada. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor de destino de SQL Server** , haga clic en uno de los siguientes temas:  
  
-   [Editor de destino de SQL &#40;página Administrador de conexiones&#41;](../sql-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de SQL &#40;página Asignaciones&#41;](../sql-destination-editor-mappings-page.md)  
  
-   [Editor de destino de SQL &#40;página Avanzadas&#41;](../sql-destination-editor-advanced-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas del destino SQL Server](sql-server-destination-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Realizar una carga masiva de datos mediante el destino de SQL Server](sql-server-destination.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Realizar una carga masiva de datos mediante el destino de SQL Server](sql-server-destination.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   Artículo técnico, sobre la [posible aparición del error "No se puede preparar la inserción masiva de SSIS para la inserción de datos" en sistemas habilitados para UAC](https://go.microsoft.com/fwlink/?LinkId=199482), en support.microsoft.com.  
  
-   Artículo técnico, [The Data Loading Performance Guide](https://go.microsoft.com/fwlink/?LinkId=233700), en msdn.microsoft.com.  
  
-   Artículo técnico [Usar SQL Server Integration Services para cargar datos de forma masiva](https://go.microsoft.com/fwlink/?LinkId=233701), en simple-talk.com.  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](data-flow.md)  
  
  
