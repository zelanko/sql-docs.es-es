---
title: Propiedades personalizadas de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5307d2507562a9a9957fb2bb7431248b4196954a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431712"
---
# <a name="ole-db-custom-properties"></a>Propiedades personalizadas de OLE DB
  **Propiedades personalizadas de origen**  
  
 El origen de OLE DB tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de OLE DB. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Entero|Modo que se usa para tener acceso a la base de datos. Los valores posibles son **Open Rowset**, **Open Rowset from variable**, `SQL Command` y **SQL Command from variable**. El valor predeterminado es **Open Rowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad `DefaultCodePage` para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es `False`.|  
|CommandTimeout|Entero|Número de segundos que tienen que transcurrir antes de que un comando supere el tiempo de espera. El valor 0 indica un tiempo infinito.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de OLE DB**, pero se puede definir con el **Editor avanzado**.|  
|DefaultCodePage|Entero|Página de códigos que se usa cuando no hay información disponible de la misma en el origen de datos.|  
|OpenRowset|String|Nombre del objeto de base de datos que se usa para abrir un conjunto de filas.|  
|OpenRowsetVariable|String|Variable que contiene el objeto del objeto de base de datos que se usa para abrir un conjunto de filas.|  
|ParameterMapping|String|Asignación de los parámetros del comando SQL a variables.|  
|SqlCommand|String|Comando SQL que se va a ejecutar.|  
|SqlCommandVariable|String|Variable que contiene el comando SQL que se va a ejecutar.|  
  
 La salida y las columnas de salida del origen de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Source](ole-db-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de OLE DB tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino OLE DB. Todas las propiedades son de lectura y escritura.  
  
> [!NOTE]  
>  Las opciones de carga rápida enumeradas aquí (FastLoadKeepIdentity, FastLoadKeepNulls y FastLoadOptions) corresponden a las propiedades con nombre similar que expone la interfaz `IRowsetFastLoad` implementada por el proveedor Microsoft OLE DB para SQL Server (SQLOLEDB). Para obtener más información, busque IRowsetFastLoad en la MSDN Library.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica cómo tiene acceso el destino a su base de datos de destino.<br /><br /> Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> `OpenRowset`(0): se proporciona el nombre de una tabla o vista.<br />`OpenRowset from Variable`(1): se proporciona el nombre de una variable que contiene el nombre de una tabla o vista.<br />`OpenRowset Using Fastload`(3): se proporciona el nombre de una tabla o vista.<br />`OpenRowset Using Fastload from Variable`(4): se proporciona el nombre de una variable que contiene el nombre de una tabla o vista.<br />`SQL Command`(2): se proporciona una instrucción SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad `DefaultCodePage` para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es `False`.|  
|CommandTimeout|Entero|Número máximo de segundos que el comando SQL se puede ejecutar antes de superar el tiempo de espera. Un valor de 0 indica un tiempo infinito. El valor predeterminado de esta propiedad es 0.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de destino OLE DB**, pero se puede definir con el **Editor avanzado**.|  
|DefaultCodePage|Entero|Página de códigos predeterminada asociada al destino OLE DB.|  
|FastLoadKeepIdentity|Boolean|Valor que especifica si se copian los valores de identidad cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es `False`. Esta propiedad corresponde a la propiedad OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) `SSPROP_FASTLOADKEEPIDENTITY` .|  
|FastLoadKeepNulls|Boolean|Valor que especifica si se copian los valores Null cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es `False`. Esta propiedad corresponde a la propiedad OLE DB [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) `SSPROP_FASTLOADKEEPNULLS` .|  
|FastLoadMaxInsertCommitSize|Entero|Valor que especifica el tamaño de lote que el destino OLE DB intenta confirmar en operaciones de carga rápida. El valor predeterminado, **0**, indica una operación de confirmación única después de que se procesen todas las filas.|  
|FastLoadOptions|String|Colección de opciones de carga rápida. Las opciones de carga rápida incluyen el bloqueo de las tablas y la comprobación de las restricciones. Puede especificar una, ambas o ninguna. Esta propiedad corresponde a la propiedad OLE DB IRowsetFastLoad `SSPROP_FASTLOADOPTIONS` y acepta opciones de cadena como `CHECK_CONSTRAINTS` y `TABLOCK` .<br /><br /> Nota: Algunas opciones de esta propiedad no están disponibles en el **Editor de destino de Excel**, pero pueden definirse con el **Editor avanzado**.|  
|OpenRowset|String|Cuando AccessMode es `OpenRowset` , el nombre de la tabla o vista a la que tiene acceso el OLE DB de destino.|  
|OpenRowsetVariable|String|Cuando AccessMode es `OpenRowset from Variable` , el nombre de la variable que contiene el nombre de la tabla o vista a la que el destino de OLE DB tiene acceso.|  
|SqlCommand|String|Cuando AccessMode es `SQL Command` , la instrucción de Transact-SQL que el destino OLE DB utiliza para especificar las columnas de destino de los datos.|  
  
 La entrada y las columnas de entrada del destino de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Destination](ole-db-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](../common-properties.md)  
  
  
