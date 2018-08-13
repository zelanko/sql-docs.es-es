---
title: Tipos definidos por el usuario CLR grandes (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large CLR user-defined types [OLE DB]
ms.assetid: 4bf12058-0534-42ca-a5ba-b1c23b24d90f
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 300d8721640d39cc31036b77b5a9223d08adf5dd
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554555"
---
# <a name="large-clr-user-defined-types-ole-db"></a>Tipos definidos por el usuario de CLR grandes (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  En este tema se describen los cambios realizados en OLE DB en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para admitir tipos definidos por el usuario (UDT) de Common Language Runtime (CLR) grandes.  
  
 Para obtener más información sobre la compatibilidad con UDT CLR grandes en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Large CLR User-Defined tipos](../../../relational-databases/native-client/features/large-clr-user-defined-types.md). Para obtener un ejemplo, vea [UDT de CLR grandes uso &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/use-large-clr-udts-ole-db.md).  
  
## <a name="data-format"></a>Formato de datos  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utiliza ~0 para representar la longitud de valores de tamaño ilimitado en tipos de objeto grandes (LOB). ~0 también representa el tamaño de UDT CLR superiores a 8.000 bytes.  
  
 En la tabla siguiente se muestra la asignación de tipos de datos en parámetros y conjuntos de filas:  
  
|Tipo de datos de SQL Server|Tipo de datos de OLE DB|Diseño de memoria|Valor|  
|--------------------------|----------------------|-------------------|-----------|  
|UDT CLR|DBTYPE_UDT|BYTE[](matriz de bytes\)|132 (oledb.h)|  
  
 Los valores UDT se representan como matrices de bytes. Se admiten conversiones a cadenas hexadecimales y desde cadenas hexadecimales. Los valores literales se representan como cadenas hexadecimales con el prefijo "0x". Una cadena hexadecimal es la representación textual de datos binarios en base 16. Un ejemplo sería una conversión del tipo de servidor **varbinary(10)** a DBTYPE_STR, que genera una representación hexadecimal de 20 caracteres donde cada par de caracteres representa un único byte.  
  
## <a name="parameter-properties"></a>Propiedades de parámetros  
 El conjunto de propiedades DBPROPSET_SQLSERVERPARAMETER admite UDT a través de OLE DB. Para obtener más información, vea [Tipos definidos por el usuario de CLR](~/relational-databases/native-client/features/using-user-defined-types.md).  
  
## <a name="column-properties"></a>Propiedades de columna  
 El conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN admite la creación de tablas a través de OLE DB. Para obtener más información, vea [Tipos definidos por el usuario de CLR](~/relational-databases/native-client/features/using-user-defined-types.md).  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Asignar tipo de datos en ITableDefinition::CreateTable  
 Cuando se necesitan columnas UDT, ITableDefinition::CreateTable usa esta información en estructuras **DBCOLUMNDESC**:  
  
|Tipo de datos OLE DB (*wType*)|*pwszTypeName*|Tipo de datos de SQL Server|*rgPropertySets*|  
|----------------------------------|--------------------|--------------------------|----------------------|  
|DBTYPE_UDT|Omitido|UDT|Debe incluir un conjunto de propiedades DBPROPSET_SQLSERVERCOLUMN.|  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La información que se devuelve en la estructura DBPARAMINFO mediante **prgParamInfo** es la que se indica a continuación:  
  
|Tipo de parámetro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|-------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|"DBTYPE_UDT"|*n*|no definido|no definido|clear|  
|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|"DBTYPE_UDT"|~0|no definido|no definido|conjunto|  
  
## <a name="icommandwithparameterssetparameterinfo"></a>ICommandWithParameters::SetParameterInfo  
 La información que se proporciona en la estructura DBPARAMBINDINFO debe cumplir lo siguiente:  
  
|Tipo de parámetro|*pwszDataSourceType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags* DBPARAMFLAGS_ISLONG|  
|--------------------|--------------------------|-------------------|------------------|--------------|------------------------------------|  
|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|DBTYPE_UDT|*n*|no se tiene en cuenta|no se tiene en cuenta|Debe establecerse si el parámetro va a pasarse utilizando DBTYPE_IUNKNOWN.|  
|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|DBTYPE_UDT|~0|no se tiene en cuenta|no se tiene en cuenta|no se tiene en cuenta|  
  
## <a name="isscommandwithparameters"></a>ISSCommandWithParameters  
 Las aplicaciones usan **ISSCommandWithParameters** para obtener y establecer las propiedades de parámetros que se definen en la sección Propiedades de parámetros.  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Éstas son las columnas que se devuelven:  
  
