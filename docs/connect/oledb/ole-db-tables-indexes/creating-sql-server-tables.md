---
title: Crear tablas de SQL Server | Documentos de Microsoft
description: Crear tablas de SQL Server mediante el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- OLE DB Driver for SQL Server, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 773f0cf781036135faeaaecd29fa3a7e78531708
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="creating-sql-server-tables"></a>Crear tablas de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server expone la **ITableDefinition:: CreateTable** función, lo que permite a los consumidores crear [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tablas. Los consumidores utilizan **CreateTable** para crear tablas permanentes denominadas por el consumidor y tablas permanentes o temporales con nombres únicos generados por el controlador OLE DB para SQL Server.  
  
 Cuando el consumidor llama **ITableDefinition:: CreateTable**, si el valor de la propiedad DBPROP_TBL_TEMPTABLE es VARIANT_TRUE, el controlador OLE DB para SQL Server genera un nombre de tabla temporal para el consumidor. El consumidor establece el *pTableID* parámetro de la **CreateTable** método en NULL. Las tablas temporales con nombres generados por el controlador OLE DB para SQL Server no aparecen en la **tablas** conjunto de filas, pero son accesibles a través de la **IOpenRowset** interfaz.  
  
 Cuando los consumidores especifican el nombre de tabla en la *pwszName* miembro de la *uName* union en la *pTableID* parámetro, el controlador OLE DB para SQL Server crea una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]tabla con ese nombre. Se aplican las restricciones de denominación de tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el nombre de tabla puede indicar una tabla permanente o una tabla temporal local o global. Para obtener más información, consulte [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md). El *ppTableID* parámetro puede ser NULL.  
  
 El controlador OLE DB para SQL Server puede generar los nombres de tablas permanentes o temporales. Cuando el consumidor establece el *pTableID* parámetro en NULL y conjuntos de *ppTableID* para que apunte a un DBID válido\*, el controlador OLE DB para SQL Server devuelve el nombre generado de la tabla en la *pwszName* miembro de la *uName* unión de DBID señalado por el valor de *ppTableID*. Para crear un archivo temporal, el controlador OLE DB para la tabla con nombre de SQL Server, el consumidor incluye la propiedad de tabla DBPROP_TBL_TEMPTABLE de OLE DB en una propiedad de tabla establecido que se hace referencia en el *rgPropertySets* parámetro. Controlador de OLE DB para las tablas temporales con nombre de SQL Server es local.  
  
 **CreateTable** devuelve DB_E_BADTABLEID si el *eKind* miembro de la *pTableID* parámetro no indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 El consumidor puede indicar un tipo de datos de columna mediante el uso del *pwszTypeName* miembro o *wType* miembro. Si el consumidor especifica el tipo de datos en *pwszTypeName*, el controlador OLE DB para SQL Server omite el valor de *wType*.  
  
 Si usa el *pwszTypeName* miembro, el consumidor especifica el tipo de datos mediante el uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nombres de tipo de datos. Los nombres de tipo de datos válidos son aquéllos devueltos en la columna TYPE_NAME del conjunto de filas de esquema PROVIDER_TYPES.  
  
 El controlador OLE DB para SQL Server reconoce un subconjunto de valores DBTYPE enumerados por OLE DB en el *wType* miembro. Para obtener más información, consulte [Data Type Mapping en ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** devuelve DB_E_BADTYPE si el consumidor establece el *Pclsid* o *pTypeInfo* miembro para especificar el tipo de datos de columna.  
  
 El consumidor especifica el nombre de columna en la *pwszName* miembro de la *uName* unión de DBCOLUMNDESC *dbcid* miembro. El nombre de columna se especifica como una cadena de caracteres Unicode. El *eKind* miembro de *dbcid* debe ser DBKIND_NAME. **CreateTable** devuelve DB_E_BADCOLUMNID si *eKind* no es válida, *pwszName* es NULL, o si el valor de *pwszName* no es válido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificador.  
  
 Todas las propiedades de columna están disponibles en todas las columnas definidas para la tabla. **CreateTable** puede devolver DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED si los valores de propiedad se establecen en conflicto. **CreateTable** devuelve un error cuando la configuración de propiedad de columna no válida hace [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] error de creación de la tabla.  
  
 Las propiedades de columna de un DBCOLUMNDESC se interpretan como sigue.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: establece la propiedad de identidad en la columna creada. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la propiedad de identidad es válida para una columna única dentro de una tabla. Establecer la propiedad en VARIANT_TRUE para más de una sola columna genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.<br /><br /> El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propiedad identity solo es válida para el **entero**, **numérico**, y **decimal** tipos cuando la escala es 0. Establecer la propiedad en VARIANT_TRUE en una columna de cualquier otro tipo de datos, genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE no es DBPROPOPTIONS_REQUIRED. Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_NULLABLE *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: crea la restricción DEFAULT de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la columna.<br /><br /> El *vValue* miembro DBPROP puede ser cualquiera de varios tipos. El *vValue.vt* miembro debe especificar un tipo compatible con el tipo de datos de la columna. Por ejemplo, la definición de BSTR N/A como el valor predeterminado para una columna definida como DBTYPE_WSTR es una coincidencia compatible. Definir el mismo valor predeterminado en una columna definida como DBTYPE_R8 genera un error cuando el controlador OLE DB para SQL Server intenta crear la tabla en el servidor.|  
|DBPROP_COL_DESCRIPTION|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: La propiedad de columna DBPROP_COL_DESCRIPTION no se implementa el controlador OLE DB para SQL Server.<br /><br /> El *dwStatus* miembro de la estructura DBPROP devuelve DBPROPSTATUS_NOTSUPPORTED cuando el consumidor intenta escribir el valor de propiedad.<br /><br /> Establecer la propiedad no constituye un error grave para el controlador OLE DB para SQL Server. Si todos los demás valores de parámetro son válidos, se crea la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: El controlador OLE DB para SQL Server utiliza DBPROP_COL_FIXEDLENGTH para determinar la asignación de tipos de datos cuando el consumidor define el tipo de datos de una columna mediante el uso de la *wType* miembro de DBCOLUMNDESC. Para obtener más información, consulte [Data Type Mapping en ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: Cuando se crea la tabla, el controlador OLE DB para SQL Server indica si la columna debe aceptar valores null si se establece la propiedad. Cuando no se establece la propiedad, la capacidad de la columna de aceptar valores NULL como valores está determinada por la opción de base de datos predeterminada ANSI_NULLS de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El controlador OLE DB para SQL Server es un proveedor compatible con ISO. Las sesiones conectadas exhiben los comportamientos ISO. Si el consumidor no establece DBPROP_COL_NULLABLE, las columnas aceptan valores nulos.|  
|DBPROP_COL_PRIMARYKEY|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: cuando VARIANT_TRUE, el controlador OLE DB para SQL Server crea la columna con una restricción PRIMARY KEY.<br /><br /> Cuando se define como una propiedad de columna, solo una columna única puede determinar la restricción. Establecer la propiedad VARIANT_TRUE para más de una sola columna devuelve un error cuando el controlador OLE DB para SQL Server intenta crear la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla.<br /><br /> Nota: El consumidor puede utilizar **IIndexDefinition:: CreateIndex** para crear una restricción PRIMARY KEY en dos o más columnas.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_PRIMARYKEY *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve un error cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_NULLABLE son VARIANT_TRUE.<br /><br /> El controlador OLE DB para SQL Server devuelve un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción PRIMARY KEY en una columna de válido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos. Las restricciones PRIMARY KEY no pueden definirse en las columnas creadas con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos **bits**, **texto**, **ntext**, y **imagen**.|  
|DBPROP_COL_UNIQUE|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: aplica una restricción UNIQUE de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la columna.<br /><br /> Cuando se define como una propiedad de columna, la restricción solo se aplica en una columna única. El consumidor puede utilizar **IIndexDefinition:: CreateIndex** para aplicar una restricción UNIQUE en los valores combinados de dos o más columnas.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_PRIMARYKEY *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_NULLABLE *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El controlador OLE DB para SQL Server devuelve un error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción UNIQUE en una columna de válido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos. No se puede definir restricciones UNIQUE en las columnas creadas con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **bits** tipo de datos.|  
  
 Cuando el consumidor llama **ITableDefinition:: CreateTable**, el controlador OLE DB para SQL Server interpreta las propiedades de la tabla como sigue.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: de forma predeterminada, el controlador OLE DB para SQL Server crea tablas denominadas por el consumidor. Cuando VARIANT_TRUE, el controlador OLE DB para SQL Server genera un nombre de tabla temporal para el consumidor. El consumidor establece el *pTableID* parámetro de **CreateTable** en NULL. El *ppTableID* parámetro debe contener un puntero válido.|  
  
 Si el consumidor solicita que se abra un conjunto de filas en una tabla se creó correctamente, el controlador OLE DB para SQL Server abre un conjunto de filas compatible con cursores. Las propiedades del conjunto de filas se pueden indicar en los conjuntos de propiedades pasados.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
