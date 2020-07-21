---
title: Destino de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdest.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5227175e80db3a8f31a8b8db8c3d6bee3061bae
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431922"
---
# <a name="ole-db-destination"></a>Destino de OLE DB
  El destino de OLE DB carga datos en una serie de bases de datos compatibles con OLE DB que usan una tabla o vista de base de datos o un comando SQL. Por ejemplo, un origen de OLE DB puede cargar datos en tablas en bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El destino de OLE DB proporciona cinco modos diferentes de acceso a los datos para cargar datos:  
  
-   Una tabla o vista. Puede especificar una tabla o vista existentes, o puede crear una nueva tabla.  
  
-   Una tabla o vista usando opciones de carga rápida. Puede especificar una tabla existente, o puede crear una nueva tabla.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Una tabla o vista especificada en una variable usando opciones de carga rápida.  
  
-   Los resultados de una instrucción SQL.  
  
> [!NOTE]  
>  El destino de OLE DB no admite parámetros. Si tiene que ejecutar una instrucción INSERT con parámetros, puede usar la transformación Comando de OLE DB. Para más información, consulte [OLE DB Command Transformation](transformations/ole-db-command-transformation.md).  
  
 Cuando el destino de OLE DB carga datos que utilizan un juego de caracteres de doble byte (DBCS), los datos se pueden dañar si el modo del acceso a datos no usa la opción de carga rápida y si el administrador de conexiones OLE DB utiliza el proveedor OLE DB de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Para garantizar la integridad de datos de DBCS es necesario configurar el administrador de conexiones OLE DB para que use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client o uno de los modos de acceso de carga rápida: **Carga rápida de tabla o vista** o **Carga rápida de variable de nombre de tabla o nombre de vista**. Ambas opciones están disponibles en el cuadro de diálogo **Editor de destino de OLE DB** . Al programar el [!INCLUDE[ssIS](../../includes/ssis-md.md)] modelo de objetos, debe establecer la propiedad AccessMode en `OpenRowset Using FastLoad` , o `OpenRowset Using FastLoad From Variable` .  
  
> [!NOTE]  
>  Si usa el cuadro de diálogo **Editor de destino de OLE DB** en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para crear la tabla de destino en la que el destino de OLE DB inserta los datos, puede tener que seleccionar la tabla nueva manualmente. La necesidad de selección manual se produce cuando un proveedor OLE DB, como el proveedor OLE DB para DB2 agrega automáticamente identificadores de esquema al nombre de la tabla.  
  