|Tipo de columna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE|DBCOLUMN_FLAGS_ISLONG|DBCOLUMNS_ISSEARCHABLE|DBCOLUMN_OCTETLENGTH|  
|-----------------|--------------------|--------------------------|-------------------------|---------------------|-----------------------------|-----------------------------|---------------------------|  
|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|DBTYPE_UDT|*n*|NULL|NULL|Desactivar|DB_ALL_EXCEPT_LIKE|n|  
|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|DBTYPE_UDT|~0|NULL|NULL|Establecer|DB_ALL_EXCEPT_LIKE|0|  
  
 También se definen las columnas siguientes para los UDT:  
  
|Identificador de columna|Tipo|Descripción|  
|-----------------------|----------|-----------------|  
|DBCOLUMN_UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, nombre del catálogo donde se define el UDT.|  
|DBCOLUMN_UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, nombre del esquema donde se define el UDT.|  
|DBCOLUMN_UDT_NAME|DBTYPE_WSTR|Para las columnas UDT, nombre de una sola parte del UDT.|  
|DBCOLUMN_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Para las columnas UDT, nombre de tipo completo del UDT. El nombre completo del tipo de ensamblado permite crear instancias de un objeto de ese tipo con el método Type.GetType.|  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 La información que se devuelve en la estructura DBCOLUMNINFO es la siguiente:  
  
|Tipo de parámetro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBCOLUMNFLAGS_ISLONG|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------|  
|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|DBTYPE_UDT|*n*|~0|~0|Desactivar|  
|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|DBTYPE_UDT|~0|~0|~0|Establecer|  
  
## <a name="columns-rowset-schema-rowsets"></a>Conjunto de filas COLUMNS (conjuntos de filas de esquema)  
 Para los tipos UDT se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_ISLONG|CHARACTER_OCTET_LENGTH|  
|-----------------|----------------|-----------------------------------------|------------------------------|  
|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|DBTYPE_UDT|Desactivar|*n*|  
|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|DBTYPE_UDT|Establecer|0|  
  
 También se definen las siguientes columnas adicionales para los UDT:  
  
|Identificador de columna|Tipo|Descripción|  
|-----------------------|----------|-----------------|  
|SS_UDT_CATALOGNAME|DBTYPE_WSTR|Para las columnas UDT, nombre del catálogo donde se define el UDT.|  
|SS_UDT_SCHEMANAME|DBTYPE_WSTR|Para las columnas UDT, nombre del esquema donde se define el UDT.|  
|SS_UDT_NAME|DBTYPE_WSTR|Para las columnas UDT, nombre de una sola parte del UDT.|  
|SS_ASSEMBLY_TYPENAME|DBTYPE_WSTR|Para las columnas UDT, se trata del nombre de tipo completo del UDT. El nombre completo del tipo de ensamblado permite crear instancias de un objeto de ese tipo con el método Type.GetType.|  
  
 Con respecto al conjunto de filas PROCEDURE_PARAMETERS, DATA_TYPE contiene los mismos valores que el conjunto de filas de esquema COLUMNS, y TYPE_NAME contiene UDT. También se definen las mismas columnas adicionales.  
  
 Los tipos definidos por el usuario no aparecerán en el conjunto de filas de esquema PROVIDER_TYPES.  
  
## <a name="bindings-and-conversions"></a>Enlaces y conversiones  
  
