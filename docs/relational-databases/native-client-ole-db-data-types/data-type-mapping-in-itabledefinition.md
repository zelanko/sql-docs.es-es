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
ms.openlocfilehash: 9ee1ea1327f2dd52a7496486f0d33b5d5d91e86d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005474"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Asignación de tipos de datos en ITableDefinition
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Al crear tablas mediante la función **ITableDefinition:: CreateTable** , el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client puede especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos en el miembro *pwszTypeName* de la matriz DBCOLUMNDESC que se pasa. Si el consumidor especifica el tipo de datos de una columna por nombre, se omite la asignación del tipo de datos de OLE DB, representada por el miembro *wType* de la estructura DBCOLUMNDESC.  
  
 Al especificar los nuevos tipos de datos de columna con OLE DB tipos de datos que usan el miembro *wType* de la estructura DBCOLUMNDESC, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna OLE DB tipos de datos de la siguiente manera.  
  
|Tipo de datos de OLE DB|SQL Server<br /><br /> tipo de datos|Información adicional|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** o **varbinary(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Basándose en el valor y la versión de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **Image**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos **binarios** , el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **binario**. Si el valor de la propiedad es VARIANT_FALSE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **varbinary**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna SQL Server creada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona los miembros miembros *BPrecision* y *bScale* para determinar la precisión y la escala de la columna **numérica** .|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** o **varchar(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. En función del valor y la versión de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **texto**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres multibyte, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **Char**. Si el valor de la propiedad es VARIANT_FALSE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **VARCHAR**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_UDT|**DEFINIDO**|Cuando se requieren columnas UDT, **ITableDefinition::CreateTable** usa la información que se muestra a continuación en estructuras **DBCOLUMNDESC**:<br /><br /> Se omite *pwSzTypeName*.<br /><br /> *rgPropertySets* debe incluir un conjunto de propiedades **DBPROPSET_SQLSERVERCOLUMN** como se describe en la sección de **DBPROPSET_SQLSERVERCOLUMN**, en [Usar tipos definidos por el usuario](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** o **nvarchar(max)**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Según el valor, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **ntext**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres Unicode, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **nchar**. Si el valor de la propiedad es VARIANT_FALSE, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client asigna el tipo a **nvarchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Cuando se crea una nueva tabla, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente asigna los valores de enumeración del tipo de datos de OLE DB especificado en la tabla anterior. Al intentar crear una tabla con una columna de cualquier otro tipo de datos de OLE DB, se genera un error.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
