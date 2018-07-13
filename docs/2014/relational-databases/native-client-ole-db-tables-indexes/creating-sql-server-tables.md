---
title: Creación de tablas de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0c56c25e5904a65fdbf24e4b3bcf7a2c98d9c7a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429394"
---
# <a name="creating-sql-server-tables"></a>Crear tablas de SQL Server
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **ITableDefinition:: CreateTable** función, lo que permite a los consumidores crear [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas. Los consumidores usan **CreateTable** para crear tablas permanentes denominadas por el consumidor y tablas permanentes o temporales con nombres únicos generados por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.  
  
 Cuando el consumidor llama a **ITableDefinition:: CreateTable**, si el valor de la propiedad DBPROP_TBL_TEMPTABLE es VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client genera un nombre de tabla temporal para el consumidor. El consumidor establece el *pTableID* parámetro de la **CreateTable** método en NULL. Las tablas temporales con nombres generados por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no aparecen en la **tablas** conjunto de filas, pero son accesibles a través de la **IOpenRowset** interfaz.  
  
 Cuando los consumidores especifican el nombre de tabla en la *pwszName* miembro de la *uName* union en la *pTableID* parámetro, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB crea un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla con ese nombre. Se aplican las restricciones de denominación de tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el nombre de tabla puede indicar una tabla permanente o una tabla temporal local o global. Para obtener más información, consulte [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql). El *ppTableID* parámetro puede ser NULL.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client puede generar los nombres de tablas permanentes o temporales. Cuando el consumidor establece el *pTableID* parámetro en NULL y establece *ppTableID* para que apunte a un DBID válido\*, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve el nombre generado de la tabla en la *pwszName* miembro de la *uName* unión de DBID señalada por el valor de *ppTableID*. Para crear un archivo temporal, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla denominadas por el proveedor OLE DB de Native Client, el consumidor incluye la propiedad de tabla DBPROP_TBL_TEMPTABLE de OLE DB en una propiedad de tabla establecida que se hace referencia en el *rgPropertySets* parámetro. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB denominadas por el proveedor las tablas temporales son locales.  
  
 **CreateTable** devuelve DB_E_BADTABLEID si el *eKind* miembro de la *pTableID* parámetro no indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 El consumidor puede indicar un tipo de datos de columna mediante el uso del *pwszTypeName* miembro o el *wType* miembro. Si el consumidor especifica el tipo de datos en *pwszTypeName*, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client omite el valor de *wType*.  
  
 Si usa el *pwszTypeName* miembro, el consumidor especifica el tipo de datos mediante el uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los nombres de tipo de datos. Los nombres de tipo de datos válidos son aquéllos devueltos en la columna TYPE_NAME del conjunto de filas de esquema PROVIDER_TYPES.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client reconoce un subconjunto de valores DBTYPE enumerados por OLE DB en el *wType* miembro. Para obtener más información, consulte [asignación de tipos de datos en ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** devuelve DB_E_BADTYPE si el consumidor establece el el *pTypeInfo* o *pTypeInfo* miembro para especificar el tipo de datos de columna.  
  
 El consumidor especifica el nombre de columna en la *pwszName* miembro de la *uName* union de DBCOLUMNDESC *dbcid* miembro. El nombre de columna se especifica como una cadena de caracteres Unicode. El *eKind* miembro de *dbcid* debe ser DBKIND_NAME. **CreateTable** devuelve DB_E_BADCOLUMNID si *eKind* no es válido, *pwszName* es NULL, o si el valor de *pwszName* no es válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador.  
  
 Todas las propiedades de columna están disponibles en todas las columnas definidas para la tabla. **CreateTable** puede devolver DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED si los valores de propiedad se establece en conflicto. **CreateTable** devuelve un error al hacer que los valores de propiedad de columna no válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error de creación de la tabla.  
  
 Las propiedades de columna de un DBCOLUMNDESC se interpretan como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: establece la propiedad de identidad en la columna creada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la propiedad de identidad es válida para una columna única dentro de una tabla. Establecer la propiedad en VARIANT_TRUE para más de una sola columna genera un error cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear la tabla en el servidor.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad identity sólo es válida para el **entero**, **numérico**, y **decimal** tipos cuando la escala es 0. Si la propiedad en VARIANT_TRUE en una columna de cualquier otro tipo de datos genera un error cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear la tabla en el servidor.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE no es DBPROPOPTIONS_ Obligatorio. Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_AUTOINCREMENT y DBPROP_COL_NULLABLE son VARIANT_TRUE y *dwOption* de DBPROP_COL_NULLABLE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_NULLABLE *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|L/E lectura/escritura<br /><br /> Predeterminado: ninguno<br /><br /> Descripción: crea la restricción DEFAULT de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la columna.<br /><br /> El *vValue* miembro DBPROP puede ser cualquier número de tipos. El *vValue.vt* miembro debe especificar un tipo compatible con el tipo de datos de la columna. Por ejemplo, la definición de BSTR N/A como el valor predeterminado para una columna definida como DBTYPE_WSTR es una coincidencia compatible. Definir el mismo valor predeterminado en una columna definida como DBTYPE_R8 genera un error cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear la tabla en el servidor.|  
|DBPROP_COL_DESCRIPTION|L/E lectura/escritura<br /><br /> Predeterminado: ninguno<br /><br /> Descripción: La propiedad de columna DBPROP_COL_DESCRIPTION no implementa la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.<br /><br /> El *dwStatus* miembro de la estructura DBPROP devuelve DBPROPSTATUS_NOTSUPPORTED cuando el consumidor intenta escribir el valor de propiedad.<br /><br /> Establecer la propiedad no constituye un error irrecuperable para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB. Si todos los demás valores de parámetro son válidos, se crea la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client utiliza DBPROP_COL_FIXEDLENGTH para determinar la asignación de tipos de datos cuando el consumidor define el tipo de datos de una columna mediante el uso de la *wType* miembro de DBCOLUMNDESC. Para obtener más información, consulte [asignación de tipos de datos en ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|L/E lectura/escritura<br /><br /> Predeterminado: ninguno<br /><br /> Descripción: Al crear la tabla, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client indica si la columna debe aceptar valores null si la propiedad está establecida. Cuando no se establece la propiedad, la capacidad de la columna de aceptar valores NULL como valores está determinada por la opción de base de datos predeterminada ANSI_NULLS de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB es un proveedor compatible con ISO. Las sesiones conectadas exhiben los comportamientos ISO. Si el consumidor no establece DBPROP_COL_NULLABLE, las columnas aceptan valores nulos.|  
|DBPROP_COL_PRIMARYKEY|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: cuando VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea la columna con una restricción PRIMARY KEY.<br /><br /> Cuando se define como una propiedad de columna, solo una columna única puede determinar la restricción. Establecer la propiedad VARIANT_TRUE para más de una sola columna devuelve un error cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.<br /><br /> Nota: El consumidor puede utilizar **IIndexDefinition:: CreateIndex** para crear una restricción PRIMARY KEY en dos o más columnas.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* de DBPROP_COL_UNIQUE es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_PRIMARYKEY *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_NULLABLE son VARIANT_TRUE.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción PRIMARY KEY en una columna de válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos. No se puede definir restricciones PRIMARY KEY en las columnas creadas con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos **bit**, **texto**, **ntext**, y **imagen**.|  
|DBPROP_COL_UNIQUE|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: aplica una restricción UNIQUE de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la columna.<br /><br /> Cuando se define como una propiedad de columna, la restricción solo se aplica en una columna única. El consumidor puede utilizar **IIndexDefinition:: CreateIndex** para aplicar una restricción UNIQUE en los valores combinados de dos o más columnas.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_PRIMARYKEY y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_PRIMARYKEY *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* no es DBPROPOPTIONS_REQUIRED.<br /><br /> Se devuelve DB_E_ERRORSOCCURRED cuando DBPROP_COL_NULLABLE y DBPROP_COL_UNIQUE son VARIANT_TRUE y *dwOption* es igual a DBPROPOPTIONS_REQUIRED. La columna se define con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad de identidad y el DBPROP_COL_NULLABLE *dwStatus* miembro se establece en DBPROPSTATUS_CONFLICTING.<br /><br /> El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando el consumidor intenta crear una restricción UNIQUE en una columna de válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos. No se puede definir restricciones UNIQUE en las columnas creadas con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** tipo de datos.|  
  
 Cuando el consumidor llama a **ITableDefinition:: CreateTable**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client interpreta las propiedades de la tabla como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: de forma predeterminada, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea tablas denominadas por el consumidor. Cuando VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client genera un nombre de tabla temporal para el consumidor. El consumidor establece el *pTableID* parámetro de **CreateTable** en NULL. El *ppTableID* parámetro debe contener un puntero válido.|  
  
 Si el consumidor solicita que se puede abrir un conjunto de filas en una tabla se creó correctamente, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client abre un conjunto de filas compatible con cursores. Las propiedades del conjunto de filas se pueden indicar en los conjuntos de propiedades pasados.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
