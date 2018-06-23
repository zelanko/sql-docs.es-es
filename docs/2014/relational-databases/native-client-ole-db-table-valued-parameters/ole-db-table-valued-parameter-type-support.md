---
title: Compatibilidad con tipos de parámetro con valores de tabla OLE DB | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (OLE DB)
ms.assetid: 147036a0-260e-4f81-8b3b-89209e023a32
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4b6416715cc6226766773d3f1d630dc2e42e1e37
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196209"
---
# <a name="ole-db-table-valued-parameter-type-support"></a>Compatibilidad con tipos de parámetros con valores de tablas de OLE DB
  En este tema se describe la compatibilidad de tipos OLE DB para parámetros con valores de tabla.  
  
## <a name="table-valued-parameter-rowset-object"></a>Objeto de conjunto de filas de parámetro con valores de tabla  
 Puede crear un objeto de conjunto de filas especializado para parámetros con valores de tabla. Crear el objeto de conjunto de filas de parámetro con valores de tabla mediante ITableDefinitionWithConstraints::CreateTableWithConstraints o IOpenRowset:: OpenRowset. Para ello, establezca la *eKind* miembro de la *pTableID* parámetro en DBKIND_GUID_NAME y suministre CLSID_ROWSET_INMEMORY como el *guid* miembro. El nombre del tipo de servidor para el parámetro con valores de tabla debe especificarse en el *pwszName* miembro de *pTableID* al usar IOpenRowset:: OpenRowset. El objeto de conjunto de filas de parámetro con valores de tabla se comporta como un objeto normal de proveedor OLE DB de SQL Server Native Client.  
  
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
  
 DBTYPE_TABLE tiene el mismo formato que DBTYPE_IUNKNOWN. Es un puntero a un objeto del búfer de datos. Para una especificación completa en los enlaces, el consumidor rellena al búfer DBOBJECT, con *iid* establecido en una de las interfaces del objeto de conjunto de filas (IID_IRowset). Si no se especifica ningún DBOBJECT en los enlaces, se asumirá IID_IRowset.  
  
 No se admiten conversiones a DBTYPE_TABLE ni desde DBTYPE_TABLE para cualquier otro tipo. IConvertType::CanConvert devolverá S_FALSE si la conversión no admitida para cualquier solicitud que no sea de DBTYPE_TABLE a la conversión de DBTYPE_TABLE. Esto asume DBCONVERTFLAGS_PARAMETER en el objeto de comando.  
  
## <a name="methods"></a>Métodos  
 Para obtener información acerca de los métodos de OLE DB que admiten parámetros con valores de tabla, vea [OLE DB Table-Valued parámetro tipo admite &#40;métodos&#41;](ole-db-table-valued-parameter-type-support-methods.md).  
  
## <a name="properties"></a>Propiedades  
 Para obtener información sobre las propiedades de OLE DB que admiten parámetros con valores de tabla, vea [OLE DB Table-Valued parámetro tipo admite &#40;propiedades&#41;](ole-db-table-valued-parameter-type-support-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  