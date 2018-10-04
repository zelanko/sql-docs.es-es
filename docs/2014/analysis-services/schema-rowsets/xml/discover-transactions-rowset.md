---
title: Conjunto de filas DISCOVER_TRANSACTIONS | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b0f8c8dc1a289eaa96325ba22aa2e7dc864fb84
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103963"
---
# <a name="discovertransactions-rowset"></a>Conjunto de filas DISCOVER_TRANSACTIONS
  Devuelve el conjunto actual de transacciones pendientes en el sistema.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_TRANSACTIONS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Descripción|  
|-----------------|--------------------|-----------------|  
|`TRANSACTION_ID`|`DBTYPE_WSTR`|Identificador único de la transacción, como un GUID.|  
|`TRANSACTION_SESSION_ID`|`DBTYPE_WSTR`|Identificador único de la sesión de transacción, como un GUID.|  
|`TRANSACTION_START_TIME`|`DBTYPE_DBTIMESTAMP`|Fecha y hora UTC del servidor cuando se inició la transacción.|  
|`TRANSACTION_ELAPSED_TIME_MS`|`DBTYPE_I8`|Tiempo transcurrido, en milisegundos, desde el inicio de la transacción.|  
|`TRANSACTION_CPU_TIME_MS`|`DBTYPE_I8`|Tiempo de CPU, en milisegundos, consumido por todas las solicitudes desde el principio de la transacción.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_TRANSACTIONS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|**Nombre de columna**|**Indicador de tipo**|**Estado de restricción**|  
|---------------------|------------------------|---------------------------|  
|`ID`|`DBTYPE_WSTR`|Opcional.|  
|`SESSION_ID`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
