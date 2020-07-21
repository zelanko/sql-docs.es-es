---
title: Asignación de tipos de datos en ITableDefinition | Microsoft Docs
description: Asignación de tipos de datos en ITableDefinition
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- OLE DB Driver for SQL Server, data types
- ITableDefinition interface
- DBCOLUMNDESC structure
- data types [OLE DB]
- CreateTable function
- OLE DB, data types
author: pmasl
ms.author: pelopes
ms.openlocfilehash: abe874a50e8534291a67393dfaf3485c96405b02
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015851"
---
# <a name="data-type-mapping-in-itabledefinition"></a>Asignación de tipos de datos en ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cuando se crean tablas mediante la función **ITableDefinition::CreateTable**, el consumidor del controlador OLE DB para SQL Server puede especificar tipos de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el miembro *pwszTypeName* de la matriz DBCOLUMNDESC que se pasa. Si el consumidor especifica el tipo de datos de una columna por nombre, se omite la asignación del tipo de datos de OLE DB, representada por el miembro *wType* de la estructura DBCOLUMNDESC.  
  
 Cuando se especifican nuevos tipos de datos de columna con tipos de datos de OLE DB mediante el miembro *wType* de la estructura DBCOLUMNDESC, el controlador OLE DB para SQL Server asigna los tipos de datos de OLE DB tal y como se indica a continuación.  
  
|Tipo de datos de OLE DB|SQL Server<br /><br /> tipo de datos|Información adicional|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binary**, **varbinary**, **image** o **varbinary(max)**|OLE DB Driver for SQL Server inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Basándose en el valor y la versión de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], OLE DB Driver for SQL Server asigna el tipo a **image**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos **binary**, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, OLE DB Driver for SQL Server asigna el tipo a **binary**. Si el valor de la propiedad es VARIANT_FALSE, OLE DB Driver for SQL Server asigna el tipo a **varbinary**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna SQL Server creada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|El controlador OLE DB para SQL Server inspecciona los miembros *bPrecision* y *bScale* de DBCOLUMDESC para determinar la precisión y la escala de la columna **numeric**.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **text** o **varchar(max)**|OLE DB Driver for SQL Server inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Basándose en el valor y la versión de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], OLE DB Driver for SQL Server asigna el tipo a **text**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres multibyte, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, OLE DB Driver for SQL Server asigna el tipo a **char**. Si el valor de la propiedad es VARIANT_FALSE, OLE DB Driver for SQL Server asigna el tipo a **varchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_UDT|**UDT**|Cuando se requieren columnas UDT, **ITableDefinition::CreateTable** usa la información que se muestra a continuación en estructuras **DBCOLUMNDESC**:<br /><br /> Se omite *pwSzTypeName*.<br /><br /> *rgPropertySets* debe incluir un conjunto de propiedades **DBPROPSET_SQLSERVERCOLUMN** como se describe en la sección de **DBPROPSET_SQLSERVERCOLUMN**, en [Usar tipos definidos por el usuario](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext** o **nvarchar(max)**|OLE DB Driver for SQL Server inspecciona el miembro *ulColumnSize* de la estructura DBCOLUMNDESC. Basándose en el valor, OLE DB Driver for SQL Server asigna el tipo a **ntext**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres Unicode, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets* de DBCOLUMNDESC. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, OLE DB Driver for SQL Server asigna el tipo a **nchar**. Si el valor de la propiedad es VARIANT_FALSE, OLE DB Driver for SQL Server asigna el tipo a **nvarchar**. En cualquier caso, el miembro *ulColumnSize* de DBCOLUMNDESC determina el ancho de la columna [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] creada.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  Cuando se crea una tabla, el controlador OLE DB para SQL Server solo asigna los valores de enumeración del tipo de datos de OLE DB especificado en la tabla anterior. Al intentar crear una tabla con una columna de cualquier otro tipo de datos de OLE DB, se genera un error.  

## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
