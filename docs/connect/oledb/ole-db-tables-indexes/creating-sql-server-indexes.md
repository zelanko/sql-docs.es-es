---
title: Creación de índices de SQL Server (controlador OLE DB) | Microsoft Docs
description: OLE DB Driver for SQL Server expone la función IIndexDefinition::CreateIndex, que permite a los consumidores definir índices nuevos en las tablas de SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e0868c24fe17c7c386ca78198e72e74a5be6cde
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88858765"
---
# <a name="creating-sql-server-indexes"></a>Crear índices de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server expone la función **IIndexDefinition::CreateIndex**, que permite a los consumidores definir índices nuevos en las tablas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 OLE DB Driver for SQL Server crea índices de tabla como índices o restricciones. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da privilegio de creación de restricciones al propietario de la tabla, el propietario de la base de datos y los miembros de ciertos roles administrativos. De forma predeterminada, solamente el propietario de la tabla puede crear un índice en una tabla. Por tanto, que la ejecución de **CreateIndex** sea correcta o no depende no solo de los derechos de acceso del usuario de la aplicación, sino también del tipo de índice creado.  
  
 Los consumidores especifican el nombre de tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
 El parámetro *pIndexID* puede ser NULL y, si es así, el controlador OLE DB para SQL Server crea un nombre único para el índice. El consumidor puede capturar el nombre del índice especificando un puntero válido a un DBID en el parámetro *ppIndexID*.  
  
 El consumidor puede especificar el nombre del índice como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* del parámetro *pIndexID*. El miembro *eKind* de *pIndexID* debe ser DBKIND_NAME.  
  
 El consumidor especifica la columna o columnas que participan en el índice por nombre. Para cada estructura de DBINDEXCOLUMNDESC usada en **CreateIndex**, el miembro *eKind* de *pColumnID* debe ser DBKIND_NAME. El nombre de la columna se especifica como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en *pColumnID*.  
  
 OLE DB Driver for SQL Server y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admiten el orden ascendente en los valores del índice. El controlador OLE DB para SQL Server devuelve E_INVALIDARG si el consumidor especifica DBINDEX_COL_ORDER_DESC en cualquier estructura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta las propiedades del índice como sigue.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: controla la agrupación en clústeres de índices.<br /><br /> VARIANT_TRUE: OLE DB Driver for SQL Server intenta crear un índice agrupado en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite a lo sumo un índice clúster en cualquier tabla.<br /><br /> VARIANT_FALSE: OLE DB Driver for SQL Server intenta crear un índice no agrupado en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_INDEX_FILLFACTOR|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: 0<br /><br /> Descripción: especifica el porcentaje de una página de índice usado para el almacenamiento. Para obtener más información, vea [CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md).<br /><br /> El tipo del variant es VT_I4. El valor debe ser mayor o igual que 1 y menor o igual que 100.|  
|DBPROP_INDEX_INITIALIZE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: Descripción de VARIANT_FALSE: crea el índice como una restricción PRIMARY KEY de integridad referencial.<br /><br /> VARIANT_TRUE: el índice se crea para admitir la restricción PRIMARY KEY de la tabla. Las columnas no deben admitir valores NULL.<br /><br /> VARIANT_FALSE: el índice no se usa como una restricción PRIMARY KEY para los valores de fila de la tabla.|  
|DBPROP_INDEX_SORTBOOKMARKS|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: None<br /><br /> Descripción: OLE DB Driver for SQL Server no admite esta propiedad. Los intentos de establecer la propiedad en **CreateIndex** producen un valor devuelto de DB_S_ERRORSOCCURRED. El miembro *dwStatus* de la estructura de propiedad indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: crea el índice como una restricción UNIQUE en la columna o columnas participantes.<br /><br /> VARIANT_TRUE: el índice se usa para restringir de forma única los valores de fila de la tabla.<br /><br /> VARIANT_FALSE: el índice no restringe de forma exclusiva los valores de fila.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERINDEX, el controlador OLE DB para SQL Server define las siguientes propiedades de información del origen de datos.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Escriba:  VT_BOOL (L/E)<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: cuando esta propiedad se especifica con un valor de VARIANT_TRUE con IIndexDefinition::CreateIndex, da como resultado la creación de un índice XML primario correspondiente a la columna que se indexa. Si esta propiedad es VARIANT_TRUE, cIndexColumnDescs debe ser 1, de lo contrario es un error.|  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
