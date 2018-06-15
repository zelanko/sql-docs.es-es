---
title: Conjunto de filas DISCOVER_DATASOURCES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9e316e1e8927acb5dcb99046a8d53034126052ce
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34029581"
---
# <a name="discoverdatasources-rowset"></a>Conjunto de filas DISCOVER_DATASOURCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve una lista de los orígenes de datos del proveedor XML for Analysis (XMLA) que están disponibles en el servidor o servicio web. Los orígenes de datos publicados se devuelven desde una dirección URL del servidor web de la aplicación. El cliente puede conectarse a uno de los orígenes de datos de esta lista.  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_DATASOURCES** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover** método devuelve el **DISCOVER_DATASOURCES** conjunto de filas.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El cliente selecciona un origen de datos estableciendo el **DataSourceInfo** propiedad en el [propiedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) elemento que se envía junto con el [comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md) elemento por la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método. Un cliente no debería construir el contenido de la propiedad **DataSourceInfo** que se ha de enviar al servidor. En su lugar, el cliente debería utilizar el método **Discover** para buscar los orígenes de datos que el proveedor admite. El cliente devuelve a continuación el mismo valor para la propiedad **DataSourceInfo** que recupera del conjunto de filas **DISCOVER_DATASOURCES** .  
  
 El conjunto de filas **DISCOVER_DATASOURCES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DataSourceName**|**DBTYPE_WSTR**|Sí|Nombre del origen de datos, por ejemplo **Adventure Works**.|  
|**DataSourceDescription**|**DBTYPE_WSTR**||La descripción del origen de datos escrita por el publicador.<br /><br /> Puede devolver **NULL**.|  
|**Dirección URL**|**DBTYPE_WSTR**|Sí|Ruta de acceso única que muestra dónde invocar los métodos de XML for Analysis (XMLA) para ese origen de datos.<br /><br /> Puede devolver **NULL**.|  
|**DataSourceInfo**|**DBTYPE_WSTR**||Una cadena que contiene la información adicional necesaria para conectarse al origen de datos.<br /><br /> Puede devolver **NULL**.|  
|**ProviderName**|**DBTYPE_WSTR**|Sí|Nombre del proveedor para el origen de datos.<br /><br /> Ejemplo: `"MSOLAP"`<br /><br /> Puede devolver **NULL**.|  
|**ProviderType**|**DBTYPE_WSTR**|Sí|Tipos de datos admitidos por el proveedor. Esta matriz puede incluir uno o varios de los tipos siguientes:<br /><br /> **MDP**: proveedor de datos multidimensionales.<br /><br /> **TDP**: proveedor de datos tabulares.<br /><br /> **DMP**: proveedor de minería de datos (implementa la especificación de OLE DB para minería de datos).|  
|**AuthenticationMode**|**DBTYPE_WSTR**|Sí|Especificación de qué tipo de modo de seguridad usa el origen de datos. Los valores pueden ser cualquier de los siguientes:<br /><br /> **Unauthenticated**: no se tiene que enviar ningún id. de usuario ni contraseña.<br /><br /> **Authenticated**: el id. de usuario y la contraseña deben incluirse en la información necesaria para conectarse al origen de datos.<br /><br /> **Integrado**: el origen de datos utiliza la seguridad subyacente para determinar la autorización, como seguridad integrada que proporciona [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS).|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas **DISCOVER_DATASOURCES** no se puede consultar utilizando consultas DMV y la sintaxis del comando SELECT. Sin embargo, el **DISCOVER_DATASOURCES** conjunto de filas se pueden consultar mediante <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
