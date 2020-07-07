---
title: Uso de tipos de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IRowsetChange interface
- IRowsetUpdate interface
- data access [SQL Server Native Client], xml data type
- SQL Server Native Client OLE DB schema rowsets
- PROVIDER_TYPES rowset
- IColumnsInfo interface
- IRowsetFind interface
- IColumnsRowset interface
- PROCEDURE_PARAMETERS rowset
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- IRowset interface
- ISequentialStream interface
- ISSCommandWithParameters interface
- SS_XMLSCHEMA rowset
- SQL Server Native Client OLE DB interfaces
- XML [SQL Server], SQL Server Native Client
- COLUMNS rowset
ms.assetid: a7af5b72-c5c2-418d-a636-ae4ac6270ee5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc526febaed2fd049fb8fa95fd0b0585933fff9b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009832"
---
# <a name="using-xml-data-types"></a>Usar tipos de datos XML
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se ha introducido un tipo de datos **xml** que permite almacenar fragmentos y documentos XML en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El tipo de datos **xml** es un tipo de datos integrado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y es de algún modo similar a otros tipos integrados, como **int** y **varchar**. Al igual que ocurre con otros tipos integrados, el tipo de datos **xml** puede usarse como un tipo de columna al crear una tabla, como un tipo de variable, un tipo de parámetro, un tipo de valor devuelto por una función o en funciones CAST y CONVERT.  
  
## <a name="programming-considerations"></a>Consideraciones sobre la programación  
 El XML puede ser autodescriptivo ya que puede incluir un encabezado XML que especifique la codificación del documento como, por ejemplo:  
  
 `<?xml version="1.0" encoding="windows-1252"?><doc/>`  
  
 El estándar XML describe la forma en que un procesador XML puede detectar la codificación usada en un documento examinando los primeros bytes del documento. Hay ocasiones en que la codificación especificada por la aplicación entra en conflicto con la codificación especificada por el documento. En el caso de los documentos que se pasan como parámetros enlazados, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] trata el XML como datos binarios, por lo que no se realiza ninguna conversión y el analizador XML puede usar la codificación especificada en el documento sin problemas. Sin embargo, en el caso de los datos XML enlazados como WSTR, la aplicación debe asegurarse de que el documento esté codificado como Unicode. Esto puede implicar la carga del documento en un DOM, el cambio de la codificación a Unicode y la serialización del documento. Si no se llevan a cabo estas operaciones, pueden producirse conversiones de datos, lo que daría lugar a un XML no válido o dañado.  
  
 También pueden surgir conflictos cuando el XML se especifica en literales. Por ejemplo, las siguientes instrucciones no son válidas:  
  
 `INSERT INTO xmltable(xmlcol) VALUES('<?xml version="1.0" encoding="UTF-16"?><doc/>')`  
  
 `INSERT INTO xmltable(xmlcol) VALUES(N'<?xml version="1.0" encoding="UTF-8"?><doc/>')`  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 DBTYPE_XML es un nuevo tipo de datos específico de XML del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Además, puede obtenerse acceso a los datos XML a través de los tipos OLE DB existentes DBTYPE_BYTES, DBTYPE_WSTR, DBTYPE_BSTR, DBTYPE_XML, DBTYPE_STR, DBTYPE_VARIANT y DBTYPE_IUNKNOWN. Los datos almacenados en columnas de tipo XML pueden recuperarse de una columna de un conjunto de filas del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con los formatos siguientes:  
  
-   Una cadena de texto  
  
-   Un elemento **ISequentialStream**  
  
