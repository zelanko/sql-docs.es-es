---
title: Creación de tablas de SQL Server | Microsoft Docs
description: Creación de tablas de SQL Server con OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- OLE DB Driver for SQL Server, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 57c561ed4086221a956c12804f4d90893dc6d2a6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994059"
---
# <a name="creating-sql-server-tables"></a>Crear tablas de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server expone la función **ITableDefinition::CreateTable**, lo que permite a los consumidores crear tablas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los consumidores usan **CreateTable** para crear tablas permanentes con nombres generados por el consumidor y tablas permanentes o temporales con nombres únicos generados por el controlador OLE DB para SQL Server.  
  
 Cuando el consumidor llama a **ITableDefinition::CreateTable**, si el valor de la propiedad DBPROP_TBL_TEMPTABLE es VARIANT_TRUE, el controlador OLE DB para SQL Server genera un nombre de tabla temporal del consumidor. El consumidor establece el parámetro *pTableID* del método **CreateTable** en NULL. Las tablas temporales con nombres generados por el controlador OLE DB para SQL Server no aparecen en el conjunto de filas **TABLES**, pero son accesibles mediante la interfaz **IOpenRowset**.  
  
 Cuando los consumidores especifican el nombre de tabla en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*, el controlador OLE DB para SQL Server crea una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con ese nombre. Se aplican las restricciones de denominación de tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el nombre de tabla puede indicar una tabla permanente o una tabla temporal local o global. Para obtener más información, vea [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md). El parámetro *ppTableID* puede ser NULL.  
  
 OLE DB Driver for SQL Server puede generar los nombres de tablas permanentes o temporales. Cuando el consumidor establece el parámetro *pTableID* en NULL y establece *ppTableID* para que señale a un DBID válido\*, el controlador OLE DB para SQL Server devuelve el nombre generado de la tabla en el miembro *pwszName* de la unión *uName* del DBID al que señala el valor de *ppTableID*. Para crear una tabla temporal con un nombre asignado por el controlador OLE DB para SQL Server, el consumidor incluye la propiedad de tabla DBPROP_TBL_TEMPTABLE de OLE DB en un conjunto de propiedades de tabla al que se hace referencia en el parámetro *rgPropertySets*. Las tablas temporales con nombre de OLE DB Driver for SQL Server son locales.  
  
 **CreateTable** devuelve DB_E_BADTABLEID si el miembro *eKind* del parámetro *pTableID* no indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 El consumidor puede indicar un tipo de datos de columna con el miembro *pwszTypeName* o el miembro *wType*. Si el consumidor especifica el tipo de datos en *pwszTypeName*, OLE DB Driver for SQL Server omite el valor de *wType*.  
  
 Si usa el miembro *pwszTypeName*, el consumidor especifica el tipo de datos con los nombres de tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los nombres de tipo de datos válidos son aquéllos devueltos en la columna TYPE_NAME del conjunto de filas de esquema PROVIDER_TYPES.  
  
 OLE DB Driver for SQL Server reconoce un subconjunto de valores DBTYPE enumerados por OLE DB en el miembro *wType*. Para más información, consulte [Asignación de tipos de datos en ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** devuelve DB_E_BADTYPE si el consumidor establece el miembro *pTypeInfo* o *pclsid* para especificar el tipo de datos de columna.  
  
 El consumidor especifica el nombre de columna en el miembro *pwszName* de la unión *uName* del miembro *dbcid* de DBCOLUMNDESC. El nombre de columna se especifica como una cadena de caracteres Unicode. El miembro *eKind* de *dbcid* debe ser DBKIND_NAME. **CreateTable** devuelve DB_E_BADCOLUMNID si *eKind* no es válido, *pwszName* es NULL o si el valor de *pwszName* no es un identificador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válido.  
  
 Todas las propiedades de columna están disponibles en todas las columnas definidas para la tabla. **CreateTable** puede devolver DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED si los valores de la propiedad se han establecido de un modo que están en conflicto. **CreateTable** devuelve un error cuando la configuración de la propiedad de columna no válida produce un error en la creación de la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Las propiedades de columna de un DBCOLUMNDESC se interpretan como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: Descripción de VARIANT_FALSE: Establece la propiedad de identidad en la columna creada. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la propiedad de identidad es válida para una columna única dentro de una tabla. Al establecer la propiedad en VARIANT_TRUE para más de una columna única, se genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.<br /><br /> La propiedad de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] solo es válida para los tipos de datos **integer**, **numeric** y **decimal** cuando la escala es 0. Al establecer la propiedad en VARIANT_TRUE en una columna de cualquier otro tipo de datos, se genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE no es DBPROPOPTIONS_REQUIRED. Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el miembro DBPROP_COL_NULLABLE de *dwStatus* se establece en DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: crea una restricción DEFAULT de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la columna.<br /><br /> El miembro DBPROP de *vValue* puede ser cualquiera de varios tipos. El miembro *vValue.vt* tiene que especificar un tipo compatible con el tipo de datos de la columna. Por ejemplo, la definición de BSTR N/A como el valor predeterminado para una columna definida como DBTYPE_WSTR es una coincidencia compatible. La definición del mismo valor predeterminado en una columna definida como DBTYPE_R8 genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.|  
