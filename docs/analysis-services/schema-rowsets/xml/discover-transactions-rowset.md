---
title: Conjunto de filas DISCOVER_TRANSACTIONS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4084d4a964a901c7f4fc78114f596ef9d6708dc3
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="discovertransactions-rowset"></a>Conjunto de filas DISCOVER_TRANSACTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve el conjunto actual de transacciones pendientes en el sistema.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_TRANSACTIONS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**VALOR DE TRANSACTION_ID**|**DBTYPE_WSTR**|Identificador único de la transacción, como un GUID.|  
|**TRANSACTION_SESSION_ID**|**DBTYPE_WSTR**|Identificador único de la sesión de transacción, como un GUID.|  
|**TRANSACTION_START_TIME**|**DBTYPE_DBTIMESTAMP**|Fecha y hora UTC del servidor cuando se inició la transacción.|  
|**TRANSACTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|Tiempo transcurrido, en milisegundos, desde el inicio de la transacción.|  
|**TRANSACTION_CPU_TIME_MS**|**DBTYPE_I8**|Tiempo de CPU, en milisegundos, consumido por todas las solicitudes desde el principio de la transacción.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_TRANSACTIONS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|**Nombre de columna**|**Indicador de tipo**|**Estado de restricción**|  
|---------------------|------------------------|---------------------------|  
|**ID**|**DBTYPE_WSTR**|Opcional.|  
|**SESSION_ID**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
