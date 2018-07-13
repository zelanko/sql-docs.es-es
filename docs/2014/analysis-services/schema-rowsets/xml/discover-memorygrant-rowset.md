---
title: Conjunto de filas DISCOVER_MEMORYGRANT | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: d254e42d-9918-47ce-b6df-47f1f0b432dd
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3cae85df7e3c76afd9243771032f21f8f91861f7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229995"
---
# <a name="discovermemorygrant-rowset"></a>Conjunto de filas DISCOVER_MEMORYGRANT
  Devuelve una lista de concesiones de cuota de memoria interna utilizadas por los trabajos que se están ejecutando actualmente en el servidor. Para averiguar si un trabajo está ejecutando en el servidor, use `Select * from $System.Discover_Jobs`.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_MEMORYGRANT` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`MEMORY_ID`|**DBTYPE_I8**||Número que identifica la concesión de cuota de memoria. Único en el contexto de una solicitud de DISCOVER_MEMORYGRANT individual.|  
|`SPID`|`DBTYPE_I4`|Obligatorio|SPID, que puede obtener ejecutando `Select * from $System.Discover_Sessions`.|  
|`CreationTime`|`DBTYPE_I8 DBTYPE_DBTIMESTAMP`||Hora en que se concedió la cuota.|  
|`LastRequestTime`|**DBTYPE_DBTIMESTAMP**||Hora en que la solicitud de cuota se modificó por última vez.|  
|`MemoryUsed`|`DBTYPE_I4`||Cantidad de memoria usada en asociación con la cuota.|  
|`MemoryGranted`|`DBTYPE_I4`||Cantidad de memoria concedida para que la use el trabajo que obtiene la cuota de memoria.|  
|`Blocked`|`DBTYPE_BOOL`||Valor booleano que indica el estado del bloqueo del trabajo. True indica que el trabajo está bloqueado a la espera de que otro trabajo libere cuota suficiente para conceder su solicitud de la cuota. False indica que el trabajo ha recibido su cuota y se puede ejecutar.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd23-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|MemoryGrant|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