|DBPROP_COL_DESCRIPTION|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: el controlador OLE DB Driver for SQL Server no implementa la propiedad de columna DBPROP_COL_DESCRIPTION.<br /><br /> El miembro *dwStatus* de la estructura DBPROP devuelve DBPROPSTATUS_NOTSUPPORTED cuando el consumidor intenta escribir el valor de propiedad.<br /><br /> El establecimiento de la propiedad no constituye un error irrecuperable para OLE DB Driver for SQL Server. Si todos los demás valores de parámetro son válidos, se crea la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: OLE DB Driver for SQL Server usa DBPROP_COL_FIXEDLENGTH para determinar la asignación de tipos de datos cuando el consumidor define el tipo de datos de una columna con el miembro *wType* de DBCOLUMNDESC. Para más información, consulte [Asignación de tipos de datos en ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: al crear la tabla, OLE DB Driver for SQL Server indica si la columna tiene que aceptar valores NULL si se establece la propiedad. Cuando no se establece la propiedad, la capacidad de la columna de aceptar valores NULL como valores está determinada por la opción de base de datos predeterminada ANSI_NULLS de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> OLE DB Driver for SQL Server es un proveedor compatible con ISO. Las sesiones conectadas exhiben los comportamientos ISO. Si el consumidor no establece DBPROP_COL_NULLABLE, las columnas aceptan valores nulos.|  
|DBPROP_COL_PRIMARYKEY|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: Descripción de VARIANT_FALSE: cuando se usa VARIANT_TRUE, OLE DB Driver for SQL Server crea la columna con una restricción PRIMARY KEY.<br /><br /> Cuando se define como una propiedad de columna, solo una columna única puede determinar la restricción. Al establecer la propiedad VARIANT_TRUE para más de una columna única, se devuelve un error cuando el controlador OLE DB para SQL Server intenta crear la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Nota: El consumidor puede usar **IIndexDefinition::CreateIndex** para crear una restricción PRIMARY KEY sobre dos o más columnas.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el miembro *dwStatus* de DBPROP_COL_PRIMARYKEY se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve un error cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_NULLABLE son VARIANT_TRUE.<br /><br /> El controlador OLE DB para SQL Server devuelve un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción PRIMARY KEY en una columna de un tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no válido. No se pueden definir restricciones PRIMARY KEY en las columnas creadas con los tipos de datos **bit**, **text**, **ntext** e **image** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_UNIQUE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: Descripción de VARIANT_FALSE: aplica una restricción UNIQUE de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la columna.<br /><br /> Cuando se define como una propiedad de columna, la restricción solo se aplica en una columna única. El consumidor puede usar **IIndexDefinition::CreateIndex** para aplicar una restricción UNIQUE en los valores combinados de dos o más columnas.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el miembro *dwStatus* de DBPROP_COL_PRIMARYKEY se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con la propiedad de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el miembro DBPROP_COL_NULLABLE de *dwStatus* se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción UNIQUE en una columna de un tipo de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no válido. No se pueden definir restricciones UNIQUE en las columnas creadas con el tipo de datos **bit** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
 Cuando el consumidor llama a **ITableDefinition::CreateTable**, el controlador OLE DB para SQL Server interpreta las propiedades de la tabla como se indica a continuación.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: Descripción de VARIANT_FALSE: de forma predeterminada, OLE DB Driver for SQL Server crea tablas denominadas por el consumidor. Cuando se usa VARIANT_TRUE, OLE DB Driver for SQL Server genera un nombre de tabla temporal para el consumidor. El consumidor establece el parámetro *pTableID* de **CreateTable** en NULL. El parámetro *ppTableID* tiene que contener un puntero válido.|  
  
 Si el consumidor pide que se abra un conjunto de filas en una tabla creada correctamente, el controlador OLE DB para SQL Server abre un conjunto de filas compatible con cursores. Las propiedades del conjunto de filas se pueden indicar en los conjuntos de propiedades pasados.  
  
 En este ejemplo se crea una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
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
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
