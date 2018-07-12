---
title: Uso de tipos definidos por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [SQL Server Native Client]
- user-defined types [SQL Server], SQL Server Native Client
- SQL Server Native Client OLE DB provider, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- SQLNCLI, user-defined types
- SQL Server Native Client, user-defined types
- data access [SQL Server Native Client], user-defined types
- ISSCommandWithParameters interface
ms.assetid: e15d8169-3517-4323-9c9e-0f5c34aff7df
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eef3d47ae77c8686ce09eb77665e64de53a229ce
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424804"
---
# <a name="using-user-defined-types"></a>Usar tipos definidos por el usuario
[!INCLUDE[appliesto-ss-asdb-xxxx-pdw-md](../../../includes/appliesto-ss-asdb-xxxx-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Los tipos definidos por el usuario (UDT) se introdujeron en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Los UDT amplían el sistema de tipos SQL al permitirle almacenar objetos y estructuras de datos personalizadas en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos. Los UDT pueden contener varios tipos de datos y pueden presentar distintos comportamientos, lo que los diferencia de los tipos de datos de alias tradicionales que constan de un único tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los UDT pueden definirse mediante cualquiera de los lenguajes compatibles con .NET Common Language Runtime (CLR) que genere código comprobable, Esto incluye Microsoft Visual C#<sup>®</sup> y Visual Basic<sup>®</sup> . NET. Los datos se exponen como campos y propiedades de una clase o estructura de .NET, y los métodos de esa clase o estructura definen los comportamientos.  
  
 Un UDT puede usarse como la definición de columna de una tabla, como una variable en un [!INCLUDE[tsql](../../../includes/tsql-md.md)] por lotes, o como un argumento de un [!INCLUDE[tsql](../../../includes/tsql-md.md)] función o procedimiento almacenado.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite los UDT como tipos binarios con información de metadatos, lo que le permite administrar los UDT como objetos. Las columnas UDT se exponen como DBTYPE_UDT y sus metadatos se exponen a través de la interfaz OLE DB **IColumnRowset**y el nuevo [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) interfaz.  
  
> [!NOTE]  
>  El **irowsetfind:: FindNextRow** método no funciona con el tipo de datos UDT. Si el UDT se usa como un tipo de columna de búsqueda, se devuelve DB_E_BADCOMPAREOP.  
  
### <a name="data-bindings-and-coercions"></a>Enlaces y conversiones de datos  
 En la tabla siguiente se describe el enlace y la conversión que tiene lugar al usar los tipos de datos enumerados con un UDT de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las columnas UDT se exponen a través de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client como DBTYPE_UDT. Puede obtener metadatos mediante los conjuntos de filas de esquema adecuados, de modo que pueda administrar sus propios tipos definidos como objetos.  
  
|Tipo de datos|A datos XML<br /><br /> **UDT**|A datos XML<br /><br /> **no UDT**|Desde datos XML<br /><br /> **UDT**|Desde datos XML<br /><br /> **no UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Admite<sup>6</sup>|Error<sup>1</sup>|Admite<sup>6</sup>|Error<sup>5</sup>|  
|DBTYPE_BYTES|Admite<sup>6</sup>|N/D<sup>2</sup>|Admite<sup>6</sup>|N/D<sup>2</sup>|  
|DBTYPE_WSTR|Admite<sup>3,6</sup>|N/D<sup>2</sup>|Admite<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_BSTR|Admite<sup>3,6</sup>|N/D<sup>2</sup>|Admite<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_STR|Admite<sup>3,6</sup>|N/D<sup>2</sup>|Admite<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_IUNKNOWN|No compatible|N/D<sup>2</sup>|No compatible|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &AMP;#124; VT_ARRAY)|Admite<sup>6</sup>|N/D<sup>2</sup>|Admite<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Admite<sup>3,6</sup>|N/D<sup>2</sup>|N/D|N/D<sup>2</sup>|  
  
 <sup>1</sup>si el tipo de un servidor distinto de DBTYPE_UDT se especifica con **ICommandWithParameters:: SetParameterInfo** y el tipo de descriptor de acceso es DBTYPE_UDT, se produce un error cuando se ejecuta la instrucción (DB_E_ERRORSOCCURRED; el estado del parámetro es DBSTATUS_E_BADACCESSOR). De lo contrario, los datos se envían al servidor, pero el servidor devuelve un error que indica que no hay ninguna conversión implícita de UDT al tipo de datos del parámetro.  
  
 <sup>2</sup>fuera del ámbito de este tema.  
  
 <sup>3</sup> se produce la conversión de datos de cadena hexadecimal a datos binarios.  
  
 <sup>4</sup> se produce la conversión de datos de los datos binarios a una cadena hexadecimal.  
  
 <sup>5</sup>puede realizar la validación en el momento de descriptor de acceso de creación o en tiempo de captura, el error es DB_E_ERRORSOCCURRED, con el estado de enlace establecido en DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>6</sup>puede utilizarse by_ref.  
  
 DBTYPE_NULL y DBTYPE_EMPTY pueden estar limitados para parámetros de entrada, pero no para los parámetros de salida o los resultados. Cuando se enlazan para parámetros de entrada, el estado debe establecerse en DBSTATUS_S_ISNULL o DBSTATUS_S_DEFAULT.  
  
 DBTYPE_UDT también puede convertirse en DBTYPE_EMPTY y DBTYPE_NULL, pero DBTYPE_NULL y DBTYPE_EMPTY no pueden convertirse en DBTYPE_UDT. Este comportamiento es coherente con el de DBTYPE_BYTES.  
  
> [!NOTE]  
>  Se usa una nueva interfaz para tratar los UDT como parámetros, **ISSCommandWithParameters**, que hereda de **ICommandWithParameters**. Las aplicaciones deben usar esta interfaz para establecer al menos la propiedad SSPROP_PARAM_UDT_NAME del conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER para los parámetros UDT. Si no se hace esto, **ICommand:: Execute** devolverá DB_E_ERRORSOCCURRED. Esta interfaz y este conjunto de propiedades se describen más adelante en este tema.  
  
 Si un tipo definido por el usuario se inserta en una columna que no es suficientemente grande como para contener todos sus datos, **ICommand:: Execute** devuelve S_OK con un estado DB_E_ERRORSOCCURRED.  
  
 Las conversiones de datos proporcionadas por los servicios principales de OLE DB (**IDataConvert**) no son aplicables a DBTYPE_UDT. No se admite ningún otro enlace.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adiciones y cambios en los conjuntos de filas de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega nuevos valores o cambios a muchos de los conjuntos de filas de esquema de OLE DB.  
  
#### <a name="the-procedureparameters-schema-rowset"></a>El conjunto de filas de esquema PROCEDURE_PARAMETERS  
 Se han realizado las siguientes adiciones al conjunto de filas de esquema PROCEDURE_PARAMETERS.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|El ensamblado de nombre completo, que incluye el nombre de tipo y todas la identificación de ensamblado necesaria para hacer referencia a CLR.|  
  
#### <a name="the-sqlassemblies-schema-rowset"></a>El conjunto de filas de esquema SQL_ASSEMBLIES  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone un nuevo proveedor específico de filas de esquema que describe los UDT registrados. El servidor ASSEMBLY puede especificarse como DBTYPE_WSTR, pero no está presente en el conjunto de filas. Si no se especifica, el conjunto de filas tendrá como valor predeterminado el servidor actual. El conjunto de filas de esquema SQL_ASSEMBLIES se define en la tabla siguiente.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Nombre de catálogo del ensamblado que contiene el tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Nombre de esquema o nombre de propietario del ensamblado que contiene el tipo. Aunque el ámbito de los ensamblados viene determinado por la base de datos y no por el esquema, los ensamblados tienen un propietario que se refleja aquí.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|Nombre del ensamblado que contiene el tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|Identificador de objeto del ensamblado que contiene el tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Valor que indica el ámbito de acceso del ensamblado. Entre los valores posibles se incluyen "SAFE", "EXTERNAL_ACCESS" y "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|Representación binaria del ensamblado.|  
  
#### <a name="the-sqlassemblies-dependencies-schema-rowset"></a>El conjunto de filas de esquema SQL_ASSEMBLIES_DEPENDENCIES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Proveedor OLE DB de cliente nativo expone un nuevo conjunto de filas de esquemas específicas del proveedor que describe las dependencias de ensamblado para un servidor especificado. El autor de la llamada puede especificar ASSEMBLY_SERVER como DBTYPE_WSTR, pero no está presente en el conjunto de filas. Si no se especifica, el conjunto de filas tendrá como valor predeterminado el servidor actual. El conjunto de filas de esquema SQL_ASSEMBLY_DEPENDENCIES se define en la tabla siguiente.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Nombre de catálogo del ensamblado que contiene el tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Nombre de esquema o nombre de propietario del ensamblado que contiene el tipo. Aunque los ensamblados tienen como ámbito la base de datos y no por el esquema, tienen un propietario, que se refleja aquí.|  
|ASSEMBLY_ID|DBTYPE_UI4|Identificador de objeto del ensamblado.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|Identificador de objeto del ensamblado al que se hace referencia.|  
  
#### <a name="the-sqlusertypes-schema-rowset"></a>El conjunto de filas de esquema SQL_USER_TYPES  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Proveedor OLE DB de cliente nativo expone nuevas filas de esquema, SQL_USER_TYPES, que se describe cuándo se agrega los UDT registrados para un servidor especificado. El autor de la llamada debe especificar UDT_SERVER como DBTYPE_WSTR, pero no está presente en el conjunto de filas. El conjunto de filas de esquema SQL_USER_TYPES se define en la tabla siguiente.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|UDT_NAME|DBTYPE_WSTR|Nombre del ensamblado que contiene la clase UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|El nombre de tipo completo (AQN) incluye el nombre de tipo precedido del espacio de nombres, si procede.|  
  
#### <a name="the-columns-schema-rowset"></a>El conjunto de filas de esquema COLUMNS  
 Las adiciones al conjunto de filas de esquema COLUMNS incluyen las columnas siguientes.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|SS_UDT_NAME|DBTYPE_WSTR|Nombre del UDT.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|El nombre de tipo completo (AQN) incluye el nombre de tipo precedido del espacio de nombres, si procede.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adiciones y cambios en los conjuntos de propiedades de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega nuevos valores o cambios a muchos de las principales propiedades de OLE DB conjuntos.  
  
#### <a name="the-dbpropsetsqlserverparameter-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER  
 Para admitir los UDT a través de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa el nuevo conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER que contiene los valores siguientes.  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para los parámetros UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el tipo definido por el usuario.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para los parámetros UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el tipo definido por el usuario.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para las columnas UDT, esta propiedad es una cadena que especifica el nombre de una sola parte del tipo definido por el usuario.|  
  
 La propiedad SSPROP_PARAM_UDT_NAME es obligatoria. Las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME son opcionales. Si alguna de las propiedades se especifica incorrectamente, se devolverá DB_E_ERRORSINCOMMAND. Si no se especifican las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME, el UDT debe definirse en la misma base de datos y esquema que la tabla. Si la definición UDT no está en el mismo esquema que la tabla (pero está en la misma base de datos), debe especificarse la propiedad SSPROP_PARAM_UDT_SCHEMANAME. Si la definición UDT está en una base de datos diferente, deben especificarse las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME.  
  
#### <a name="the-dbpropsetsqlservercolumn-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN  
 Para admitir la creación de tablas en el **ITableDefinition** interfaz, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega tres nuevas columnas al conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nombre|Descripción|Tipo|Descripción|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre de una sola parte del UDT. Para otros tipos de columna, esta propiedad devuelve una cadena vacía.|  
  
> [!NOTE]  
>  Los UDT no aparecerán en el conjunto de filas de esquema PROVIDER_TYPES. Todas las columnas tienen acceso de lectura y escritura.  
  
 ADO hará referencia a estas propiedades utilizando la entrada correspondiente de la columna Descripción.  
  
 La propiedad SSPROP_COL_UDTNAME es obligatoria. Las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME son opcionales. Si alguna de las propiedades se especifica incorrectamente, **DB_E_ERRORSINCOMMAND** se devolverá.  
  
 Si no se especifican las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME, el UDT debe definirse en la misma base de datos y esquema que la tabla.  
  
 Si la definición UDT no está en el mismo esquema que la tabla (pero está en la misma base de datos), debe especificarse la propiedad SSPROP_COL_UDT_SCHEMANAME.  
  
 Si la definición UDT está en una base de datos diferente, deben especificarse las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adiciones y cambios en las interfaces de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega nuevos valores o cambios a muchas de las interfaces OLE DB básicas.  
  
#### <a name="the-isscommandwithparameters-interface"></a>La interfaz ISSCommandWithParameters  
 Para admitir los UDT a través de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa diversos cambios, incluida la adición de la **ISSCommandWithParameters** interfaz. Esta nueva interfaz hereda de la interfaz OLE DB **ICommandWithParameters**. Además de los tres métodos heredados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, y **SetParameterInfo**; **ISSCommandWithParameters** proporciona el **GetParameterProperties** y **SetParameterProperties** métodos que se usan para controlar específico del servidor tipos de datos.  
  
> [!NOTE]  
>  El **ISSCommandWithParameters** interfaz también hace uso de SSPARAMPROPS nueva estructura.  
  
#### <a name="the-icolumnsrowset-interface"></a>La interfaz IColumnsRowset  
 Además el **ISSCommandWithParameters** interfaz, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client también agrega nuevos valores al conjunto de filas devuelto desde la llamada la **IColumnsRowset:: Getcolumnrowset** (método) incluidos los siguientes.  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de catálogo UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de esquema UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Identificador de nombre UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Nombre de ensamblado completo, que incluye el nombre de tipo y toda la identificación de ensamblado necesaria a la que debe hacer referencia CLR.|  
  
 Es posible diferenciar una columna UDT del servidor de otros tipos binarios cuando el parámetro DBCOLUMN_TYPE está establecido en DBTYPE_UDT; para ello, hay que examinar los metadatos UDT agregados especificados anteriormente. Si esos datos están parcialmente completos, el tipo del servidor es un UDT. Para los tipos del servidor que no son UDT, estas columnas se devuelven siempre como NULL.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 Se han realizado varios cambios en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client para admitir los UDT. El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] asignaciones de controlador ODBC de Native Client la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificador de tipo UDT a los datos SQL específicas del controlador SQL_SS_UDT. Las columnas UDT se exponen como SQL_SS_UDT. Si asigna una columna UDT explícitamente a otro tipo en una instrucción SQL mediante el uso de la **ToString** o **ToXMLString** métodos del UDT o a través de la **CAST/CONVERT** (función), el tipo de la columna en el resultado de conjunto refleja el tipo real de en que la columna se convierte  
  
### <a name="sqlcolattribute-sqldescribeparam-sqlgetdescfield"></a>SQLColAttribute, SQLDescribeParam, SQLGetDescField  
 Se han agregado cuatro nuevos campos descriptores específicos del controlador para proporcionar información adicional para una columna UDT de un conjunto de resultados o un parámetro UDT de consulta parametrizada o procedimiento almacenado, va a recuperar a través de la [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md), [SQLDescribeParam](../../../relational-databases/native-client-odbc-api/sqldescribeparam.md), y [SQLGetDescField](../../../relational-databases/native-client-odbc-api/sqlgetdescfield.md) funciones.  
  
 Estos cuatro nuevos campos descriptores que se han agregado son SQL_CA_SS_UDT_CATALOG_NAME, SQL_CA_SS_UDT_SCHEMA_NAME, SQL_CA_SS_UDT_TYPE_NAME y SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="sqlcolumns-sqlprocedurecolumns"></a>SQLColumns, SQLProcedureColumns  
 Además, se agregan tres nuevas columnas específicas del controlador para el conjunto de resultados devuelto desde el [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) y [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) funciones para proporcionar información adicional sobre un resultado UDT conjunto de columnas o un parámetro UDT. Estas tres nuevas columnas son SS_UDT_CATALOG_NAME, SS_UDT_SCHEMA_NAME y SS_UDT_ASSEMBLY_TYPE_NAME.  
  
### <a name="supported-conversions"></a>Conversiones admitidas  
 Al convertir tipos de datos de SQL a C, SQL_C_WCHAR, SQL_C_BINARY y SQL_C_CHAR pueden convertirse en SQL_SS_UDT. Tenga en cuenta, no obstante, que los datos binarios se convierten en una cadena hexadecimal cuando se realizan conversiones desde los tipos de datos SQL SQL_C_CHAR y SQL_C_WCHAR.  
  
 Al convertir tipos de datos de C a SQL, SQL_C_WCHAR, SQL_C_BINARY y SQL_C_CHAR pueden convertirse en SQL_SS_UDT. Sin embargo, tenga en cuenta que los datos binarios se convierten en una cadena hexadecimal al convertir los tipos de datos SQL SQL_C_CHAR y SQL_C_WCHAR.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