> [!NOTE]  
>  El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client no incluye un lector Sax, pero **ISequentialStream** se puede pasar fácilmente a objetos Sax y Dom en MSXML.  
  
 **ISequentialStream** debe usarse para la recuperación de documentos XML de gran tamaño. Las mismas técnicas que se usan para otros tipos de valores grandes también se aplican a XML. Para más información, consulte [Usar tipos de valor grande](../../../relational-databases/native-client/features/using-large-value-types.md).  
  
 Una aplicación también puede recuperar, insertar o actualizar datos almacenados en columnas de tipo XML de un conjunto de filas mediante las interfaces habituales, como **IRow::GetColumns**, **IRowChange::SetColumns** e **ICommand::Execute**. De forma similar al caso de recuperación, un programa de aplicación puede pasar una cadena de texto o una **ISequentialStream** al [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client.  
  
> [!NOTE]  
>  Para enviar datos XML en formato de cadena mediante la interfaz **ISequentialStream**, tiene que obtener **ISequentialStream** especificando DBTYPE_IUNKNOWN y establecer su argumento *pObject* en NULL en el enlace.  
  
 Cuando los datos XML recuperados se truncan debido a que el búfer del consumidor es demasiado pequeño, la longitud puede devolverse como 0xffffffff, lo que significa que no se conoce la longitud. Esto es coherente con su implementación como un tipo de datos que se transmite por secuencias al cliente sin enviar la información de longitud antes que los datos reales. En algunos casos, se puede devolver la longitud real cuando el proveedor ha almacenado en búfer el valor completo, como **IRowset:: GetData** y donde se realiza la conversión de datos.  
  
 El servidor trata los datos XML enviados a SQL Server como datos binarios. Esto impide que se produzcan conversiones y permite al analizador XML detectar automáticamente la codificación XML. De esta forma puede aceptarse una mayor variedad de documentos XML como entrada para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (por ejemplo, los documentos codificados en UTF-8).  
  
 Si el XML de entrada se enlaza como DBTYPE_WSTR, la aplicación debe asegurarse de que se trata de Unicode codificado para evitar cualquier posibilidad de que se produzcan daños a causa de conversiones de datos no deseadas.  
  
### <a name="data-bindings-and-coercions"></a>Enlaces y conversiones de datos  
 En la tabla siguiente, se describen el enlace y la coerción que tienen lugar al usar los tipos de datos enumerados con el tipo de datos  **xml** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
|Tipo de datos|A datos XML<br /><br /> **XML**|A datos XML<br /><br /> **Distinto de XML**|Desde datos XML<br /><br /> **XML**|Desde datos XML<br /><br /> **Distinto de XML**|  
|---------------|---------------------------|--------------------------------|-----------------------------|----------------------------------|  
|DBTYPE_XML|Paso a través<sup>6,7</sup>|Error<sup>1</sup>|Correcto<sup>11, 6</sup>|Error<sup>8</sup>|  
|DBTYPE_BYTES|Paso a través<sup>6,7</sup>|N/D<sup>2</sup>|Correcto<sup>11, 6</sup>|N/D <sup>2</sup>|  
|DBTYPE_WSTR|Paso a través<sup>6,10</sup>|N/D <sup>2</sup>|Correcto<sup>4, 6, 12</sup>|N/D <sup>2</sup>|  
|DBTYPE_BSTR|Paso a través<sup>6,10</sup>|N/D <sup>2</sup>|Correcto<sup>3</sup>|N/D <sup>2</sup>|  
|DBTYPE_STR|Correcto<sup>6, 9, 10</sup>|N/D <sup>2</sup>|Correcto<sup>5, 6, 12</sup>|N/D <sup>2</sup>|  
|DBTYPE_IUNKNOWN|Flujo de bytes mediante **ISequentialStream**<sup>7</sup>|N/D <sup>2</sup>|Flujo de bytes mediante **ISequentialStream**<sup>11</sup>|N/D <sup>2</sup>|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Paso a través<sup>6,7</sup>|N/D <sup>2</sup>|N/D|N/D <sup>2</sup>|  
|DBTYPE_VARIANT (VT_BSTR)|Paso a través<sup>6,10</sup>|N/D <sup>2</sup>|Correcto<sup>3</sup>|N/D <sup>2</sup>|  
  
 <sup>1</sup> Si se especifica un tipo de servidor distinto de DBTYPE_XML con **ICommandWithParameters:: SetParameterInfo** y el tipo de descriptor de acceso es DBTYPE_XML, se produce un error cuando se ejecuta la instrucción (DB_E_ERRORSOCCURRED, el estado del parámetro es DBSTATUS_E_BADACCESSOR); en caso contrario, los datos se envían al servidor, pero el servidor devuelve un error que indica que no hay ninguna conversión implícita de XML al tipo de datos del parámetro.  
  
 <sup>2</sup> Más allá del ámbito de este tema.  
  
 <sup>3</sup>Formato UTF-16, sin marca de orden de bytes (BOM), sin especificación de codificación, sin terminación NULL.  
  
 <sup>4</sup>Formato UTF-16, sin marca BOM, sin especificación de codificación, con terminación NULL.  
  
 <sup>5</sup>Formato de caracteres multibyte codificados en la página de códigos de cliente con terminador NULL. La conversión del Unicode proporcionado por el servidor puede producir daños en los datos, de modo que no se recomienda utilizar este enlace.  
  
 <sup>6</sup>Puede usarse BY_REF.  
  
 <sup>7</sup>Los datos UTF-16 tienen que empezar con una marca BOM. Si no es así, es posible que el servidor no reconozca correctamente la codificación.  
  
 <sup>8</sup>La validación puede producirse en el momento de creación del descriptor de acceso o en el momento de la captura. El error es DB_E_ERRORSOCCURRED, con el estado de enlace establecido en DBBINDSTATUS_UNSUPPORTEDCONVERSION.  
  
 <sup>9</sup>Los datos se convierten a Unicode con la página de códigos del cliente antes de enviarse al servidor. Si la codificación del documento no coincide con la página de códigos del cliente, pueden producirse daños en los datos, por lo que no se recomienda usar este enlace.  
  
 <sup>10</sup>Siempre se agrega la marca BOM a los datos enviados al servidor. Si los datos ya comenzaban con una marca BOM, habrá dos marcas BOM al inicio del búfer. El servidor usa la primera marca BOM para reconocer la codificación como UTF-16 y, después, la descarta. La segunda marca se interpreta como un carácter de espacio de no separación de ancho cero.  
  
 <sup>11</sup>Formato UTF-16 sin especificación de codificación, se agrega una marca BOM a los datos recibidos del servidor. Aunque el servidor devuelva una cadena vacía, se devuelve una marca BOM a la aplicación. Si la longitud del búfer es un número de bytes impar, los datos se truncan correctamente. Si el valor completo se devuelve en fragmentos, estos pueden concatenarse para reconstituir el valor correcto.  
  
 <sup>12</sup> Si la longitud del búfer es inferior a dos caracteres, es decir, no hay espacio suficiente para la terminación de NULL, se genera un error de desbordamiento.  
  
> [!NOTE]  
>  Los valores XML NULL no devuelven ningún dato.  
  
 El estándar XML exige que el XML con codificación UTF-16 comience con una marca de orden de bytes (BOM), el código de carácter UTF-16 0xFEFF. Cuando se trabaja con enlaces WSTR y BSTR, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no requiere ni agrega una marca Bom, ya que la codificación está implícita en el enlace. Cuando se trabaja con enlaces BYTES, XML o IUNKNOWN, se intenta proporcionar simplicidad a la hora de actuar con otros sistemas de almacenamiento y procesadores XML. En este caso, debe haber una marca BOM en el XML con codificación UTF-16 y la aplicación no necesita ocuparse de la codificación real, ya que la mayoría de los procesadores XML (incluido SQL Server) deducen la codificación inspeccionando los primeros bytes del valor. Los datos XML recibidos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mediante enlaces bytes, XML o IUNKNOWN siempre están codificados en UTF-16 con una marca Bom y sin una declaración de codificación incrustada.  
  
 Las conversiones de datos que proporcionan los servicios principales de OLE DB (**IDataConvert**) no pueden aplicarse en DBTYPE_XML.  
  
 La validación se lleva a cabo cuando los datos se envían al servidor. La aplicación debe administrar los cambios de codificación y la validación en el cliente; además, se recomienda no procesar los datos XML directamente sino usar un lector DOM o SAX para procesarlos.  
  
 DBTYPE_NULL y DBTYPE_EMPTY pueden enlazarse en parámetros de entrada, pero no en parámetros de salida ni en resultados. Cuando se enlazan para parámetros de entrada, el estado debe establecerse en DBSTATUS_S_ISNULL o DBSTATUS_S_DEFAULT.  
  
 DBTYPE_XML puede convertirse en DBTYPE_EMPTY y DBTYPE_NULL, DBTYPE_EMPTY puede convertirse en DBTYPE_XML, pero DBTYPE_NULL no puede convertirse en DBTYPE_XML. Este comportamiento es coherente con el de DBTYPE_WSTR.  
  
 DBTYPE_IUNKNOWN es un enlace compatible (tal y como se mostraba en la tabla anterior), pero no hay ninguna conversión entre DBTYPE_XML y DBTYPE_IUNKNOWN. DBTYPE_IUNKNOWN no puede usarse con DBTYPE_BYREF.  
  
### <a name="ole-db-rowset-additions-and-changes"></a>Adiciones y cambios en los conjuntos de filas de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client agrega nuevos valores o cambios a muchos de los conjuntos de filas de esquema de OLE DB básicos.  
  
#### <a name="the-columns-and-procedure_parameters-schema-rowsets"></a>Los conjuntos de filas de esquema COLUMNS y PROCEDURE_PARAMETERS  
 Las adiciones a los conjuntos de filas de esquema COLUMNS y PROCEDURE_PARAMETERS incluyen las columnas siguientes.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Nombre del catálogo donde se define una colección de esquemas XML. Es NULL para una columna no XML o una columna XML sin tipo.|  
|SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Nombre de un esquema donde se define una colección de esquemas XML. Es NULL para una columna no XML o una columna XML sin tipo.|  
|SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Nombre de la colección de esquemas XML. Es NULL para una columna no XML o una columna XML sin tipo.|  
  
#### <a name="the-provider_types-schema-rowset"></a>El conjunto de filas de esquema PROVIDER_TYPES  
 En el conjunto de filas de esquema PROVIDER_TYPES, el valor de COLUMN_SIZE es 0 para el tipo de datos **xml** y DATA_TYPE es DBTYPE_XML.  
  
#### <a name="the-ss_xmlschema-schema-rowset"></a>El conjunto de filas de esquema SS_XMLSCHEMA  
 Se ha introducido un nuevo conjunto de filas de esquema SS_XMLSCHEMA para que los clientes recuperen información del esquema XML. El conjunto de filas SS_XMLSCHEMA contiene las columnas siguientes.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Catálogo al que pertenece una colección XML.|  
|SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Esquema al que pertenece una colección XML.|  
|SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Nombre de una colección de esquemas XML para columnas XML con tipo; de lo contrario, NULL.|  
|TARGETNAMESPACEURI|DBTYPE_WSTR|Espacio de nombres de destino de un esquema XML.|  
|SCHEMACONTENT|DBTYPE_WSTR|Contenido del esquema XML.|  
  
 Los esquemas XML tienen como ámbito el nombre del catálogo, el nombre de esquema, el nombre de la colección de esquemas y el identificador uniforme de recursos (URI) del espacio de nombres de destino. También se define un nuevo GUID con el nombre DBSCHEMA_XML_COLLECTIONS. El número de restricciones y las columnas restringidas del conjunto de filas de esquema SS_XMLSCHEMA se definen tal y como se indica a continuación.  
  
|GUID|Número de restricciones|Columnas restringidas|  
|----------|----------------------------|------------------------|  
|DBSCHEMA_XML_COLLECTIONS|4|SCHEMACOLLECTION_CATALOGNAME<br /><br /> SCHEMACOLLECTION_SCHEMANAME<br /><br /> SCHEMACOLLECTIONNAME<br /><br /> TARGETNAMESPACEURI|  
  
### <a name="ole-db-property-set-additions-and-changes"></a>Adiciones y cambios en los conjuntos de propiedades de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client agrega nuevos valores o cambios a muchos de los conjuntos de propiedades de OLE DB básicos.  
  
#### <a name="the-dbpropset_sqlserverparameter-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER  
 Para admitir el tipo de datos **XML** a través de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa el nuevo conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER, que contiene los valores siguientes.  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Nombre del catálogo (base de datos) donde se define una colección de esquemas XML. Una de las partes del identificador de nombre de tres partes de SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Nombre de un esquema XML de la colección de esquemas. Una de las partes del identificador de nombre de tres partes de SQL.|  
|SSPROP_PARAM_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Nombre de la colección de esquemas XML del catálogo. Una de las partes del identificador de nombre de tres partes de SQL.|  
  
#### <a name="the-dbpropset_sqlservercolumn-property-set"></a>El conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN  
 Para admitir la creación de tablas en la interfaz **ITableDefinition** , [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega tres nuevas columnas al conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN.  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME|VT_BSTR|Para las columnas XML con tipo, esta propiedad es una cadena que especifica el nombre del catálogo donde se almacena el esquema XML. Para otros tipos de columna, esta propiedad devuelve una cadena vacía.|  
|SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME|VT_BSTR|Para las columnas XML con tipo, esta propiedad es una cadena que especifica el nombre del esquema XML que define esta columna.|  
|SSPROP_COL_XML_SCHEMACOLLECTIONNAME|VT_BSTR|Para las columnas XML con tipo, esta propiedad es una cadena que especifica el nombre de la colección de esquemas XML que define el valor.|  
  
 Al igual que los valores de SSPROP_PARAM, todas estas propiedades son opcionales y su valor predeterminado es una cadena vacía. SSPROP_COL_XML_SCHEMACOLLECTION_CATALOGNAME y SSPROP_COL_XML_SCHEMACOLLECTION_SCHEMANAME solo pueden especificarse si se especifica SSPROP_COL_XML_SCHEMACOLLECTIONNAME. Al pasar XML al servidor, si se incluyen estos valores se comprueba su existencia (validez) en la base de datos actual y los datos de instancia se comprueban en el esquema. En todos los casos, para ser válidos, deben estar todos vacíos o todos rellenos.  
  
### <a name="ole-db-interface-additions-and-changes"></a>Adiciones y cambios en las interfaces de OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client agrega nuevos valores o cambios a muchas de las interfaces de OLE DB principales.  
  
#### <a name="the-isscommandwithparameters-interface"></a>La interfaz ISSCommandWithParameters  
 Con el fin de admitir el tipo de datos **XML** a través de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client implementa diversos cambios, incluida la adición de la interfaz [ISSCommandWithParameters](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) . Esta nueva interfaz hereda de la interfaz OLE DB básica **ICommandWithParameters**. Además de los tres métodos heredados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**y **SetParameterInfo**; **ISSCommandWithParameters** proporciona los métodos [GetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md) y [SetParameterProperties](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) que se usan para administrar tipos de datos específicos del servidor.  
  
> [!NOTE]  
>  La interfaz **ISSCommandWithParameters** también usa la nueva estructura SSPARAMPROPS.  
  
#### <a name="the-icolumnsrowset-interface"></a>La interfaz IColumnsRowset  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client agrega las siguientes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] columnas específicas del conjunto de filas devuelto por el método **IColumnRowset:: GetColumnsRowset** . Estas columnas contienen el nombre de tres partes de una colección de esquemas XML. Para las columnas que no son XML o las columnas XML sin tipo, las tres columnas toman el valor predeterminado NULL.  
  
|Nombre de columna|Tipo|Descripción|  
|-----------------|----------|-----------------|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_CATALOGNAME|DBTYPE_WSTR|Catálogo al que pertenece una colección de esquemas XML.<br /><br /> De lo contrario, NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTION_SCHEMANAME|DBTYPE_WSTR|Esquema al que pertenece una colección de esquemas XML. De lo contrario, NULL.|  
|DBCOLUMN_SS_XML_SCHEMACOLLECTIONNAME|DBTYPE_WSTR|Nombre de una colección de esquemas XML para columnas XML con tipo; de lo contrario, NULL.|  
  
#### <a name="the-irowset-interface"></a>La interfaz IRowset  
 La instancia XML de una columna XML se recupera a través del método **IRowset::GetData**. Una instancia XML puede recuperarse como DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML, DBTYPE_STR, DBTYPE_BYTES o como una interfaz a través de DBTYPE_IUNKNOWN, en función del enlace especificado por el cliente. Si el consumidor especifica DBTYPE_BSTR, DBTYPE_WSTR o DBTYPE_VARIANT, el proveedor convierte la instancia XML en el tipo solicitado por el usuario y la coloca en la ubicación especificada en el enlace correspondiente.  
  
 Si el consumidor especifica DBTYPE_IUNKNOWN y establece el argumento *pObject* en NULL o establece el argumento *pObject* en IID_ISequentialStream, el proveedor devuelve una interfaz **ISequentialStream** al consumidor para que este pueda transmitir los datos XML por secuencias fuera de la columna. Después, **ISequentialStream** devuelve los datos XML como una secuencia de caracteres Unicode.  
  
 Al devolver un valor XML enlazado a DBTYPE_IUNKNOWN, el proveedor notifica un valor de tamaño `sizeof (IUnknown *)`. Observe que esto es coherente con el enfoque que se aplica al enlazar una columna como DBTYPE_IUnknown o DBTYPE_IDISPATCH y con el enfoque que aplica DBTYPE_IUNKNOWN/ISequentialStream cuando no puede determinarse el tamaño exacto de la columna.  
  
#### <a name="the-irowsetchange-interface"></a>La interfaz IRowsetChange  
 Un consumidor puede actualizar una instancia XML de una columna de dos formas. La primera, a través del objeto de almacenamiento **ISequentialStream** creado por el proveedor. El consumidor puede llamar al método **ISequentialStream::Write** para actualizar directamente la instancia XML devuelta por el proveedor.  
  
 La segunda, mediante los métodos **IRowsetChange::SetData** o **IRowsetChange::InsertRow**. En este enfoque, puede especificarse una instancia XML del búfer del consumidor en un enlace de tipo DBTYPE_BSTR, DBTYPE_WSTR, DBTYPE_VARIANT, DBTYPE_XML o DBTYPE_IUNKNOWN.  
  
 En caso de DBTYPE_BSTR, DBTYPE_WSTR o DBTYPE_VARIANT, el proveedor almacena la instancia XML que reside en el búfer del consumidor en la columna apropiada.  
  
 En el caso de DBTYPE_IUNKNOWN/ISequentialStream, si el consumidor no especifica ningún objeto de almacenamiento, el consumidor debe crear un objeto **ISequentialStream** de antemano, enlazar el documento XML con el objeto y, a continuación, pasar el objeto al proveedor a través del método **IRowsetChange:: SetData** . El consumidor también puede crear un objeto de almacenamiento, establecer el argumento pObject en IID_ISequentialStream, crear un objeto **ISequentialStream** y, después, pasar el objeto **ISequentialStream** al método **IRowsetChange::SetData**. En ambos casos, el proveedor puede recuperar el objeto XML a través del objeto **ISequentialStream** e insertarlo en una columna apropiada.  
  
#### <a name="the-irowsetupdate-interface"></a>La interfaz IRowsetUpdate  
 La interfaz **IRowsetUpdate** proporciona funciones para las actualizaciones retrasadas. Los datos que se ponen a disposición de los conjuntos de filas no se ponen a disposición de otras transacciones hasta que el consumidor llama al método **IRowsetUpdate: Update** .  
  
#### <a name="the-irowsetfind-interface"></a>La interfaz IRowsetFind  
 El método **IRowsetFind::FindNextRow** no funciona con el tipo de datos **xml**. Cuando se llama a **IRowsetFind::FindNextRow** y el argumento *hAccessor* especifica una columna DBTYPE_XML, se devuelve DB_E_BADBINDINFO. Esto ocurre independientemente del tipo de columna que se esté buscando. En los demás tipos de enlaces, se produce un error en **FindNextRow** con DB_E_BADCOMPAREOP si el tipo de datos de la columna que va a buscarse es **xml**.  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 En el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, se han realizado varios cambios en varias funciones para admitir el tipo de datos **XML** .  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 La función [SQLColAttribute](../../../relational-databases/native-client-odbc-api/sqlcolattribute.md) tiene tres nuevos identificadores de campo, como SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME y SQL_CA_SS _XML_SCHEMACOLLECTION_NAME.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client SQL_SS_LENGTH_UNLIMITED los informes para las columnas SQL_DESC_DISPLAY_SIZE y SQL_DESC_LENGTH.  
  
### <a name="sqlcolumns"></a>SQLColumns  
 La función [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) tiene tres columnas nuevas, entre las que se incluyen SS_XML_SCHEMACOLLECTION_CATALOG_NAME, SS_XML_SCHEMACOLLECTION_SCHEMA_NAME y SS_XML_SCHEMACOLLECTION_NAME. La columna TYPE_NAME existente se usa para indicar el nombre del tipo XML, y el valor DATA_TYPE de una columna o parámetro de tipo XML es SQL_SS_XML.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client SQL_SS_LENGTH_UNLIMITED los valores COLUMN_SIZE y CHAR_OCTET_LENGTH.  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica SQL_SS_LENGTH_UNLIMITED cuando no se puede determinar el tamaño de columna en la función [SQLDescribeCol](../../../relational-databases/native-client-odbc-api/sqldescribecol.md) .  
  
### <a name="sqlgettypeinfo"></a>SQLGetTypeInfo  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client notifica SQL_SS_LENGTH_UNLIMITED como el COLUMN_SIZE máximo del tipo de datos **XML** en la función [SQLGetTypeInfo](../../../relational-databases/native-client-odbc-api/sqlgettypeinfo.md) .  
  
### <a name="sqlprocedurecolumns"></a>SQLProcedureColumns  
 La función [SQLProcedureColumns](../../../relational-databases/native-client-odbc-api/sqlprocedurecolumns.md) tiene las mismas adiciones de columna que la función **SQLColumns** .  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client informa SQL_SS_LENGTH_UNLIMITED como el COLUMN_SIZE máximo del tipo de datos **XML** .  
  
### <a name="supported-conversions"></a>Conversiones admitidas  
 Al convertir tipos de datos de SQL en tipos de datos de C, SQL_C_WCHAR, SQL_C_BINARY y SQL_C_CHAR pueden convertirse en SQL_SS_XML, con las condiciones siguientes:  
  
-   SQL_C_WCHAR: formato UTF-16, sin marca de orden de bytes (BOM), con terminación NULL.  
  
-   SQL_C_BINARY: formato UTF-16, sin terminación NULL. Se agrega una marca BOM a los datos recibidos del servidor. Aunque el servidor devuelva una cadena vacía, se devuelve una marca BOM a la aplicación. Si la longitud de búfer es un número de bytes impar, los datos se truncan correctamente. Si el valor completo se devuelve en fragmentos, éstos pueden concatenarse para reconstituir el valor correcto.  
  
-   SQL_C_CHAR: formato de caracteres multibyte codificados en la página de códigos del cliente con terminación NULL. La conversión del UTF-16 proporcionado por el servidor puede producir daños en los datos, de modo que no se recomienda usar este enlace.  
  
 Al convertir tipos de datos de C en tipos de datos de SQL, SQL_C_WCHAR, SQL_C_BINARY y SQL_C_CHAR pueden convertirse en SQL_SS_XML, con las condiciones siguientes:  
  
-   SQL_C_WCHAR: siempre se agrega una marca BOM a los datos enviados al servidor. Si los datos ya comenzaban con una marca BOM, habrá dos marcas BOM al inicio del búfer. El servidor usa la primera marca para reconocer la codificación como UTF-16 y, a continuación, la descarta. La segunda marca se interpreta como un carácter de espacio de no separación de ancho cero.  
  
-   SQL_C_BINARY: no se realiza ninguna conversión y los datos se pasan al servidor "tal cual". Los datos UTF-16 deben comenzar con una marca BOM; de lo contrario, es posible que el servidor no reconozca correctamente la codificación.  
  
-   SQL_C_CHAR: los datos se convierten a UTF-16 en el cliente y se envían al servidor de la misma forma que SQL_C_WCHAR (incluida la adición de una marca BOM). Si el XML no está codificado en la página de códigos del cliente, pueden producirse daños en los datos.  
  
 El estándar XML exige que el XML con codificación UTF-16 comience con una marca de orden de bytes (BOM), el código de carácter UTF-16 0xFEFF. Cuando se trabaja con un enlace de SQL_C_BINARY, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no requiere ni agrega una marca Bom, ya que la codificación está implícita en el enlace. Se intenta proporcionar simplicidad a la hora de actuar con otros sistemas de almacenamiento y procesadores XML. En este caso, debe haber una marca BOM en el XML con codificación UTF-16 y la aplicación no necesita ocuparse de la codificación real, ya que la mayoría de los procesadores XML (incluido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) deducen la codificación inspeccionando los primeros bytes del valor. Los datos XML recibidos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mediante enlaces de SQL_C_BINARY siempre se codifican en UTF-16 con una marca Bom y sin una declaración de codificación incrustada.  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
