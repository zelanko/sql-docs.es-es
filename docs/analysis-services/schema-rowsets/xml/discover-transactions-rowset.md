---
title: Conjunto de filas DISCOVER_TRANSACTIONS | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a9dc8533965c6187311cedbecafb6361e5f505a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discovertransactions-rowset"></a>Conjunto de filas DISCOVER_TRANSACTIONS
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
|Cadena|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
