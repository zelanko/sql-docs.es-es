---
title: Creación de tablas de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f3d1ae29828e18cf98941666e7884e70115ba39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301870"
---
# <a name="creating-sql-server-tables"></a>Crear tablas de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la función **ITableDefinition::CreateTable,** lo que permite a los consumidores crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas. Los consumidores usan **CreateTable** para crear tablas permanentes con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor y tablas permanentes o temporales con nombres únicos generados por el proveedor OLE DB de Native Client.  
  
 Cuando el consumidor llama a **ITableDefinition::CreateTable**, si el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valor de la propiedad DBPROP_TBL_TEMPTABLE es VARIANT_TRUE, el proveedor OLE DB de Native Client genera un nombre de tabla temporal para el consumidor. El consumidor establece el parámetro *pTableID* del método **CreateTable** en NULL. Las tablas temporales con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombres generados por el proveedor OLE DB de Native Client no aparecen en el conjunto de filas **TABLES,** pero son accesibles a través de la **interfaz IOpenRowset.**  
  
 Cuando los consumidores especifican el nombre de la tabla en el miembro *pwszName* de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unión *uName* en el parámetro *pTableID,* el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea una tabla con ese nombre. Se aplican las restricciones de denominación de tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el nombre de tabla puede indicar una tabla permanente o una tabla temporal local o global. Para obtener más información, consulte [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md). El parámetro *ppTableID* puede ser NULL.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client puede generar los nombres de tablas permanentes o temporales. Cuando el consumidor establece el parámetro *pTableID* en NULL y establece\* *ppTableID* para que apunte a un DBID válido , el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve el nombre generado de la tabla en el miembro *pwszName* de la unión *uName* de la DBID señalada por el valor de *ppTableID*. Para crear una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla temporal con nombre de proveedor OLE DB de Native Client, el consumidor incluye la propiedad de tabla OLE DB DBPROP_TBL_TEMPTABLE en un conjunto de propiedades de tabla al que se hace referencia en el parámetro *rgPropertySets.* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Las tablas temporales con nombre de proveedor OLE DB de Native Client son locales.  
  
 **CreateTable** devuelve DB_E_BADTABLEID si el miembro *eKind* del parámetro *pTableID* no indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 El consumidor puede indicar un tipo de datos de columna con el miembro *pwszTypeName* o el miembro *wType*. Si el consumidor especifica el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en *pwszTypeName*, el proveedor OLE DB de Native Client omite el valor de *wType*.  
  
 Si usa el miembro *pwszTypeName*, el consumidor especifica el tipo de datos con los nombres de tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los nombres de tipo de datos válidos son aquéllos devueltos en la columna TYPE_NAME del conjunto de filas de esquema PROVIDER_TYPES.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client reconoce un subconjunto de valores DBTYPE enumerados por OLE DB en el miembro *wType.* Para más información, consulte [Asignación de tipos de datos en ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** devuelve DB_E_BADTYPE si el consumidor establece el miembro *pTypeInfo* o *pclsid* para especificar el tipo de datos de columna.  
  
 El consumidor especifica el nombre de columna en el miembro *pwszName* de la unión *uName* del miembro *dbcid* de DBCOLUMNDESC. El nombre de columna se especifica como una cadena de caracteres Unicode. El miembro *eKind* de *dbcid* debe ser DBKIND_NAME. **CreateTable** devuelve DB_E_BADCOLUMNID si *eKind* no es válido, *pwszName* es NULL o si el valor de *pwszName* no es un identificador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido.  
  
 Todas las propiedades de columna están disponibles en todas las columnas definidas para la tabla. **CreateTable** puede devolver DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED si los valores de la propiedad se han establecido de un modo que están en conflicto. **CreateTable** devuelve un error cuando la configuración de la propiedad de columna no válida produce un error en la creación de la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Las propiedades de columna de un DBCOLUMNDESC se interpretan como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: establece la propiedad de identidad en la columna creada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la propiedad de identidad es válida para una columna única dentro de una tabla. Establecer la propiedad en VARIANT_TRUE para más de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una sola columna genera un error cuando el proveedor OLE DB de Native Client intenta crear la tabla en el servidor.<br /><br /> La propiedad de identidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo es válida para los tipos de datos **integer**, **numeric** y **decimal** cuando la escala es 0. Establecer la propiedad en VARIANT_TRUE en una columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cualquier otro tipo de datos genera un error cuando el proveedor OLE DB de Native Client intenta crear la tabla en el servidor.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *el dwOption* de DBPROP_COL_NULLABLE no está DBPROPOPTIONS_REQUIRED. Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el miembro DBPROP_COL_NULLABLE de *dwStatus* se establece en DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: crea la restricción DEFAULT de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la columna.<br /><br /> El miembro DBPROP de *vValue* puede ser cualquiera de varios tipos. El miembro *vValue.vt* tiene que especificar un tipo compatible con el tipo de datos de la columna. Por ejemplo, la definición de BSTR N/A como el valor predeterminado para una columna definida como DBTYPE_WSTR es una coincidencia compatible. Definir el mismo valor predeterminado en una columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definida como DBTYPE_R8 genera un error cuando el proveedor OLE DB de Native Client intenta crear la tabla en el servidor.|  
|DBPROP_COL_DESCRIPTION|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: el proveedor OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cliente nativo no implementa la propiedad de columna DBPROP_COL_DESCRIPTION.<br /><br /> El miembro *dwStatus* de la estructura DBPROP devuelve DBPROPSTATUS_NOTSUPPORTED cuando el consumidor intenta escribir el valor de propiedad.<br /><br /> Establecer la propiedad no constituye un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error grave para el proveedor OLE DB de native Client. Si todos los demás valores de parámetro son válidos, se crea la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el proveedor OLE DB de Native Client usa DBPROP_COL_FIXEDLENGTH para determinar la asignación de tipos de datos cuando el consumidor define el tipo de datos de una columna mediante el miembro *wType* de DBCOLUMNDESC. Para más información, consulte [Asignación de tipos de datos en ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: al crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la tabla, el proveedor OLE DB de Native Client indica si la columna debe aceptar valores nulos si se establece la propiedad. Cuando no se establece la propiedad, la capacidad de la columna de aceptar valores NULL como valores está determinada por la opción de base de datos predeterminada ANSI_NULLS de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client es un proveedor compatible con ISO. Las sesiones conectadas exhiben los comportamientos ISO. Si el consumidor no establece DBPROP_COL_NULLABLE, las columnas aceptan valores nulos.|  
|DBPROP_COL_PRIMARYKEY|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE Descripción: cuando VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea la columna con una restricción PRIMARY KEY.<br /><br /> Cuando se define como una propiedad de columna, solo una columna única puede determinar la restricción. Establecer la propiedad VARIANT_TRUE para más de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sola columna devuelve un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error cuando el proveedor OLE DB de Native Client intenta crear la tabla.<br /><br /> Nota: El consumidor puede usar **IIndexDefinition::CreateIndex** para crear una restricción PRIMARY KEY en dos o más columnas.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *el dwOption* de DBPROP_COL_UNIQUE no está DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el miembro *dwStatus* de DBPROP_COL_PRIMARYKEY se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_NULLABLE son VARIANT_TRUE.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelve un error desde que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor intenta crear una restricción PRIMARY KEY en una columna de tipo de datos no válido. No se pueden definir restricciones PRIMARY KEY en las columnas creadas con los tipos de datos **bit**, **text**, **ntext** e **image** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_UNIQUE|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: aplica una restricción UNIQUE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la columna.<br /><br /> Cuando se define como una propiedad de columna, la restricción solo se aplica en una columna única. El consumidor puede usar **IIndexDefinition::CreateIndex** para aplicar una restricción UNIQUE en los valores combinados de dos o más columnas.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no está DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el miembro *dwStatus* de DBPROP_COL_PRIMARYKEY se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no está DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el miembro DBPROP_COL_NULLABLE de *dwStatus* se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client devuelve un error desde que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el consumidor intenta crear una restricción UNIQUE en una columna de tipo de datos no válido. No se pueden definir restricciones UNIQUE en las columnas creadas con el tipo de datos  **bit** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Cuando el consumidor llama a **ITableDefinition::CreateTable**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client interpreta las propiedades de la tabla de la siguiente manera.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|L/E: lectura y escritura<br /><br /> Valor predeterminado: descripción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_FALSE: de forma predeterminada, el proveedor OLE DB de Native Client crea tablas con nombre para el consumidor. Cuando VARIANT_TRUE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el proveedor OLE DB de Native Client genera un nombre de tabla temporal para el consumidor. El consumidor establece el parámetro *pTableID* de **CreateTable** en NULL. El parámetro *ppTableID* tiene que contener un puntero válido.|  
  
 Si el consumidor solicita que se abra un conjunto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de filas en una tabla creada correctamente, el proveedor OLE DB de Native Client abre un conjunto de filas compatible con cursores. Las propiedades del conjunto de filas se pueden indicar en los conjuntos de propiedades pasados.  
  
 En este ejemplo se crea una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
