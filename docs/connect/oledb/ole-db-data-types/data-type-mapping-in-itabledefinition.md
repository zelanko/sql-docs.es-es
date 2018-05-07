---
title: Asignación de tipo de datos en ITableDefinition | Documentos de Microsoft
description: Asignación de tipo de datos en ITableDefinition
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ade365add5b89069e86f67d82dfa84638bcb71f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-mapping-in-itabledefinition"></a>Asignación de tipos de datos en ITableDefinition
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cuando se crean tablas utilizando la **ITableDefinition:: CreateTable** función, puede especificar el controlador OLE DB para el consumidor de SQL Server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos de la *pwszTypeName* miembro de la Matriz DBCOLUMNDESC que se pasa. Si el consumidor especifica el tipo de datos de una columna por su nombre, los datos de OLE DB escriba asignación, representada por la *wType* miembro de la estructura DBCOLUMNDESC, se omite.  
  
 Al especificar los nuevos tipos de datos de columna con tipos de datos de OLE DB mediante la estructura DBCOLUMNDESC *wType* miembro, el controlador OLE DB para SQL Server asigna los tipos de datos OLE DB como se indica a continuación.  
  
|Tipo de datos de OLE DB|SQL Server<br /><br /> tipo de datos|Información adicional|  
|----------------------|------------------------------|----------------------------|  
|DBTYPE_BOOL|**bit**||  
|DBTYPE_BYTES|**binario**, **varbinary**, **imagen,** o **varbinary (max)**|El controlador OLE DB para SQL Server inspecciona la *ulColumnSize* miembro de la estructura DBCOLUMNDESC. Según el valor y la versión de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia, el controlador OLE DB para SQL Server asigna el tipo a **imagen**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de un **binario** columna, tipo de datos, a continuación, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets*miembro. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el controlador OLE DB para SQL Server asigna el tipo a **binario**. Si el valor de la propiedad es VARIANT_FALSE, el controlador OLE DB para SQL Server asigna el tipo a **varbinary**. En cualquier caso, el miembro *ulColumnSize* miembro determina el ancho de la columna de SQL Server creada.|  
|DBTYPE_CY|**money**||  
|DBTYPE_DBTIMESTAMP|**datetime2**||  
|DBTYPE_GUID|**uniqueidentifier**||  
|DBTYPE_I2|**smallint**||  
|DBTYPE_I4|**int**||  
|DBTYPE_I8|**bigint**||
|DBTYPE_NUMERIC|**numeric**|El controlador OLE DB para SQL Server inspecciona los miembros *bPrecision* y *bScale* miembros para determinar la precisión y escala para la **numérico** columna.|  
|DBTYPE_R4|**real**||  
|DBTYPE_R8|**float**||  
|DBTYPE_STR|**char**, **varchar**, **texto,** o **varchar (max)**|El controlador OLE DB para SQL Server inspecciona la *ulColumnSize* miembro de la estructura DBCOLUMNDESC. Según el valor y la versión de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia, el controlador OLE DB para SQL Server asigna el tipo a **texto**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres multibyte y, a continuación, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets* miembro. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el controlador OLE DB para SQL Server asigna el tipo a **char**. Si el valor de la propiedad es VARIANT_FALSE, el controlador OLE DB para SQL Server asigna el tipo a **varchar**. En cualquier caso, el miembro *ulColumnSize* miembro determina el ancho de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] columna creada.|  
|DBTYPE_UDT|**UDT**|La siguiente información se usa en **DBCOLUMNDESC** estructuras **ITableDefinition:: CreateTable** cuando se requieren columnas UDT:<br /><br /> *pwSzTypeName* se omite.<br /><br /> *rgPropertySets* debe incluir un **DBPROPSET_SQLSERVERCOLUMN** propiedad establecida tal y como se describe en la sección sobre **DBPROPSET_SQLSERVERCOLUMN**, en [Defined Types ](../../oledb/features/using-user-defined-types.md).|  
|DBTYPE_UI1|**tinyint**||  
|DBTYPE_VARIANT|**sql_variant**||
|DBTYPE_WSTR|**nchar**, **nvarchar**, **ntext,** o **nvarchar (max)**|El controlador OLE DB para SQL Server inspecciona la *ulColumnSize* miembro de la estructura DBCOLUMNDESC. En función del valor, el controlador OLE DB para SQL Server asigna el tipo a **ntext**.<br /><br /> Si el valor de *ulColumnSize* es menor que la longitud máxima de una columna de tipo de datos de caracteres Unicode y, a continuación, el controlador OLE DB para SQL Server inspecciona el miembro *rgPropertySets* miembro. Si DBPROP_COL_FIXEDLENGTH es VARIANT_TRUE, el controlador OLE DB para SQL Server asigna el tipo a **nchar**. Si el valor de la propiedad es VARIANT_FALSE, el controlador OLE DB para SQL Server asigna el tipo a **nvarchar**. En cualquier caso, el miembro *ulColumnSize* miembro determina el ancho de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] columna creada.|  
|DBTYPE_XML|**XML**||  

> [!NOTE]  
>  Al crear una nueva tabla, el controlador OLE DB para SQL Server asigna solo los valores OLE DB datos tipo enumeración especificados en la tabla anterior. Al intentar crear una tabla con una columna de cualquier otro tipo de datos de OLE DB, se genera un error.  

## <a name="see-also"></a>Vea también  
 [Tipos de datos & #40; OLE DB & #41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
