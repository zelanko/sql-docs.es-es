---
title: Origen OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.oledbsource.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 077ccf4ad3793db7bbf067460f42cf8c8e98b427
ms.sourcegitcommit: d463f543e8db4a768f8e9736ff28fedb3fb17b9f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/22/2018
ms.locfileid: "36324679"
---
# <a name="ole-db-source"></a>Origen de OLE DB
  El origen de OLE DB extrae datos de varias bases de datos relacionales compatibles con OLE DB mediante una tabla de base de datos, una vista o un comando SQL. Por ejemplo, el origen de OLE DB puede extraer datos de tablas de bases de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El origen de OLE DB proporciona cuatro modos de acceso distintos para extraer datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
-   Los resultados de una instrucción SQL, almacenados en una variable.  
  
> [!NOTE]  
>  Cuando use una instrucción SQL para invocar un procedimiento almacenado que devuelve resultados de una tabla temporal, use la opción WITH RESULT SETS para definir los metadatos del conjunto de resultados.  
  
 Si utiliza una consulta con parámetros, puede asignar variables a parámetros para especificar los valores para parámetros individuales en las instrucciones SQL.  
  
 Este origen utiliza un administrador de conexiones OLE DB para conectar con el origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
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
  
 El procedimiento almacenado espera las variables `@StartProductID` y `@CheckDate`para proporcionar valores de parámetros. El orden en el que los parámetros aparecen en la lista **Asignaciones** es irrelevante. El único requisito es que los nombres de parámetros coincidan con los nombres de variables en el procedimiento almacenado, incluido el signo @.  
  
### <a name="mapping-parameters-to-variables"></a>Asignar parámetros a variables  
 Los parámetros se asignan a variables que proporcionan los valores de parámetros en tiempo de ejecución. Las variables son generalmente variables definidas por el usuario, aunque también puede usar variables del sistema que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Si utiliza variables definidas por el usuario, asegúrese de establecer el tipo de datos en un tipo que sea compatible con el tipo de datos de la columna a la que hace referencia el parámetro asignado. Para más información, vea [Integration Services &#40;SSIS&#41; Variables](../integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Solucionar problemas del origen de OLE DB  
 Puede registrar las llamadas realizadas por el origen de OLE DB a proveedores de datos externos. Puede utilizar esta capacidad de registro para solucionar problemas relacionados con la carga de datos desde orígenes de datos externos que realiza el origen de OLE DB. Para registrar las llamadas realizadas por el origen de OLE DB a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para obtener más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Configurar el origen de OLE DB  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de origen de OLE DB** , haga clic en uno de los temas siguientes:  
  
-   [Editor de origen de OLE DB &#40;página Administrador de conexiones&#41;](../ole-db-source-editor-connection-manager-page.md)  
  
-   [Editor de origen de OLE DB &#40;página columnas&#41;](../ole-db-source-editor-columns-page.md)  
  
-   [Editor de origen de OLE DB &#40;página de salida de Error&#41;](../ole-db-source-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas de OLE DB](ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Extraer datos mediante el origen de OLE DB](ole-db-source.md)  
  
-   [Asignar parámetros de consulta a variables en un componente de flujo de datos](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo wiki, sobre [SSIS con conectores Oracle](http://go.microsoft.com/fwlink/?LinkId=220670), en social.technet.microsoft.com.  
  
## <a name="see-also"></a>Vea también  
 [Destino de OLE DB](ole-db-destination.md)   
 [Servicios de integración &#40;SSIS&#41; Variables](../integration-services-ssis-variables.md)   
 [Flujo de datos](data-flow.md)  
  
  