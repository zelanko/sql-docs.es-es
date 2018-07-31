---
title: Creación de índices de SQL Server | Microsoft Docs
description: Creación de índices de SQL Server mediante el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 6d8f20b4d6b18e6e7c995e3957b51b20cb59d5b3
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39107981"
---
# <a name="creating-sql-server-indexes"></a>Crear índices de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server expone la función **IIndexDefinition::CreateIndex**, que permite a los consumidores definir índices nuevos en las tablas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El controlador OLE DB para SQL Server crea los índices de tabla como índices o restricciones. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da privilegio de creación de restricciones al propietario de la tabla, el propietario de la base de datos y los miembros de ciertos roles administrativos. De forma predeterminada, solamente el propietario de la tabla puede crear un índice en una tabla. Por tanto, que la ejecución de **CreateIndex** sea correcta o no depende no solo de los derechos de acceso del usuario de la aplicación, sino también del tipo de índice creado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El parámetro *pIndexID* puede ser NULL y, si es así, el controlador OLE DB para SQL Server crea un nombre único para el índice. El consumidor puede capturar el nombre del índice especificando un puntero válido a un DBID en el parámetro *ppIndexID*.  
  
 El consumidor puede especificar el nombre del índice como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* del parámetro *pIndexID*. El miembro *eKind* de *pIndexID* debe ser DBKIND_NAME.  
  
 El consumidor especifica la columna o columnas que participan en el índice por nombre. Para cada estructura de DBINDEXCOLUMNDESC usada en **CreateIndex**, el miembro *eKind* de *pColumnID* debe ser DBKIND_NAME. El nombre de la columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en *pColumnID*.  
  
 El controlador OLE DB para SQL Server y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad ascendente por los valores del índice. El controlador OLE DB para SQL Server devuelve E_INVALIDARG si el consumidor especifica DBINDEX_COL_ORDER_DESC en cualquier estructura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta las propiedades del índice como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: controla la agrupación en clústeres de índices.<br /><br /> VARIANT_TRUE: El controlador OLE DB para SQL Server intenta crear un índice agrupado en la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite a lo sumo un índice clúster en cualquier tabla.<br /><br /> VARIANT_FALSE: El controlador OLE DB para SQL Server intenta crear un índice no agrupado en la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla.|  
|DBPROP_INDEX_FILLFACTOR|L/E: lectura y escritura<br /><br /> Predeterminado: 0<br /><br /> Descripción: especifica el porcentaje de una página de índice utilizado para el almacenamiento. Para obtener más información, vea [CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md).<br /><br /> El tipo del variant es VT_I4. El valor debe ser mayor o igual que 1 y menor o igual que 100.|  
|DBPROP_INDEX_INITIALIZE|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE. Descripción: crea el índice como una integridad referencial, restricción PRIMARY KEY.<br /><br /> VARIANT_TRUE: el índice se crea para admitir la restricción PRIMARY KEY de la tabla. Las columnas no deben admitir valores NULL.<br /><br /> VARIANT_FALSE: el índice no se utiliza como una restricción PRIMARY KEY para los valores de fila de la tabla.|  
|DBPROP_INDEX_SORTBOOKMARKS|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|L/E: lectura y escritura<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: El controlador OLE DB para SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|L/E: lectura y escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: crea el índice como una restricción UNIQUE en la columna o columnas participantes.<br /><br /> VARIANT_TRUE: el índice se utiliza para restringir de forma única los valores de fila de la tabla.<br /><br /> VARIANT_FALSE: el índice no restringe de forma exclusiva los valores de fila.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERINDEX, el controlador OLE DB para SQL Server define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
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
  
## <a name="see-also"></a>Ver también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
