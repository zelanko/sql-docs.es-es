---
title: Conjunto de filas DISCOVER_MEMORYGRANT | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
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
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 68bbbbcebe6c3f47f8b3868ba7a67b79f75503cf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discovermemorygrant-rowset"></a>Conjunto de filas DISCOVER_MEMORYGRANT
  Devuelve una lista de concesiones de cuota de memoria interna utilizadas por los trabajos que se están ejecutando actualmente en el servidor. Para averiguar si un trabajo está ejecutando en el servidor, use `Select * from $System.Discover_Jobs`.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_MEMORYGRANT** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**MEMORY_ID**|**DBTYPE_I8**||Número que identifica la concesión de cuota de memoria. Único en el contexto de una solicitud de DISCOVER_MEMORYGRANT individual.|  
|**SPID**|**DBTYPE_I4**|Necesario|SPID, que puede obtener ejecutando `Select * from $System.Discover_Sessions`.|  
|**CreationTime**|**DBTYPE_I8 DBTYPE_DBTIMESTAMP**||Hora en que se concedió la cuota.|  
|**LastRequestTime**|**DBTYPE_DBTIMESTAMP**||Hora en que la solicitud de cuota se modificó por última vez.|  
|**MemoryUsed**|**DBTYPE_I4**||Cantidad de memoria usada en asociación con la cuota.|  
|**MemoryGranted**|**DBTYPE_I4**||Cantidad de memoria concedida para que la use el trabajo que obtiene la cuota de memoria.|  
|**Bloqueado**|**DBTYPE_BOOL**||Valor booleano que indica el estado del bloqueo del trabajo. True indica que el trabajo está bloqueado a la espera de que otro trabajo libere cuota suficiente para conceder su solicitud de la cuota. False indica que el trabajo ha recibido su cuota y se puede ejecutar.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
