---
title: Asignación de tipos de datos en ITableDefinition | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
ms.assetid: 13292d1f-c17e-4d11-bf98-3460a10cbb18
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3e828efa513db1ace272e59379f77d063220290
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297089"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Asignación de tipos de datos en ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al crear tablas mediante la función **ITableDefinition::CreateTable,** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client puede especificar tipos de datos en el miembro *pwszTypeName* de la matriz DBCOLUMNDESC que se pasa. Si el consumidor especifica el tipo de datos de una columna por nombre, se omite la asignación del tipo de datos de OLE DB, representada por el miembro *wType* de la estructura DBCOLUMNDESC.  
  
 Al especificar nuevos tipos de datos de columna con tipos de datos OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DB mediante el miembro *wType* de la estructura DBCOLUMNDESC, el proveedor OLE DB de Native Client asigna los tipos de datos OLE DB de la siguiente manera.  
  
|Tipo de datos de OLE DB|SQL Server<br /><br /> tipo de datos|Información adicional|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** o **varbinary(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. En función del valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión de la instancia, el proveedor OLE DB de Native Client asigna el tipo a **image**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] máxima de una columna de tipo de datos **binarios,** el proveedor OLE DB de Native Client inspecciona el miembro DBCOLUMNDESC *rgPropertySets.* Si se VARIANT_TRUE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_FIXEDLENGTH, el proveedor OLE DB de Native Client asigna el tipo a **binario.** Si el valor de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad se VARIANT_FALSE, el proveedor OLE DB de Native Client asigna el tipo a **varbinary**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna SQL Server creada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**UNIQUEIDENTIFIER**||  
|DBTYPE_I2|**SMALLINT**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**Numérico**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client inspecciona los miembros DBCOLUMDESC *bPrecision* y *bScale* para determinar la precisión y la escala de la columna **numérica.**|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**Flotador**||  
|DBTYPE_STR|**char**, **varchar**, **text** o **varchar(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. En función del valor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la versión de la instancia, el proveedor OLE DB de Native Client asigna el tipo al **texto.**<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una columna de tipo de datos de caracteres multibyte, el proveedor OLE DB de Native Client inspecciona el miembro DBCOLUMNDESC *rgPropertySets.* Si DBPROP_COL_FIXEDLENGTH es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, el proveedor OLE DB de Native Client asigna el tipo a **char**. Si el valor de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad se VARIANT_FALSE, el proveedor OLE DB de Native Client asigna el tipo a **varchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_UDT|**UDT**|Cuando se requieren columnas UDT, **ITableDefinition::CreateTable** usa la información que se muestra a continuación en estructuras **DBCOLUMNDESC**:<br /><br /> Se omite *pwSzTypeName*.<br /><br /> *rgPropertySets* debe incluir un conjunto de propiedades **DBPROPSET_SQLSERVERCOLUMN** como se describe en la sección de **DBPROPSET_SQLSERVERCOLUMN**, en [Usar tipos definidos por el usuario](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**TINYINT**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** o **nvarchar(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. En función del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valor, el proveedor OLE DB de Native Client asigna el tipo a **ntext**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una columna de tipo de datos de caracteres Unicode, el proveedor OLE DB de Native Client inspecciona el miembro DBCOLUMNDESC *rgPropertySets.* Si se DBPROP_COL_FIXEDLENGTH [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VARIANT_TRUE, el proveedor OLE DB de Native Client asigna el tipo a **nchar**. Si el valor de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] propiedad es VARIANT_FALSE, el proveedor OLE DB de Native Client asigna el tipo a **nvarchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Cuando se crea una nueva tabla, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente asigna los valores de enumeración del tipo de datos de OLE DB especificado en la tabla anterior. Al intentar crear una tabla con una columna de cualquier otro tipo de datos de OLE DB, se genera un error.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
