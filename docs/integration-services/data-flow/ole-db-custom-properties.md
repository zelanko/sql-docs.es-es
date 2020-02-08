---
title: Propiedades personalizadas de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 039b36c2092d9e08e81802e441f42587be66445c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298158"
---
# <a name="ole-db-custom-properties"></a>Propiedades personalizadas de OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Propiedades personalizadas de origen**  
  
 El origen de OLE DB tiene tanto propiedades personalizadas como propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de OLE DB. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Entero|Modo que se usa para tener acceso a la base de datos. Los valores posibles son **Open Rowset**, **Open Rowset from Variable**, **SQL Command**y **SQL Command from Variable**. El valor predeterminado es **Open Rowset**.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad **DefaultCodePage** para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es **False**.|  
|CommandTimeout|Entero|Número de segundos que tienen que transcurrir antes de que un comando supere el tiempo de espera. El valor 0 indica un tiempo infinito.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de OLE DB**, pero se puede definir con el **Editor avanzado**.|  
|DefaultCodePage|Entero|Página de códigos que se usa cuando no hay información disponible de la misma en el origen de datos.|  
|OpenRowset|String|Nombre del objeto de base de datos que se usa para abrir un conjunto de filas.|  
|OpenRowsetVariable|String|Variable que contiene el objeto del objeto de base de datos que se usa para abrir un conjunto de filas.|  
|ParameterMapping|String|Asignación de los parámetros del comando SQL a variables.|  
|SqlCommand|String|Comando SQL que se va a ejecutar.|  
|SqlCommandVariable|String|Variable que contiene el comando SQL que se va a ejecutar.|  
  
 La salida y las columnas de salida del origen de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de OLE DB tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino OLE DB. Todas las propiedades son de lectura y escritura.  
  
> [!NOTE]  
>  Las opciones de carga rápida enumeradas aquí (FastLoadKeepIdentity, FastLoadKeepNulls y FastLoadOptions) corresponden a las propiedades con nombre similar que expone la interfaz **IRowsetFastLoad** implementada por el proveedor Microsoft OLE DB para SQL Server (SQLOLEDB). Para obtener más información, busque IRowsetFastLoad en la MSDN Library.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica cómo tiene acceso el destino a su base de datos de destino.<br /><br /> Esta propiedad admite cualquiera de los siguientes valores:<br /><br /> <br /><br /> **OpenRowset** (0): se proporciona el nombre de una tabla o vista.<br /><br /> **OpenRowset desde variable** (1): se proporciona el nombre de una variable que contiene el nombre de una tabla o vista.<br /><br /> **OpenRowset con FastLoad** (3): se proporciona el nombre de una tabla o vista.<br /><br /> **OpenRowset con FastLoad desde variable** (4): se proporciona el nombre de una variable que contiene el nombre de una tabla o vista.<br /><br /> **Comando SQL** (2): se proporciona una instrucción SQL.|  
|AlwaysUseDefaultCodePage|Boolean|Valor que indica si usar el valor de la propiedad **DefaultCodePage** para cada columna, o intentar derivar la página de códigos de la configuración regional de cada columna. El valor predeterminado de esta propiedad es **False**.|  
|CommandTimeout|Entero|Número máximo de segundos que el comando SQL se puede ejecutar antes de superar el tiempo de espera. Un valor de 0 indica un tiempo infinito. El valor predeterminado de esta propiedad es 0.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de destino OLE DB**, pero se puede definir con el **Editor avanzado**.|  
|DefaultCodePage|Entero|Página de códigos predeterminada asociada al destino OLE DB.|  
|FastLoadKeepIdentity|Boolean|Valor que especifica si se copian los valores de identidad cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es **False**. Esta propiedad corresponde a **SSPROP_FASTLOADKEEPIDENTITY** de la propiedad [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) de OLE DB.|  
|FastLoadKeepNulls|Boolean|Valor que especifica si se copian los valores Null cuando se cargan los datos. Esta propiedad solo está disponible con una de las opciones de carga rápida. El valor predeterminado de esta propiedad es **False**. Esta propiedad corresponde a **SSPROP_FASTLOADKEEPNULLS** de la propiedad [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) de OLE DB.|  
|FastLoadMaxInsertCommitSize|Entero|Valor que especifica el tamaño de lote que el destino OLE DB intenta confirmar en operaciones de carga rápida. El valor predeterminado, **0**, indica una operación de confirmación única después de que se procesen todas las filas.|  
|FastLoadOptions|String|Colección de opciones de carga rápida. Las opciones de carga rápida incluyen el bloqueo de las tablas y la comprobación de las restricciones. Puede especificar una, ambas o ninguna. Esta propiedad corresponde a **SSPROP_FASTLOADOPTIONS** de la propiedad IRowsetFastLoad de OLE DB y acepta opciones de cadena como **CHECK_CONSTRAINTS** y **TABLOCK**.<br /><br /> Nota: Algunas opciones de esta propiedad no están disponibles en el **Editor de destino de Excel**, pero pueden definirse con el **Editor avanzado**.|  
|OpenRowset|String|Cuando AccessMode es **OpenRowset**, nombre de la tabla o vista a la que tiene acceso el destino de OLE DB.|  
|OpenRowsetVariable|String|Cuando AccessMode es **OpenRowset desde variable**, nombre de la variable que contiene el nombre de la tabla o vista a la que tiene acceso el destino de OLE DB.|  
|SqlCommand|String|Cuando AccessMode es **Comando SQL**, instrucción Transact-SQL que usa el destino de OLE DB para especificar las columnas de destino para los datos.|  
  
 La entrada y las columnas de entrada del destino de OLE DB no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
