---
title: SchemaEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c95ec9525fe0890d241fd6a99a6c298f6ef7568e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315799"
---
# <a name="schemaenum"></a>SchemaEnum
Especifica el tipo de esquema **Recordset** que la [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) recupera del método.  
  
## <a name="remarks"></a>Comentarios  
 Información adicional acerca de la función y las columnas se devuelve para cada constante ADO puede encontrarse en los temas de [Apéndice B: Conjuntos de filas de esquema](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) de referencia del programador OLE DB. El nombre de cada tema aparece entre paréntesis en la sección de descripción de la tabla siguiente.  
  
 Información adicional acerca de la función y las columnas se devuelve para cada constante ADO MD se puede encontrar en los temas de [OLE DB para los objetos OLAP y conjuntos de filas de esquema](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) en OLE DB para la documentación de procesamiento analítico en línea (OLAP). El nombre de cada tema aparece entre paréntesis en la columna de descripción de la tabla siguiente.  
  
 Puede convertir los tipos de datos de columnas en la documentación de OLE DB a tipos de datos ADO consultando la columna Descripción de la propiedad ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) tema. Por ejemplo, un tipo de datos OLE DB de **DBTYPE_WSTR** es equivalente a un tipo de datos de ADO de **adWChar**.  
  
 ADO genera resultados con el aspecto del esquema para las constantes, **adSchemaDBInfoKeywords** y **adSchemaDBInfoLiterals**. ADO crea un **Recordset**y, a continuación, rellena cada fila con los valores devueltos respectivamente por la **GetKeywords** y **IDBInfo:: GetLiteralInfo** métodos. Se puede encontrar información adicional acerca de estos métodos en el [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) sección de referencia de la base de datos del programador de OLE.  
  
