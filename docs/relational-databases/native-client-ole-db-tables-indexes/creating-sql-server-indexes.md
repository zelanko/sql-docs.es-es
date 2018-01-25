---
title: "Creación de índices de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-tables-indexes
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
- adding indexes
ms.assetid: 6239d440-2818-4b98-bb79-732dced41952
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72d112e951b940a0eb424e79bc431237bcf06d0d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="creating-sql-server-indexes"></a>Crear índices de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **IIndexDefinition:: CreateIndex** función, lo que permite a los consumidores definir índices nuevos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea los índices de tabla como índices o restricciones. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da privilegio de creación de restricciones al propietario de la tabla, el propietario de la base de datos y los miembros de ciertos roles administrativos. De forma predeterminada, solamente el propietario de la tabla puede crear un índice en una tabla. Por lo tanto, el éxito o fracaso de **CreateIndex** depende no solo de derechos de acceso del usuario de la aplicación sino también en el tipo de índice creado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pTableID* parámetro. El *eKind* miembro de *pTableID* debe ser DBKIND_NAME.  
  
 El *pIndexID* parámetro puede ser NULL, si es así, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client crea un nombre único para el índice. El consumidor puede capturar el nombre del índice mediante la especificación de un puntero válido a un DBID en el *ppIndexID* parámetro.  
  
 El consumidor puede especificar el nombre del índice como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union de la *pIndexID* parámetro. El *eKind* miembro de *pIndexID* debe ser DBKIND_NAME.  
  
 El consumidor especifica la columna o columnas que participan en el índice por nombre. Para cada estructura DBINDEXCOLUMNDESC utilizada en **CreateIndex**, *eKind* miembro de la *pColumnID* debe ser DBKIND_NAME. El nombre de la columna se especifica como una cadena de caracteres Unicode en el *pwszName* miembro de la *uName* union en la *pColumnID*.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten el orden ascendente de valores en el índice. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve E_INVALIDARG si el consumidor especifica DBINDEX_COL_ORDER_DESC en cualquier estructura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta las propiedades del índice como sigue.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: controla la agrupación en clústeres de índices.<br /><br /> VARIANT_TRUE: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear un índice agrupado en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite a lo sumo un índice clúster en cualquier tabla.<br /><br /> VARIANT_FALSE: La [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client intenta crear un índice no agrupado en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.|  
|DBPROP_INDEX_FILLFACTOR|L/E lectura/escritura<br /><br /> Valor predeterminado: 0<br /><br /> Descripción: especifica el porcentaje de una página de índice utilizado para el almacenamiento. Para obtener más información, consulte [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md).<br /><br /> El tipo del variant es VT_I4. El valor debe ser mayor o igual que 1 y menor o igual que 100.|  
|DBPROP_INDEX_INITIALIZE|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: crea el índice como una integridad referencial, restricción PRIMARY KEY.<br /><br /> VARIANT_TRUE: el índice se crea para admitir la restricción PRIMARY KEY de la tabla. Las columnas no deben admitir valores NULL.<br /><br /> VARIANT_FALSE: el índice no se utiliza como una restricción PRIMARY KEY para los valores de fila de la tabla.|  
|DBPROP_INDEX_SORTBOOKMARKS|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|L/E lectura/escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no admite esta propiedad. Intenta establecer la propiedad **CreateIndex** hacer que un valor devuelto de DB_S_ERRORSOCCURRED. El *dwStatus* miembro de la estructura de la propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|L/E lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: crea el índice como una restricción UNIQUE en la columna o columnas participantes.<br /><br /> VARIANT_TRUE: el índice se utiliza para restringir de forma única los valores de fila de la tabla.<br /><br /> VARIANT_FALSE: el índice no restringe de forma exclusiva los valores de fila.|  
  
 En la propiedad específica del proveedor establezca DBPROPSET_SQLSERVERINDEX, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define la siguiente propiedad de información de origen de datos.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Tipo: VT_BOOL (L/E)<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: cuando esta propiedad se especifica con un valor de VARIANT_TRUE con IIndexDefinition::CreateIndex, da como resultado la creación de un índice xml primario correspondiente a la columna que se está indizando. Si esta propiedad es VARIANT_TRUE, cIndexColumnDescs debe ser 1, de lo contrario es un error.|  
  
 En este ejemplo se crea un índice de la clave principal:  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Vea también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
