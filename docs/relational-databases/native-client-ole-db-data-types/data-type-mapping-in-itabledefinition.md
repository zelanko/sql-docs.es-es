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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bdf3a1e716fd1de5354b735e353916bab863059c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73774308"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Asignación de tipos de datos en ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Al crear tablas mediante la función **ITableDefinition:: CreateTable** , el consumidor del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB puede especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos en el miembro *pwszTypeName* de la matriz DBCOLUMNDESC que se pasa. Si el consumidor especifica el tipo de datos de una columna por nombre, se omite la asignación del tipo de datos de OLE DB, representada por el miembro *wType* de la estructura DBCOLUMNDESC.  
  
 Al especificar los nuevos tipos de datos de columna con OLE DB tipos de datos que usan el miembro *wType* de la estructura DBCOLUMNDESC, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna los tipos de datos OLE DB como se indica a continuación.  
  
|Tipo de datos de OLE DB|SQL Server<br /><br /> tipo de datos|Información adicional|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** o **varbinary(max)**|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Según el valor y la versión de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **Image**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos **binarios** , el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **binario**. Si el valor de la propiedad es VARIANT_FALSE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **varbinary**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna SQL Server creada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_NUMERIC|**numeric**|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client inspecciona los miembros miembros *bPrecision* y *bScale* para determinar la precisión y la escala de la columna **numérica** .|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** o **varchar(max)**|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. En función del valor y la versión de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **texto**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres multibyte, el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **Char**. Si el valor de la propiedad es VARIANT_FALSE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **VARCHAR**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_UDT|**UDT**|Cuando se requieren columnas UDT, **ITableDefinition::CreateTable** usa la información que se muestra a continuación en estructuras **DBCOLUMNDESC**:<br /><br /> *pwSzTypeName* se omite.<br /><br /> *rgPropertySets* debe incluir un conjunto de propiedades **DBPROPSET_SQLSERVERCOLUMN** como se describe en la sección sobre **DBPROPSET_SQLSERVERCOLUMN**, en el [uso de tipos definidos por el usuario](../../relational-databases/native-client/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** o **nvarchar(max)**|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Según el valor, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **ntext**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres Unicode, el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB Native Client inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **nchar**. Si el valor de la propiedad es VARIANT_FALSE, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client asigna el tipo a **nvarchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_XML|**XML**||  
  
> [!NOTE]  
>  Cuando se crea una nueva tabla, el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client solamente asigna los valores de enumeración del tipo de datos de OLE DB especificado en la tabla anterior. Al intentar crear una tabla con una columna de cualquier otro tipo de datos de OLE DB, se genera un error.  
  
## <a name="see-also"></a>Vea también  
 [Tipos &#40;de datos OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
