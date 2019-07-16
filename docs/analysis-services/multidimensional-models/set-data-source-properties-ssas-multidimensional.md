---
title: Establecer las propiedades del origen de datos (SSAS Multidimensional) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c9053154d01616f1ff39c67a85d1319e1d02625f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208473"
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>Establecer propiedades de origen de datos (SSAS multidimensional)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], un origen de datos especifica una conexión a un almacenamiento de datos externo o a la base de datos relacional que proporciona datos a un modelo multidimensional. Las propiedades del origen de datos determinan la cadena de conexión, un intervalo de tiempo de espera, el número máximo de conexiones y el nivel de aislamiento de transacciones.  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>Establecer las propiedades del origen de datos en SQL Server Data Tools  
  
1.  Haga doble clic en un origen de datos en el explorador de soluciones para abrir el Diseñador de origen de datos.  
  
2.  Haga clic en la pestaña **Información de suplantación** en el Diseñador de origen de datos. Para más información sobre cómo crear un origen de datos, vea [Crear un origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
## <a name="set-data-source-properties-in-management-studio"></a>Establecer las propiedades del origen de datos en Management Studio  
  
1.  Expanda la carpeta de la base de datos, abra la carpeta **Origen de datos** y, debajo del nombre de la base de datos, haga clic con el botón derecho en un origen de datos en el **Explorador de objetos** y seleccione **Propiedades**.  
  
2.  Opcionalmente, modifique el nombre, la descripción o la opción de suplantación. Para más información, vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).  
  
## <a name="data-source-properties"></a>Propiedades del origen de datos  
  
|Término|Definición|  
|----------|----------------|  
|**Nombre, identificador, descripción**|El nombre, el identificador y la descripción se utilizan para identificar y describir el objeto de origen de datos en el modelo multidimensional.<br /><br /> El nombre y la descripción se pueden especificar en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] después de implementar o procesar la solución.<br /><br /> El identificador se genera cuando se crea el objeto. Aunque puede modificar con facilidad el nombre y la descripción, los identificadores son de solo lectura y no deben cambiarse. Un identificador de objeto fijo conserva las dependencias de objeto y las referencias en el modelo.|  
|**Marca de tiempo de creación**|Esta propiedad de solo lectura aparece en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Muestra la fecha y hora en que se creó el origen de datos.|  
|**Última actualización de esquema**|Esta propiedad de solo lectura aparece en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Muestra la fecha y hora en que se actualizaron por última vez los metadatos del origen de datos. Se actualiza este valor al implementar la solución.|  
|**Tiempo de espera de la consulta**|Especifica cuánto tiempo una solicitud de conexión se intentó antes de quitar.<br /><br /> Escriba el tiempo de espera de la columna con el siguiente formato:<br /><br /> *\<Horas >* : *\<minutos >* : *\<segundos >*<br /><br /> Esta propiedad se puede reemplazar por la propiedad del servidor de **DatabaseConnectionPoolTimeoutConnection** . Si la propiedad de servidor es menor, se utilizará en lugar de **Tiempo de espera de consulta**.<br /><br /> Para más información sobre la propiedad **Tiempo de espera de la consulta** , vea <xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>. Para obtener más información acerca de la propiedad de servidor, vea [OLAP Properties](../../analysis-services/server-properties/olap-properties.md).|  
|**Cadena de conexión**|Especifica la ubicación física de una base de datos que proporciona datos a un modelo multidimensional y el proveedor de datos utilizado para la conexión. Esta información se proporciona a una biblioteca cliente que realiza la solicitud de conexión. El proveedor determina qué propiedades se pueden establecer en la cadena de conexión.<br /><br /> La cadena de conexión se genera utilizando la información que se proporciona en el cuadro de diálogo **Administrador de conexiones** . También puede ver y modificar la cadena de conexión en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] en la página de propiedades del origen de datos.<br /><br /> Para una base de datos de SQL Server, una cadena de conexión que contiene un **identificador de usuario** indica la autenticación de base de datos, mientras que una conexión que contiene **Integrated Security=SSPI** indica la autenticación de Windows.<br /><br /> Puede cambiar el nombre de servidor o la base de datos si la base de datos se movió a una nueva ubicación. Asegúrese de comprobar que las credenciales especificadas actualmente para la conexión están asignadas a un inicio de sesión de base de datos.|  
|**Número máximo de conexiones**|Especifica el número máximo de conexiones permitidas por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectarse al origen de datos. Si varias conexiones son necesarias, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] esperará hasta que una conexión esté disponible. El valor predeterminado es 10. Al restringir el número de conexiones, se garantiza que el origen de datos externo no está sobrecargado con las solicitudes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Aislamiento**|Especifica el bloqueo y el comportamiento de las versiones de filas de los comandos SQL emitidos por una conexión a una base de datos relacional. Los valores válidos son ReadCommitted o Snapshot. El valor predeterminado es ReadCommitted, que especifica que los datos deben confirmarse antes de que se lean, lo que evita la lectura de datos no actualizados. La instantánea especifica que las lecturas son de una instantánea de datos no confirmados. Para más información sobre el nivel de aislamiento en SQL Server, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).|  
|**Proveedor administrado**|Si el origen de datos utiliza un proveedor administrado, muestra el nombre del proveedor administrado, como System.Data.SqlClient o System.Data.OracleClient.<br /><br /> Si el origen de datos no utiliza un proveedor administrado, la propiedad muestra una cadena vacía.<br /><br /> Esta propiedad es de solo lectura en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para cambiar el proveedor utilizado en la conexión, modifique la cadena de conexión.|  
|**Información de suplantación**|Especifica la identidad de Windows con la que se ejecuta [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al conectarse a un origen de datos que usa la autenticación de Windows. Las opciones incluyen el uso de un conjunto predefinido de credenciales de Windows, la cuenta de servicio, la identidad del usuario actual o una opción heredada que puede ser útil si el modelo contiene objetos de origen de datos. Para más información, vea [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md).<br /><br /> En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], la lista de valores válidos incluyen los siguientes:<br /><br /> **ImpersonateAccount** (usar un nombre de usuario y una contraseña de Windows específicos para conectarse con el origen de datos).<br /><br /> **ImpersonateServiceAccount** (usar la identidad de seguridad de la cuenta de servicio para conectarse con el origen de datos). Este es el valor predeterminado.<br /><br /> **ImpersonateCurrentUser** (usar la identidad de seguridad del usuario actual para conectarse con el origen de datos). Esta opción solo es válida para las consultas de minería de datos que recuperan datos de un almacén de datos o de datos externos; no la elija para las conexiones de datos utilizadas para procesar, cargar o reescribir en una base de datos multidimensional.<br /><br /> **Inherit** o **default** (usar la configuración de suplantación de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene este objeto de origen de datos). Las propiedades de la base de datos incluyen opciones de suplantación.|  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Crear un origen de datos &#40;SSAS multidimensional&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