|Constante|Valor|Descripción|Columnas de restricción|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|Devuelve las aserciones definidas en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas de ASERCIONES)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|Devuelve los atributos físicos asociados con los catálogos accesibles desde el DBMS.<br /><br /> (Conjunto de filas de catálogos)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|Devuelve los juegos de caracteres definidos en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas CHARACTER_SETS)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Devuelve las restricciones check definidas en el catálogo que pertenecen a un usuario determinado.<br /><br /> (CHECK_CONSTRAINTS) Conjunto de filas)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|Devuelve las intercalaciones de caracteres definidas en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas de las INTERCALACIONES)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|Devuelve los privilegios para columnas de tablas definidas en el catálogo que están disponibles para o a un usuario determinado.<br /><br /> (Conjunto de filas COLUMN_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|Devuelve las columnas de tablas (incluidas las vistas) definidas en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas COLUMNS)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|Devuelve las columnas definidas en el catálogo que dependen de un dominio definido en el catálogo y que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas COLUMN_DOMAIN_USAGE)|DOMAIN_CATALOG DOMAIN_SCHEMA NOMBRE_DOMINIO COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|Devuelve las columnas utilizadas por las restricciones referenciales, restricciones únicas, restricciones check y aserciones, definidas en el catálogo y que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas CONSTRAINT_COLUMN_USAGE)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|Devuelve las tablas que se usan por las restricciones referenciales, restricciones únicas, restricciones check y aserciones definidas en el catálogo y que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas CONSTRAINT_TABLE_USAGE)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|Devuelve información acerca de los cubos disponibles en un esquema (o el catálogo, si el proveedor no admite esquemas).<br /><br /> (Los cubos de filas *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|Devuelve una lista de palabras clave específicas del proveedor.<br /><br /> (IDBInfo::GetKeywords)|\<None>|  
|**adSchemaDBInfoLiterals**|31|Devuelve una lista de literales específicos del proveedor utilizados en los comandos de texto.<br /><br /> (IDBInfo::GetLiteralInfo)|\<None>|  
|**adSchemaDimensions**|33|Devuelve información acerca de las dimensiones de un cubo determinado. Tiene una fila para cada dimensión.<br /><br /> (Conjunto de filas de dimensiones)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|Devuelve las columnas de clave externas definidas en el catálogo por un usuario determinado.<br /><br /> (Conjunto de filas FOREIGN_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|Devuelve información acerca de las jerarquías disponibles en una dimensión.<br /><br /> (Conjunto de filas de las JERARQUÍAS)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|Devuelve los índices definidos en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas de índices)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TIPO TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|Devuelve las columnas definidas en el catálogo que un usuario determinado restringe como claves.<br /><br /> (KEY_COLUMN_USAGE Rowset)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|Devuelve información sobre los niveles disponibles en una dimensión.<br /><br /> (Los niveles de conjunto de filas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|Devuelve información acerca de las medidas disponibles.<br /><br /> (Conjunto de filas de las medidas)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|Devuelve información acerca de los miembros disponibles.<br /><br /> (Conjunto de filas de miembros)|Catalog_Name SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE operador de árbol. Para obtener más información, consulte OLE DB para OLAP Online Analytical Processing ().|  
|**adSchemaPrimaryKeys**|28|Devuelve las columnas de clave principales definidas en el catálogo por un usuario determinado.<br /><br /> (Conjunto de filas PRIMARY_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|Devuelve información sobre las columnas de los conjuntos de filas que devuelven los procedimientos.<br /><br /> (Conjunto de filas PROCEDURE_COLUMNS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|Devuelve información sobre los parámetros y los códigos devueltos de los procedimientos.<br /><br /> (Conjunto de filas PROCEDURE_PARAMETERS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|Devuelve los procedimientos definidos en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas de procedimientos)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|Devuelve información acerca de las propiedades disponibles para cada nivel de la dimensión.<br /><br /> (Conjunto de filas de propiedades)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|Se utiliza si el proveedor define sus propias consultas de esquema no estándar.|\<Específico del proveedor >|  
|**adSchemaProviderTypes**|22|Devuelve los tipos de datos (base) admitidos por el proveedor de datos.<br /><br /> (Conjunto de filas PROVIDER_TYPES)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|Devuelve las restricciones referenciales definidas en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas REFERENTIAL_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|Devuelve los esquemas (objetos de base de datos) pertenecientes a un usuario determinado.<br /><br /> (Conjunto de filas de esquema de datos)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|Devuelve los niveles de compatibilidad, opciones y dialectos admitidos por los datos de procesamiento de implementación SQL definidos en el catálogo.<br /><br /> (Conjunto de filas SQL_LANGUAGES)|\<None>|  
|**adSchemaStatistics**|19|Devuelve las estadísticas definidas en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas de estadísticas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|Devuelve las restricciones de tabla definidas en el catálogo que pertenecen a un usuario determinado.<br /><br /> (Conjunto de filas TABLE_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|Devuelve los privilegios en tablas definidas en el catálogo que están disponibles para o a un usuario determinado.<br /><br /> (Conjunto de filas TABLE_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|Devuelve las tablas (incluidas las vistas) definidas en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas de tablas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|Devuelve las conversiones de caracteres definidas en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas de traducciones)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|Reservado para uso futuro.||  
|**adSchemaUsagePrivileges**|15|Devuelve los privilegios USAGE en objetos definidos en el catálogo que están disponibles para o a un usuario determinado.<br /><br /> (Conjunto de filas USAGE_PRIVILEGES)|RECEPTOR DE OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME OBJECT_TYPE OTORGANTE DE PERMISOS|  
|**adSchemaViewColumnUsage**|24|Devuelve las columnas en el que las tablas vistas, definen en el catálogo y que pertenecen a un usuario determinado, son dependientes.<br /><br /> (VIEW_COLUMN_USAGE Rowset)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|Devuelve las vistas definidas en el catálogo que se puede acceder a un usuario determinado.<br /><br /> (Conjunto de filas de las vistas)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|Devuelve las tablas en el que las tablas vistas, definen en el catálogo y que pertenecen a un usuario determinado, son dependientes.<br /><br /> (Conjunto de filas VIEW_TABLE_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Método OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
