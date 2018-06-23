---
title: Conjunto de filas DISCOVER_LOCATIONS | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 6d3a1171-8e4d-4022-ade0-b785cf795d70
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cfcc451a3369a3f15e29381df3d21e7275a90f7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199005"
---
# <a name="discoverlocations-rowset"></a>Conjunto de filas DISCOVER_LOCATIONS
  Devuelve información sobre el contenido de un archivo de copia de seguridad. Debe tener permiso de acceso a la ubicación del archivo de copia de seguridad.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_LOCATIONS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|Requerido, vea más abajo.|La ubicación del archivo de copia de seguridad.|  
|`LOCATION_PARTITION_OBJECTPATH`|`DBTYPE_WSTR`||La ruta de acceso a la partición relativa a la carpeta de datos.|  
|`LOCATION_PARTITION_DATASOURCEID`|`DBTYPE_WSTR`||El identificador de origen de datos usado para procesar la partición.|  
|`LOCATION_PARTITION_DATASOURCENAME`|`DBTYPE_WSTR`||El nombre del origen de datos utilizado para el procesamiento.|  
|`LOCATION_PARTITION_NAME`|`DBTYPE_WSTR`||El nombre de la partición.|  
|`LOCATION_PARTITION_SIZE`|`DBTYPE_WSTR`||El tamaño aproximado de la partición.|  
|`LOCATION_CONNECTION_STRING`|`DBTYPE_WSTR`||La cadena de conexión para el origen de datos que se utiliza en el procesamiento.|  
|`LOCATION_PARTITION_FOLDER`|`DBTYPE_WSTR`||La ubicación original de esta partición cuando se ha generado el archivo de copia de seguridad.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_LOCATIONS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`LOCATION_BACKUP_FILE_PATHNAME`|`DBTYPE_WSTR`|Obligatorio|  
|`LOCATION_PASSWORD PF_DBTYPE`|`DBTYPE_WSTR`|Requerido si se especificó durante la copia de seguridad. Esta restricción no se utiliza para limitar las filas devueltas. Se utiliza para proporcionar la contraseña para tener acceso a la ubicación.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd92-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|Ubicaciones|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  