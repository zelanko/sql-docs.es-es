---
title: Compatibilidad con tipos de parámetro con valores de tabla OLE DB | Documentos de Microsoft
description: Compatibilidad con tipos de parámetro de OLE DB Table-Valued
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8f1a20a09e4c15b0dbe84352a4bfbbef59b5d784
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Compatibilidad con tipos de parámetros con valores de tablas de OLE DB
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artículo describe la compatibilidad de tipo de OLE DB para los parámetros con valores de tabla.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de filas de parámetro con valores de tabla  
 Puede crear un objeto de conjunto de filas especializado para parámetros con valores de tabla. Crear el objeto de conjunto de filas de parámetro con valores de tabla mediante ITableDefinitionWithConstraints::CreateTableWithConstraints o IOpenRowset:: OpenRowset. Para ello, establezca la *eKind* miembro de la *pTableID* parámetro en DBKIND_GUID_NAME y suministre CLSID_ROWSET_INMEMORY como el *guid* miembro. El nombre del tipo de servidor para el parámetro con valores de tabla debe especificarse en el *pwszName* miembro de *pTableID* al usar IOpenRowset:: OpenRowset. El objeto de conjunto de filas de parámetro con valores de tabla se comporta como un regular controlador OLE DB para el objeto de SQL Server.  
  
```  
const GUID CLSID_ROWSET_TVP =   
{0xc7ef28d5, 0x7bee, 0x443f, {0x86, 0xda, 0xe3, 0x98, 0x4f, 0xcd, 0x4d, 0xf9}};  
  
CoType RowsetTVP  
{  
[mandatory] interface IAccessor;  
[mandatory] interface IColumnsInfo;  
[mandatory] interface IConvertType;  
[mandatory] interface IRowset;  
[mandatory] interface IRowsetInfo;  
[optional]  interface IColumnsRowset;  
[optional]  interface IRowsetChange;  
[optional]  interface ISupportErrorInfo;  
};  
```  
  
## <a name="dbtypetable"></a>DBTYPE_TABLE  
 DBTYPE_TABLE es un nuevo tipo que representa un tipo de tabla. Este tipo especifica los parámetros con valores de tabla de varias interfaces OLE DB donde se requiere un DBTYPE.  
  
```  
#define DBTYPE_TABLE (143)  
```  
  
 DBTYPE_TABLE tiene el mismo formato que DBTYPE_IUNKNOWN. Es un puntero a un objeto en el búfer de datos. Para una especificación completa en los enlaces, el consumidor rellena al búfer DBOBJECT, con *iid* establecido en una de las interfaces del objeto de conjunto de filas (IID_IRowset). Si no se especifica ningún DBOBJECT en los enlaces, se asumirá IID_IRowset.  
  
 No se admiten conversiones a dbtype_table ni desde DBTYPE_TABLE para cualquier otro tipo. IConvertType::CanConvert devolverá S_FALSE si la conversión no admitida para cualquier solicitud que no sea de DBTYPE_TABLE a la conversión de DBTYPE_TABLE. Esto asume DBCONVERTFLAGS_PARAMETER en el objeto de comando.  
  
## <a name="methods"></a>Métodos  
 Para obtener información acerca de los métodos de OLE DB que admiten parámetros con valores de tabla, vea [OLE DB Table-Valued parámetro tipo admite &#40;métodos&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propiedades  
 Para obtener información acerca de las propiedades de OLE DB que admiten parámetros con valores de tabla, vea [OLE DB Table-Valued parámetro tipo admite &#40;propiedades&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
