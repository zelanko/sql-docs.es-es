---
title: Conjunto de filas DISCOVER_DATASOURCES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e319b05d1d9aec74b01b73b671f613a2703d900f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185262"
---
# <a name="discoverdatasources-rowset"></a>Conjunto de filas DISCOVER_DATASOURCES
  Devuelve una lista de los orígenes de datos del proveedor XML for Analysis (XMLA) que están disponibles en el servidor o servicio web. Los orígenes de datos publicados se devuelven desde una dirección URL del servidor web de la aplicación. El cliente puede conectarse a uno de los orígenes de datos de esta lista.  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_DATASOURCES` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_DATASOURCES` conjunto de filas.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El cliente selecciona un origen de datos estableciendo el `DataSourceInfo` propiedad en el [propiedades](../../xmla/xml-elements-properties/properties-element-xmla.md) elemento que se envía junto con el [comando](../../xmla/xml-elements-properties/command-element-xmla.md) elemento por el [Execute](../../xmla/xml-elements-methods-execute.md) método. Un cliente no debería construir el contenido de la propiedad `DataSourceInfo` que se ha de enviar al servidor. En su lugar, el cliente debería utilizar el método `Discover` para buscar los orígenes de datos que el proveedor admite. El cliente devuelve a continuación el mismo valor para la propiedad `DataSourceInfo` que recupera del conjunto de filas `DISCOVER_DATASOURCES`.  
  
 El `DISCOVER_DATASOURCES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`DataSourceName`|`DBTYPE_WSTR`|Sí|Nombre del origen de datos, por ejemplo `Adventure Works`.|  
|`DataSourceDescription`|`DBTYPE_WSTR`||La descripción del origen de datos escrita por el publicador.<br /><br /> Puede devolver `NULL`.|  
|`URL`|`DBTYPE_WSTR`|Sí|Ruta de acceso única que muestra dónde invocar los métodos de XML for Analysis (XMLA) para ese origen de datos.<br /><br /> Puede devolver `NULL`.|  
|`DataSourceInfo`|`DBTYPE_WSTR`||Una cadena que contiene la información adicional necesaria para conectarse al origen de datos.<br /><br /> Puede devolver `NULL`.|  
|`ProviderName`|`DBTYPE_WSTR`|Sí|Nombre del proveedor para el origen de datos.<br /><br /> Ejemplo: `"MSOLAP"`<br /><br /> Puede devolver `NULL`.|  
|`ProviderType`|`DBTYPE_WSTR`|Sí|Tipos de datos admitidos por el proveedor. Esta matriz puede incluir uno o varios de los tipos siguientes:<br /><br /> `MDP`: proveedor de datos multidimensionales.<br /><br /> `TDP`: proveedor de datos tabulares.<br /><br /> `DMP`: proveedor de minería de datos (implementa la especificación de OLE DB para minería de datos).|  
|`AuthenticationMode`|`DBTYPE_WSTR`|Sí|Especificación de qué tipo de modo de seguridad usa el origen de datos. Los valores pueden ser cualquier de los siguientes:<br /><br /> `Unauthenticated`: no se tiene que enviar ningún identificador de usuario ni contraseña.<br /><br /> `Authenticated`: el identificador de usuario y la contraseña deben incluirse en la información necesaria para conectarse al origen de datos.<br /><br /> `Integrated`: el origen de datos utiliza la seguridad subyacente para determinar la autorización, como la Seguridad integrada que proporciona [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas `DISCOVER_DATASOURCES` no se puede consultar utilizando consultas DMV y la sintaxis del comando SELECT. Sin embargo, el conjunto de filas `DISCOVER_DATASOURCES` se puede consultar usando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
