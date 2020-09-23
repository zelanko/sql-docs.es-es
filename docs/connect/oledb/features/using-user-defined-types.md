---
title: Uso de tipos definidos por el usuario | Microsoft Docs
description: OLE DB Driver for SQL Server admite los tipos definidos por el usuario como tipos binarios con información de metadatos, lo que permite administrarlos como objetos.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_DATASOURCEINFO property set
- UDTs [OLE DB Driver for SQL Server]
- user-defined types [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, user-defined types
- DBPROPSET_SQLSERVERPARAMETER property set
- IColumnsRowset interface
- MSOLEDBSQL, user-defined types
- OLE DB Driver for SQL Server, user-defined types
- data access [OLE DB Driver for SQL Server], user-defined types
- ISSCommandWithParameters interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32f1d88d7fad962e1a8aac7b82f8e672fa8e5942
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88860621"
---
# <a name="using-user-defined-types"></a>Usar tipos definidos por el usuario
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Los tipos definidos por el usuario (UDT) se introdujeron en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Los UDT amplían el sistema de tipos SQL, ya que permiten almacenar objetos y estructuras de datos personalizadas en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los UDT pueden contener varios tipos de datos y pueden presentar distintos comportamientos, lo que los diferencia de los tipos de datos de alias tradicionales que constan de un único tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los UDT pueden definirse mediante cualquiera de los lenguajes compatibles con .NET Common Language Runtime (CLR) que genere código comprobable, como Microsoft Visual C#<sup>®</sup> y Visual Basic<sup>®</sup> .NET. Los datos se exponen como campos y propiedades de una clase o estructura de .NET, y los métodos de esa clase o estructura definen los comportamientos.  
  
 Un UDT puede usarse como la definición de columna de una tabla, como una variable de un lote [!INCLUDE[tsql](../../../includes/tsql-md.md)] o como un argumento de una función o procedimiento almacenado [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server  
 El controlador OLE DB para SQL Server admite los UDT como tipos binarios con información de metadatos, lo que permite administrar los UDT como objetos. Las columnas UDT se exponen como DBTYPE_UDT y sus metadatos se exponen mediante la interfaz OLE DB básica **IColumnRowset** y la nueva interfaz [ISSCommandWithParameters](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md).  
  
> [!NOTE]  
>  El método **IRowsetFind::FindNextRow** no funciona con el tipo de datos UDT. Si el UDT se usa como un tipo de columna de búsqueda, se devuelve DB_E_BADCOMPAREOP.  
  
### <a name="data-bindings-and-coercions"></a>Enlaces y conversiones de datos  
 En la tabla siguiente se describe el enlace y la conversión que tiene lugar al usar los tipos de datos enumerados con un UDT de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las columnas UDT se exponen mediante el proveedor OLE DB Driver for SQL Server como DBTYPE_UDT. Puede obtener metadatos mediante los conjuntos de filas de esquema adecuados, de modo que pueda administrar sus propios tipos definidos como objetos.  
  
|Tipo de datos|A datos XML<br /><br /> **UDT**|A datos XML<br /><br /> **non-UDT**|Desde datos XML<br /><br /> **UDT**|Desde datos XML<br /><br /> **non-UDT**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_UDT|Compatible<sup>6</sup>|Error<sup>1</sup>|Compatible<sup>6</sup>|Error<sup>5</sup>|  
|DBTYPE_BYTES|Compatible<sup>6</sup>|N/D<sup>2</sup>|Compatible<sup>6</sup>|N/D<sup>2</sup>|  
|DBTYPE_WSTR|Compatible<sup>3,6</sup>|N/D<sup>2</sup>|Compatible<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_BSTR|Compatible<sup>3,6</sup>|N/D<sup>2</sup>|Compatible<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_STR|Compatible<sup>3,6</sup>|N/D<sup>2</sup>|Compatible<sup>4,6</sup>|N/D<sup>2</sup>|  
|DBTYPE_IUNKNOWN|No compatible|N/D<sup>2</sup>|No compatible|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Compatible<sup>6</sup>|N/D<sup>2</sup>|Compatible<sup>4</sup>|N/D<sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Compatible<sup>3,6</sup>|N/D<sup>2</sup>|N/D|N/D<sup>2</sup>|  
  
 <sup>1</sup>Si se especifica un tipo de servidor distinto de DBTYPE_UDT con **ICommandWithParameters::SetParameterInfo** y el tipo de descriptor de acceso es DBTYPE_UDT, se produce un error cuando se ejecuta la instrucción (DB_E_ERRORSOCCURRED; el estado del parámetro es DBSTATUS_E_BADACCESSOR). De lo contrario, los datos se envían al servidor, pero el servidor devuelve un error que indica que no hay ninguna conversión implícita de UDT al tipo de datos del parámetro.  
  
 <sup>2</sup>Más allá del ámbito de este artículo.  
  
 <sup>3</sup>Las cadenas hexadecimales se convierten en datos binarios.  
  
 <sup>4</sup>Los datos binarios se convierten en cadenas hexadecimales.  
  
 <sup>5</sup>La validación puede tener lugar en el momento de creación del descriptor de acceso o en el momento de la captura; el error es DB_E_ERRORSOCCURRED, con el estado de enlace establecido en DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>6</sup>Puede usarse BY_REF.  
  
 DBTYPE_NULL y DBTYPE_EMPTY pueden enlazarse en parámetros de entrada, pero no en parámetros de salida ni en resultados. Cuando se enlazan para parámetros de entrada, el estado tiene que establecerse en DBSTATUS_S_ISNULL o DBSTATUS_S_DEFAULT.  
  
 DBTYPE_UDT también puede convertirse en DBTYPE_EMPTY y DBTYPE_NULL, pero DBTYPE_NULL y DBTYPE_EMPTY no pueden convertirse en DBTYPE_UDT. Este comportamiento es coherente con el de DBTYPE_BYTES.  
  
> [!NOTE]  
>  Se usa una nueva interfaz para tratar los UDT como parámetros, la interfaz **ISSCommandWithParameters**, que hereda de **ICommandWithParameters**. Las aplicaciones deben usar esta interfaz para establecer al menos la propiedad SSPROP_PARAM_UDT_NAME del conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER para los parámetros UDT. De lo contrario, **ICommand::Execute** devolverá DB_E_ERRORSOCCURRED. Esta interfaz y este conjunto de propiedades se describen más adelante en este artículo.  
  
 Si un tipo definido por el usuario se inserta en una columna que no es lo suficientemente grande como para contener todos sus datos, **ICommand::Execute** devuelve S_OK con un estado DB_E_ERRORSOCCURRED.  
  
 Las conversiones de datos que proporcionan los servicios principales de OLE DB (**IDataConvert**) no son aplicables a DBTYPE_UDT. No se admite ningún otro enlace.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adiciones y cambios en los conjuntos de filas de OLE DB  
 OLE DB Driver for SQL Server agrega nuevos valores o cambios a muchos de los conjuntos de filas de esquema básicos de OLE DB.  
  
#### <a name="the-procedure_parameters-schema-rowset"></a>El conjunto de filas de esquema PROCEDURE_PARAMETERS  
 Se han realizado las siguientes adiciones al conjunto de filas de esquema PROCEDURE_PARAMETERS.  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_NAME|DBTYPE_WSTR|Identificador de nombre de tres partes.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Nombre de ensamblado completo, que incluye el nombre de tipo y toda la identificación de ensamblado necesaria a la que tiene que hacer referencia CLR.|  
  
#### <a name="the-sql_assemblies-schema-rowset"></a>El conjunto de filas de esquema SQL_ASSEMBLIES  
 El controlador OLE DB para SQL Server expone un nuevo conjunto de filas de esquema específico del proveedor que describe los UDT registrados. El servidor ASSEMBLY puede especificarse como DBTYPE_WSTR, pero no está presente en el conjunto de filas. Si no se especifica, el conjunto de filas tendrá como valor predeterminado el servidor actual. El conjunto de filas de esquema SQL_ASSEMBLIES se define en la tabla siguiente:  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Nombre de catálogo del ensamblado que contiene el tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Nombre de esquema o nombre de propietario del ensamblado que contiene el tipo. Aunque el ámbito de los ensamblados viene determinado por la base de datos y no por el esquema, los ensamblados tienen un propietario que se refleja aquí.|  
|ASSEMBLY_NAME|DBTYPE_WSTR|Nombre del ensamblado que contiene el tipo.|  
|ASSEMBLY_ID|DBTYPE_UI4|Id. de objeto del ensamblado que contiene el tipo.|  
|PERMISSION_SET|DBTYPE_WSTR|Valor que indica el ámbito de acceso del ensamblado. Entre los valores posibles se incluyen "SAFE", "EXTERNAL_ACCESS" y "UNSAFE".|  
|ASSEMBLY_BINARY|DBTYPE_BYTES|Representación binaria del ensamblado.|  
  
#### <a name="the-sql_assemblies_-dependencies-schema-rowset"></a>El conjunto de filas de esquema SQL_ASSEMBLIES_DEPENDENCIES  
 El controlador OLE DB para SQL Server expone un nuevo conjunto de filas de esquema específico del proveedor que describe las dependencias de ensamblado de un servidor especificado. El autor de la llamada puede especificar ASSEMBLY_SERVER como DBTYPE_WSTR, pero no está presente en el conjunto de filas. Si no se especifica, el conjunto de filas tendrá como valor predeterminado el servidor actual. El conjunto de filas de esquema SQL_ASSEMBLY_DEPENDENCIES se define en la tabla siguiente:  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|ASSEMBLY_CATALOG|DBTYPE_WSTR|Nombre de catálogo del ensamblado que contiene el tipo.|  
|ASSEMBLY_SCHEMA|DBTYPE_WSTR|Nombre de esquema o nombre de propietario del ensamblado que contiene el tipo. Aunque el ámbito de los ensamblados viene determinado por la base de datos y no por el esquema, los ensamblados tienen un propietario que se refleja aquí.|  
|ASSEMBLY_ID|DBTYPE_UI4|Id. de objeto del ensamblado.|  
|REFERENCED_ASSEMBLY_ID|DBTYPE_UI4|Id. de objeto del ensamblado al que se hace referencia.|  
  
#### <a name="the-sql_user_types-schema-rowset"></a>El conjunto de filas de esquema SQL_USER_TYPES  
 El controlador OLE DB para SQL Server expone un nuevo conjunto de filas de esquema, SQL_USER_TYPES, que describe cuándo tienen que agregarse los UDT registrados para un servidor especificado. El autor de la llamada debe especificar UDT_SERVER como DBTYPE_WSTR, pero no está presente en el conjunto de filas. El conjunto de filas de esquema SQL_USER_TYPES se define en la tabla siguiente.  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|UDT_NAME|DBTYPE_WSTR|Nombre del ensamblado que contiene la clase UDT.|  
|UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|El nombre de tipo completo (AQN) incluye el nombre de tipo precedido del espacio de nombres, si procede.|  
  
#### <a name="the-columns-schema-rowset"></a>El conjunto de filas de esquema COLUMNS  
 Las adiciones al conjunto de filas de esquema COLUMNS incluyen las columnas siguientes:  
  
|Nombre de la columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|SS_UDT_NAME|DBTYPE_WSTR|Nombre del UDT.|  
|SS_UDT_ASSEMBLY_TYPENAME|DBTYPE_WSTR|El nombre de tipo completo (AQN) incluye el nombre de tipo precedido del espacio de nombres, si procede.|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adiciones y cambios en los conjuntos de propiedades de OLE DB  
 OLE DB Driver for SQL Server agrega nuevos valores o cambios a muchos de los conjuntos de propiedades básicos de OLE DB.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER  
 Para admitir los UDT mediante OLE DB, el controlador OLE DB para SQL Server implementa el nuevo conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER, que contiene los valores siguientes:  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|SSPROP_PARAM_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para los parámetros UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el tipo definido por el usuario.|  
|SSPROP_PARAM_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para los parámetros UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el tipo definido por el usuario.|  
|SSPROP_PARAM_UDT_NAME|DBTYPE_WSTR|Identificador de nombre de tres partes.<br /><br /> Para las columnas UDT, esta propiedad es una cadena que especifica el nombre de una sola parte del tipo definido por el usuario.|  
  
 La propiedad SSPROP_PARAM_UDT_NAME es obligatoria. Las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME son opcionales. Si alguna de las propiedades se especifica de forma incorrecta, se devolverá DB_E_ERRORSINCOMMAND. Si no se especifican las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME, el UDT debe definirse en la misma base de datos y esquema que la tabla. Si la definición UDT no está en el mismo esquema que la tabla (pero está en la misma base de datos), debe especificarse la propiedad SSPROP_PARAM_UDT_SCHEMANAME. Si la definición UDT está en otra base de datos, es necesario especificar las propiedades SSPROP_PARAM_UDT_CATALOGNAME y SSPROP_PARAM_UDT_SCHEMANAME.  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN  
 Para admitir la creación de tablas en la interfaz **ITableDefinition**, el controlador OLE DB para SQL Server agrega las siguientes tres nuevas columnas al conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nombre|Descripción|Tipo|Descripción|  
|----------|-----------------|----------|-----------------|  
|SSPROP_COL_UDT_CATALOGNAME|UDT_CATALOGNAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre del catálogo donde se define el UDT.|  
|SSPROP_COL_UDT_SCHEMANAME|UDT_SCHEMANAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre del esquema donde se define el UDT.|  
|SSPROP_COL_UDT_NAME|UDT_NAME|VT_BSTR|Para las columnas de tipo DBTYPE_UDT, esta propiedad es una cadena que especifica el nombre de una sola parte del UDT. Para otros tipos de columna, esta propiedad devuelve una cadena vacía.|  
  
> [!NOTE]  
>  Los UDT no aparecerán en el conjunto de filas de esquema PROVIDER_TYPES. Todas las columnas tienen acceso de lectura y escritura.  
  
 ADO hará referencia a estas propiedades utilizando la entrada correspondiente de la columna Descripción.  
  
 La propiedad SSPROP_COL_UDTNAME es obligatoria. Las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME son opcionales. Si alguna de las propiedades se especifica de forma incorrecta, se devolverá **DB_E_ERRORSINCOMMAND**.  
  
 Si no se especifican las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME, el UDT debe definirse en la misma base de datos y esquema que la tabla.  
  
 Si la definición UDT no está en el mismo esquema que la tabla (pero está en la misma base de datos), debe especificarse la propiedad SSPROP_COL_UDT_SCHEMANAME.  
  
 Si la definición UDT está en una base de datos diferente, deben especificarse las propiedades SSPROP_COL_UDT_CATALOGNAME y SSPROP_COL_UDT_SCHEMANAME.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adiciones y cambios en las interfaces de OLE DB  
 OLE DB Driver for SQL Server agrega nuevos valores o cambios a muchas de las interfaces básicas de OLE DB.  
  
#### <a name="the-isscommandwithparameters-interface"></a>La interfaz ISSCommandWithParameters  
 Para admitir los UDT mediante OLE DB, el controlador OLE DB para SQL Server implementa diversos cambios, incluida la adición de la interfaz **ISSCommandWithParameters**. Esta nueva interfaz hereda de la interfaz OLE DB básica **ICommandWithParameters**. Además de los tres métodos heredados de **ICommandWithParameters**, **GetParameterInfo**, **MapParameterNames** y **SetParameterInfo**, **ISSCommandWithParameters** proporciona los métodos **GetParameterProperties** y **SetParameterProperties**, que se usan para administrar tipos de datos específicos del servidor.  
  
> [!NOTE]  
>  La interfaz **ISSCommandWithParameters** también usa la nueva estructura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>La interfaz IColumnsRowset  
 Además de la interfaz **ISSCommandWithParameters**, el controlador OLE DB para SQL Server también agrega nuevos valores al conjunto de filas que se devuelve al llamar al método **IColumnsRowset::GetColumnRowset**, incluidos los siguientes.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_UDT_CATALOGNAME|DBTYPE_WSTR|Identificador de nombre de catálogo UDT.|  
|DBCOLUMN_SS_UDT_SCHEMANAME|DBTYPE_WSTR|Identificador de nombre de esquema UDT.|  
|DBCOLUMN_SS_UDT_NAME|DBTYPE_WSTR|Identificador de nombre UDT.|  
|DBCOLUMN_SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Nombre de ensamblado completo, que incluye el nombre de tipo y toda la identificación de ensamblado necesaria a la que debe hacer referencia CLR.|  
  
 Es posible diferenciar una columna UDT del servidor de otros tipos binarios cuando el parámetro DBCOLUMN_TYPE está establecido en DBTYPE_UDT; para ello, es necesario examinar los metadatos UDT agregados especificados en la tabla anterior. Si esos datos están parcialmente completos, el tipo del servidor es un UDT. Para los tipos del servidor que no son UDT, estas columnas se devuelven siempre como NULL.  
 
  
## <a name="see-also"></a>Consulte también  
 [Características del controlador OLE DB para SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
