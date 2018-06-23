---
title: Conjunto de filas DISCOVER_COMMAND_OBJECTS | Documentos de Microsoft
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
helpviewer_keywords:
- DISCOVER_COMMAND_OBJECTS rowset
ms.assetid: 325114ee-3a50-4504-9782-dbf7c1a44778
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c53fccdecc824bd123312a881c1ddcdbcae6060a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113476"
---
# <a name="discovercommandobjects-rowset"></a>DISCOVER_COMMAND_OBJECTS, conjunto de filas
  Proporciona información sobre el uso de los recursos y la actividad en los objetos que utiliza el comando al que se hace referencia.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_COMMAND_OBJECTS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`SESSION_SPID`|`DBTYPE_I4`|Sí|Identificador de la sesión.|  
|`SESSION_ID`|`DBTYPE_WSTR`|Sí|Identificador único de la sesión, como un GUID.|  
|`SESSION_COMMAND_COUNT`|`DBTYPE_I4`||Número de secuencia del comando.|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`|Sí|Ruta de acceso al elemento primario del objeto actual.|  
|`OBJECT_ID`|`DBTYPE_WSTR`|Sí|Id. del objeto tal y como se definió en el momento de su creación.|  
|`OBJECT_VERSION`|`DBTYPE_I4`||Número de versión de metadatos del objeto; este número cambia cada vez que se modifica el objeto.|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||Número de linaje de los datos del objeto. Este número se incrementa cada vez que se procesa el objeto.|  
|`OBJECT_CPU_TIME_MS`|`DBTYPE_I8`||Tiempo de CPU, en milisegundos, consumido por el objeto desde el inicio del comando.|  
|`OBJECT_READ_KB`|`DBTYPE_I8`||Valor acumulado de los datos leídos por el objeto desde el inicio del comando, en kilobytes.|  
|`OBJECT_READS`|`DBTYPE_I8`||Número acumulado de operaciones de lectura realizadas por el objeto desde el inicio del comando.|  
|`OBJECT_WRITE_KB`|`DBTYPE_I8`||Valor acumulado de los datos escritos por el objeto desde el inicio del comando, en kilobytes.|  
|`OBJECT_WRITES`|`DBTYPE_I8`||Número acumulado de operaciones de escritura realizadas por el objeto desde el inicio del comando.|  
|`OBJECT_ROWS_RETURNED`|`DBTYPE_I8`||Número de filas devueltas por el objeto al autor de las llamadas desde el inicio del comando.|  
|`OBJECT_ROWS_SCANNED`|`DBTYPE_I8`||Número de filas examinadas por el objeto desde el inicio del comando.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas de esquema DISCOVER_COMMAND_OBJECTS no notifica la actividad mediante consultas DMV.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd35-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|CommandObjects|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  