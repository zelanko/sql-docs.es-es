---
title: Asignación de tipos de datos en conjuntos de filas y parámetros | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- DBTYPE_SQLVARIANT data type
- SQL Server Native Client OLE DB provider, data types
- rowsets [OLE DB], data type mapping
- data types [OLE DB]
- GetColumnInfo function
- parameters [OLE DB]
- SSPROP_ALLOWNATIVEVARIANT property
- GetParameterInfo function
- OLE DB, data types
ms.assetid: 3d831ff8-3b79-4698-b2c1-2b5dd2f8235c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0979892b6770b9a9c2d0d9c4e8a0d734d873c085
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63062204"
---
# <a name="data-type-mapping-in-rowsets-and-parameters"></a>Asignar tipos de datos en conjuntos de filas y parámetros
  En conjuntos de filas y como valores de parámetro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el proveedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Native Client representa los datos utilizando los siguientes tipos de datos definidos por el OLE DB, que se muestran en las funciones **IColumnsInfo:: GetColumnInfo** y **ICommandWithParameters:: GetParameterInfo**.  
  
|Tipos de datos de SQL Server|Tipo de datos de OLE DB|  
|--------------------------|----------------------|  
|**BIGINT**|DBTYPE_I8|  
|**binary**|DBTYPE_BYTES|  
|**bit**|DBTYPE_BOOL|  
|**char**|DBTYPE_STR|  
|**datetime**|DBTYPE_DBTIMESTAMP|  
|**datetime2**|DBTYPE_DBTIME2|  
|**Decimal**|DBTYPE_NUMERIC|  
|**float**|DBTYPE_R8|  
|**impresión**|DBTYPE_BYTES|  
|**int**|DBTYPE_I4|  
|**money**|DBTYPE_CY|  
|**nchar**|DBTYPE_WSTR|  
|**ntext**|DBTYPE_WSTR|  
|**alfanumérico**|DBTYPE_NUMERIC|  
|**nvarchar**|DBTYPE_WSTR|  
|**impuestos**|DBTYPE_R4|  
|**smalldatetime**|DBTYPE_DBTIMESTAMP|  
|**smallint**|DBTYPE_I2|  
|**SMALLMONEY**|DBTYPE_CY|  
|**sql_variant**|DBTYPE_VARIANT, DBTYPE_SQLVARIANT|  
|**sysname**|DBTYPE_WSTR|  
|**negrita**|DBTYPE_STR|  
|**timestamp**|DBTYPE_BYTES|  
|**tinyint**|DBTYPE_UI1|  
|**UDT**|DBTYPE_UDT|  
|**uniqueidentifier**|DBTYPE_GUID|  
|**varbinary**|DBTYPE_BYTES|  
|**varchar**|DBTYPE_STR|  
|**XML**|DBTYPE_XML|  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite conversiones de datos solicitadas por el consumidor, tal como se muestra en la ilustración.  
  
 Los objetos **sql_variant** pueden contener datos de cualquier tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] excepto text, ntext, image, varchar(max), nvarchar(max), varbinary(max), xml, timestamp y los tipos definidos por el usuario de Common Language Runtime (CLR) de Microsoft .NET Framework. Una instancia de datos sql_variant no puede tener sql_variant como tipo de datos base subyacente. Por ejemplo, la columna puede contener valores **smallint** en algunas filas, valores **float** en otras filas y valores **char**/**nchar** en el resto.  
  
> [!NOTE]  
>  El tipo de datos **sql_variant** es similar al tipo de datos Variant de Microsoft Visual Basic? y el DBTYPE_VARIANT, DBTYPE_SQLVARIANT en OLEDB.  
  
 Cuando los datos **sql_variant** se capturan como DBTYPE_VARIANT, se incluyen en una estructura VARIANT en el búfer. Pero es posible que los subtipos de la estructura VARIANT no se asignen a los subtipos definidos en el tipo de datos **sql_variant**. Los datos **sql_variant** se tienen que capturar en este caso como DBTYPE_SQLVARIANT para que todos los subtipos coincidan.  
  
## <a name="dbtype_sqlvariant-data-type"></a>Tipo de datos DBTYPE_SQLVARIANT  
 Para admitir el tipo de datos **sql_variant** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el proveedor de OLE DB de Native Client expone un tipo de datos específico del proveedor denominado DBTYPE_SQLVARIANT. Cuando los datos **sql_variant** se capturan como DBTYPE_SQLVARIANT, se almacenan en una estructura SSVARIANT específica del proveedor. La estructura SSVARIANT contiene todos los subtipos que coinciden con los subtipos del tipo de datos **sql_variant**.  
  
 La propiedad SSPROP_ALLOWNATIVEVARIANT de la sesión también debe estar establecida en TRUE.  
  
## <a name="provider-specific-property-ssprop_allownativevariant"></a>Propiedad SSPROP_ALLOWNATIVEVARIANT específica del proveedor  
 Al capturar los datos, puede especificar explícitamente qué clase de tipo de datos se debería devolver para una columna o para un parámetro. **IColumnsInfo** también se puede utilizar para obtener la información de columna y usarla para realizar el enlace. Cuando se usa **IColumnsInfo** para obtener información de columna con fines de enlace, si la propiedad SSPROP_ALLOWNATIVEVARIANT de sesión es FALSE (valor predeterminado), en las columnas **sql_variant** se devuelve DBTYPE_VARIANT. Si la propiedad SSPROP_ALLOWNATIVEVARIANT es FALSE, no se admite DBTYPE_SQLVARIANT. Si la propiedad SSPROP_ALLOWNATIVEVARIANT está establecida en TRUE, el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT. Al capturar datos **sql_variant** como DBTYPE_SQLVARIANT, la propiedad SSPROP_ALLOWNATIVEVARIANT de sesión tiene que establecerse en TRUE.  
  
 La propiedad SSPROP_ALLOWNATIVEVARIANT forma parte del conjunto de propiedades DBPROPSET_SQLSERVERSESSION específico del proveedor y es una propiedad de sesión.  
  
 DBTYPE_VARIANT se aplica a todos los demás proveedores OLE DB.  
  
## <a name="ssprop_allownativevariant"></a>SSPROP_ALLOWNATIVEVARIANT  
 SSPROP_ALLOWNATIVEVARIANT es una propiedad de sesión y forma parte del conjunto de propiedades DBPROPSET_SQLSERVERSESSION.  
  
|||  
|-|-|  
|SSPROP_ALLOWNATIVEVARIANT|Tipo: VT_BOOL<br /><br /> L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
