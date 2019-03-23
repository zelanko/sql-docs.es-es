---
title: Propiedades personalizadas de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 996acc5f8e9b47af683c8d8376515f7f59e63120
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374932"
---
# <a name="ole-db-custom-properties"></a>Propiedades personalizadas de OLE DB
  **Propiedades personalizadas de origen**  
  
 El origen de OLE DB tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de OLE DB. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|Modo que se usa para tener acceso a la base de datos. Los valores posibles son **Open Rowset**, **Open Rowset from Variable**, `SQL Command`, y **comando SQL de Variable**. El valor predeterminado es **Open Rowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad `DefaultCodePage` para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es `False`.|  
|CommandTimeout|Integer|Número de segundos que tienen que transcurrir antes de que un comando supere el tiempo de espera. El valor 0 indica un tiempo infinito.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de OLE DB**, pero se puede establecer utilizando la **Editor avanzado**.|  
|DefaultCodePage|Integer|Página de códigos que se usa cuando no hay información disponible de la misma en el origen de datos.|  
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
|AccessMode|Integer (enumeración)|Valor que especifica cómo tiene acceso el destino a su base de datos de destino.<br /><br /> Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> `OpenRowset` (0): Proporcione el nombre de una tabla o vista.<br />`OpenRowset from Variable` (1): Proporcione el nombre de una variable que contiene el nombre de una tabla o vista.<br />`OpenRowset Using Fastload` (3): Proporcione el nombre de una tabla o vista.<br />`OpenRowset Using Fastload from Variable` (4): Proporcione el nombre de una variable que contiene el nombre de una tabla o vista.<br />`SQL Command` (2): Proporcione una instrucción SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad `DefaultCodePage` para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es `False`.|  
|CommandTimeout|Integer|Número máximo de segundos que el comando SQL se puede ejecutar antes de superar el tiempo de espera. Un valor de 0 indica un tiempo infinito. El valor predeterminado de esta propiedad es 0.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de destino de OLE DB**, pero se puede establecer utilizando la **Editor avanzado**.|  
|DefaultCodePage|Integer|Página de códigos predeterminada asociada al destino OLE DB.|  
|FastLoadKeepIdentity|Boolean|Valor que especifica si se copian los valores de identidad cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es `False`. Esta propiedad se corresponde con OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) propiedad `SSPROP_FASTLOADKEEPIDENTITY`.|  
|FastLoadKeepNulls|Boolean|Valor que especifica si se copian los valores Null cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es `False`. Esta propiedad se corresponde con OLE DB [IRowsetFastLoad &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) propiedad `SSPROP_FASTLOADKEEPNULLS`.|  
|FastLoadMaxInsertCommitSize|Integer|Valor que especifica el tamaño de lote que el destino OLE DB intenta confirmar en operaciones de carga rápida. El valor predeterminado, **0**, indica una operación de confirmación única después de que se procesen todas las filas.|  
|FastLoadOptions|String|Colección de opciones de carga rápida. Las opciones de carga rápida incluyen el bloqueo de las tablas y la comprobación de las restricciones. Puede especificar una, ambas o ninguna. Esta propiedad se corresponde con la propiedad IRowsetFastLoad de OLE DB `SSPROP_FASTLOADOPTIONS` y acepta opciones de cadena como `CHECK_CONSTRAINTS` y `TABLOCK`.<br /><br /> Nota: Algunas opciones para esta propiedad no están disponibles en el **Editor de destino de Excel**, pero se puede establecer utilizando la **Editor avanzado**.|  
|OpenRowset|String|Cuando AccessMode es `OpenRowset`, el nombre de la tabla o vista que tiene acceso el destino de OLE DB.|  
|OpenRowsetVariable|String|Cuando AccessMode es `OpenRowset from Variable`, el nombre de la variable que contiene el nombre de la tabla o vista que tiene acceso el destino de OLE DB.|  
|SqlCommand|String|Cuando AccessMode es `SQL Command`, la instrucción de Transact-SQL que usa el destino de OLE DB para especificar las columnas de destino para los datos.|  
  
 La entrada y las columnas de entrada del destino de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Destination](ole-db-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  