|Tipo de datos de enlace|UDT a servidor|No UDT a servidor|UDT desde servidor|No UDT desde servidor|  
|----------------------|-------------------|------------------------|---------------------|--------------------------|  
|DBTYPE_UDT|Compatible (5)|Error (1)|Compatible (5)|Error (4)|  
|DBTYPE_BYTES|Compatible (5)|N/D|Compatible (5)|N/D|  
|DBTYPE_WSTR|Compatible (2), (5)|N/D|Compatible (3), (5), (6)|N/D|  
|DBTYPE_BSTR|Compatible (2), (5)|N/D|Compatible (3), (5)|N/D|  
|DBTYPE_STR|Compatible (2), (5)|N/D|Compatible (3), (5)|N/D|  
|DBTYPE_IUNKNOWN|Compatible (6)|N/D|Compatible (6)|N/D|  
|DBTYPE_VARIANT (VT_UI1 &#124; VT_ARRAY)|Compatible (5)|N/D|Compatible (3), (5)|N/D|  
|DBTYPE_VARIANT (VT_BSTR)|Compatible (2), (5)|N/D|N/D|N/D|  
  
### <a name="key-to-symbols"></a>Clave de los símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|1|Si se especifica un tipo de servidor distinto de DBTYPE_UDT con **ICommandWithParameters::SetParameterInfo** y el tipo de descriptor de acceso es DBTYPE_UDT, se produce un error cuando se ejecuta la instrucción.  El error será DB_E_ERRORSOCCURRED y el estado del parámetro será DBSTATUS_E_BADACCESSOR.<br /><br /> Es un error especificar un parámetro de tipo UDT en un parámetro de servidor que no es un UDT.|  
|2|Los datos se convierten de una cadena hexadecimal a datos binarios.|  
|3|Los datos se convierten de datos binarios a una cadena hexadecimal.|  
|4|Puede producirse una validación cuando se usa **CreateAccessor** o **GetNextRows**. El error es DB_E_ERRORSOCCURRED. El estado del enlace se establece en DBBINDSTATUS_UNSUPPORTEDCONVERSION.|  
|5|Puede utilizarse BY_REF.|  
|6|Los parámetros UDT pueden enlazarse como DBTYPE_IUNKNOWN en DBBINDING. El enlace a DBTYPE_IUNKNOWN indica que la aplicación quiere procesar los datos como un flujo mediante la interfaz ISequentialStream. Cuando un consumidor especifica *wType* en un enlace como un tipo DBTYPE_IUNKNOWN y la correspondiente columna o la salida parámetro del procedimiento almacenado es un UDT, SQL Server Native Client devolverá ISequentialStream. Para un parámetro de entrada, SQL Server Native Client consultará la para la interfaz ISequentialStream.<br /><br /> En el caso de UDT grandes, puede decidir no enlazar la longitud de los datos UDT mientras utiliza el enlace DBTYPE_IUNKNOWN. Sin embargo, la longitud debe enlazarse en los UDT pequeños. Un parámetro DBTYPE_UDT puede especificarse como un UDT grande si se cumplen una o varias de las siguientes condiciones:<br />*ulParamParamSize* es ~ 0.<br />DBPARAMFLAGS_ISLONG está establecido en la estructura DBPARAMBINDINFO.<br /><br /> Para los datos de fila, el enlace DBTYPE_IUNKNOWN solamente se permite en los UDT grandes. Puede averiguar si una columna es un tipo UDT grande utilizando el método IColumnsInfo:: GetColumnInfo en un conjunto de filas o IColumnsInfo interfaz del objeto de comandos. Una columna DBTYPE_UDT es una columna UDT grande si se cumplen una o varias de las siguientes condiciones:<br />La marca DBCOLUMNFLAGS_ISLONG se establece en el miembro *dwFlags* de la estructura DBCOLUMNINFO. <br />*ulColumnSize* miembro de DBCOLUMNINFO es ~ 0.|  
  
 DBTYPE_NULL y DBTYPE_EMPTY pueden enlazarse en parámetros de entrada, pero no en parámetros de salida ni en resultados. Cuando se enlazan en parámetros de entrada, el estado debe establecerse en DBSTATUS_S_ISNULL para DBTYPE_NULL o DBSTATUS_S_DEFAULT para DBTYPE_EMPTY. DBTYPE_BYREF no puede utilizarse con DBTYPE_NULL ni con DBTYPE_EMPTY.  
  
 DBTYPE_UDT también puede convertirse a DBTYPE_EMPTY y DBTYPE_NULL. Sin embargo, DBTYPE_NULL y DBTYPE_EMPTY no pueden convertirse a DBTYPE_UDT. Este comportamiento es coherente con el de DBTYPE_BYTES. **ISSCommandWithParameters** se usa para procesar UDT como parámetros.  
  
 Las conversiones de datos que proporcionan los servicios principales de OLE DB (**IDataConvert**) no son aplicables a DBTYPE_UDT.  
  
 No se admite ningún otro enlace.  
  
## <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind  
 En los tipos UDT, solo se admiten las siguientes comparaciones:  
  
-   EQ  
  
-   NE  
  
-   IGNORE  
  
 Si se intenta realizar cualquier otra comparación, se devuelve DB_E_BADCOMPAREOP.  
  
## <a name="bcp-support-for-udts"></a>Compatibilidad de BCP con los UDT  
 Los valores UDT pueden importarse y exportarse solo como valores de caracteres o binarios.  
  
## <a name="down-level-client-behavior-for-udts"></a>Comportamiento del cliente de nivel inferior en los UDT  
 Los UDT están sujetos a la asignación de tipos con clientes de nivel inferior, tal y como se indica a continuación:  
  
|Versión del cliente|DBTYPE_UDT<br /><br /> (longitud menor o igual a 8.000 bytes)|DBTYPE_UDT<br /><br /> (longitud mayor que 8.000 bytes)|  
|--------------------|------------------------------------------------------------------|---------------------------------------------------------|  
|SQL Server 2005|UDT|varbinary(max)|  
|SQL Server 2008 y posterior|UDT|UDT|  
  
 Cuando **DataTypeCompatibility** (SSPROP_INIT_DATATYPECOMPATIBILITY) se establece en "80", los tipos UDT grandes se muestran a los clientes del mismo modo que se muestran a los clientes de nivel inferior.  
  
## <a name="see-also"></a>Vea también  
 [Tipos definidos por el usuario de CLR grandes](~/relational-databases/native-client/features/large-clr-user-defined-types.md)  
  
  