> [!NOTE]  
>  La instrucción CREATE TABLE que genera el cuadro de diálogo **Editor de destino de OLE DB** puede requerir una modificación, en función del tipo de destino. Por ejemplo, algunos destinos no admiten tipos de datos que utiliza la instrucción CREATE TABLE.  
  
 Este destino usa un administrador de conexiones OLE DB para conectarse a un origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] también proporciona el objeto de origen de datos desde el que puede crear un administrador de conexiones OLE DB para poner los orígenes de datos y las vistas del origen de datos a disposición del destino de OLE DB.  
  
 Un destino de OLE DB incluye asignaciones entre columnas de entrada y columnas en el origen de datos de destino. No es necesario asignar columnas de entrada a todas las columnas de destino, pero, según las propiedades de las columnas de destino, pueden producirse errores si no se asignan columnas de entrada a las columnas de destino. Por ejemplo, si una columna de destino no permite valores NULL, se debe asignar una columna de entrada a esa columna. Además, los tipos de datos de las columnas asignadas deben ser compatibles. Por ejemplo, no se puede asignar una columna de entrada que tiene un tipo de datos de cadena a una columna de destino con un tipo de datos numérico.  
  
 El destino de OLE DB tiene una entrada normal y una salida de error.  
  
 Para obtener más información sobre los tipos de datos, vea [Integration Services tipos de datos](integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Opciones de carga rápida  
 Si el destino de OLE DB usa el modo de acceso a datos de carga rápida, puede especificar las siguientes opciones de carga rápida en la interfaz de usuario del **Editor de destino de OLE DB**para el destino:  
  
-   Mantener los valores de identidad del archivo de datos importado o usar valores exclusivos asignados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Conservar un valor NULL durante la operación de carga masiva.  
  
-   Comprobar las restricciones en la tabla o vista de destino durante la operación de importación masiva.  
  
-   Adquirir un bloqueo de nivel de tabla durante la operación de carga masiva.  
  
-   Especificar la cantidad de filas del lote y el tamaño de confirmación.  
  
 Algunas opciones de carga rápida están almacenadas en propiedades específicas del destino de OLE DB. Por ejemplo, FastLoadKeepIdentity especifica si se mantienen los valores de identificación, FastLoadKeepNulls especifica si se mantienen los valores nulos y FastLoadMaxInsertCommitSize especifica el número de filas que se confirmarán como un lote. Otras opciones de carga rápida se almacenan en una lista separada por comas, en la propiedad FastLoadOptions. Si el OLE DB destino utiliza todas las opciones de carga rápida que se almacenan en FastLoadOptions y se enumeran en el cuadro de diálogo **Editor de destino OLE DB** , el valor de la propiedad se establece en `TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000` . El valor 1000 indica que el destino se configura para usar lotes de 1000 filas.  
  
> [!NOTE]  
>  Los errores de restricciones en el destino provocan el error del lote completo de las filas definidas por FastLoadMaxInsertCommitSize.  
  
 Además de las opciones de carga rápida que se muestran en el cuadro de diálogo **Editor de destino de OLE DB** , puede configurar el destino de OLE DB para usar las siguientes opciones de carga masiva al escribir las opciones en la propiedad FastLoadOptions del cuadro de diálogo **Editor avanzado** .  
  
|Opción de carga rápida|Descripción|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Especifica el tamaño en kilobytes para insertar. La opción tiene el formato `KILOBYTES_PER_BATCH`  =  \<positive integer value**> * *.|  
|FIRE_TRIGGERS|Especifica si se activan los desencadenadores en la tabla de inserción. La opción tiene la forma **FIRE_TRIGGERS**. La presencia de la opción indica que se activan los desencadenadores.|  
|ORDER|Especifica cómo se ordenan los datos de entrada. La opción tiene el orden de formulario \<column name> ASC&#124;desc. Se puede enumerar cualquier cantidad de columnas (el orden es opcional). Si se omite el orden, la operación de inserción presupone que los datos no están ordenados.<br /><br /> Nota: El rendimiento puede mejorar si se utiliza la opción ORDER para ordenar los datos de entrada según el índice agrupado de la tabla.|  
  
 Las palabras clave de [!INCLUDE[tsql](../../includes/tsql-md.md)] se suelen escribir en mayúsculas, aunque las palabras clave no distinguen entre mayúsculas y minúsculas.  
  
 Para más información sobre las opciones de carga rápida, vea [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Solucionar problemas del destino de OLE DB  
 Puede registrar las llamadas realizadas por el destino OLE DB a proveedores de datos externos. Puede utilizar esta nueva capacidad de registro para solucionar problemas relacionados con el almacenamiento de datos en orígenes de datos externos que realiza el destino OLE DB. Para registrar las llamadas realizadas por el destino OLE DB a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Configurar el destino de OLE DB  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden establecer en el cuadro de diálogo **Editor de destino de OLE DB** , haga clic en uno de los siguientes temas:  
  
-   [Editor de destino de OLE DB &#40;página Administrador de conexiones&#41;](../ole-db-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino de OLE DB &#40;página Asignaciones&#41;](../ole-db-destination-editor-mappings-page.md)  
  
-   [Editor de destino de OLE DB &#40;página Salida de error&#41;](../ole-db-destination-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../common-properties.md)  
  
-   [Propiedades personalizadas de OLE DB](ole-db-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer valores de propiedades, haga clic en uno de los temas siguientes:  
  
-   [Cargar datos mediante el destino de OLE DB](ole-db-destination.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Origen de OLE DB](ole-db-source.md)  
  
 [Variables de Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md)  
  
 [Flujo de datos](data-flow.md)  
  
  
