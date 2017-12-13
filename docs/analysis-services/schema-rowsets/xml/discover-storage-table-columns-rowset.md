---
title: Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMNS | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 24abb88e-33a9-4ae2-829d-cdef0ff22ec1
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6ca81b54546e3ff69c42ea60484e462513443c5e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="discoverstoragetablecolumns-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMNS, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Proporciona información en el nivel de columna acerca de las tablas de almacenamiento utilizado por una base de datos de Analysis Services que se ejecuta en modo SharePoint o Tabular.  
  
 **Se aplica a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DISCOVER_STORAGE_TABLE_COLUMNS** filas contiene las columnas siguientes.  
  
|**Nombre de columna**|**Indicador de tipo**|**Restricción**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Sí|Especifica el nombre de la base de datos que contiene las tablas. Si se omite, se utiliza la base de datos actual.<br /><br /> El **DISCOVER_STORAGE_TABLE_COLUMNS** conjunto de filas puede restringirse mediante esta columna.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Sí|Especifica el cubo o el modelo que contiene las tablas.<br /><br /> El conjunto de filas **DISCOVER_STORAGE_TABLES** puede restringirse mediante esta columna.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Sí|Nombre del grupo de medida.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Nombre de la dimensión.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||El nombre del atributo.|  
|**TABLE_ID**|**DBTYPE_WSTR**||Identificador de la tabla.|  
|**COLUMN_ID**|**DBTYPE_ WSTR**||El identificador de la columna. El identificador de columna es interno al motor de análisis de memoria de xVelocity (VertiPaq) y tiene un fin informativo únicamente.|  
|**COLUMN_TYPE**|**DBTYPE_WSTR**||Tipo de columna. El tipo de columna es interno al motor de análisis de memoria de xVelocity (VertiPaq) y tiene un fin informativo únicamente.<br /><br /> BASIC_DATA<br /><br /> HIERARCHY_DATAID_TO_POSITION<br /><br /> HIERARCHY_POSITION_TO_DATAID<br /><br /> RELATIONSHIP|  
|**COLUMN_ENCODING**|**DBTYPE_UI8**||Entero que representa el tipo de codificación utilizado para los datos de la columna.<br /><br /> **0**, que se usa con **COLUMN_TYPE**: HIERARCHY_DATAID_TO_POSITION, HIERARCHY_POSITION_TO_DATAID, relación<br /><br /> **1**, que se usa con **COLUMN_TYPE**: BASIC_DATA<br /><br /> **2**, que se usa con **COLUMN_TYPE**: BASIC_DATA|  
|**TIPO DE DATOS**|**DBTYPE_WSTR**||Tipo de datos de la columna. Puede tener estos valores:<br /><br /> DBTYPE_BOOL<br /><br /> DBTYPE_CY<br /><br /> DBTYPE_DATE<br /><br /> DBTYPE_I4<br /><br /> DBTYPE_I8<br /><br /> DBTYPE_R8<br /><br /> DBTYPE_WSTR<br /><br /> N/D|  
|**ISKEY**|**DBTYPE_BOOL**||**True** si la columna se utiliza como una clave principal o externa; en caso contrario **false**.|  
|**ISUNIQUE**|**DBTYPE_BOOL**||**True** si los valores de la columna son únicos; en caso contrario **false**.|  
|**ISNULLABLE**|**DBTYPE_BOOL**||**True** si la columna admite valores NULL; en caso contrario **false**.|  
|**ISROWNUMBER**|**DBTYPE_BOOL**||**True** si la columna es una columna de número de fila. Columnas de número de fila para uso interno del motor de análisis de memoria xVelocity.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd44-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageTableColumns|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo de código se usa una consulta DMV para devolver el conjunto de resultados.  
  
```  
SELECT *  
FROM $System.DISCOVER_STORAGE_TABLE_COLUMNS  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
