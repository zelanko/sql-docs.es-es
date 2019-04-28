---
title: Compatibilidad con columnas dispersas (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b286ba7bde145a9a3676f38f329a8efbd932a4cf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667652"
---
# <a name="sparse-columns-support-ole-db"></a>Compatibilidad con columnas dispersas (OLE DB)
  En este tema se proporciona información acerca de la compatibilidad con columnas dispersas OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para obtener más información sobre las columnas dispersas, vea [con las columnas dispersas en SQL Server Native Client](../features/sparse-columns-support-in-sql-server-native-client.md). Por ejemplo, consulte [Mostrar metadatos de columna y del catálogo para columnas dispersas &#40;OLE DB&#41;](../../native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>Metadatos de instrucción OLE DB  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], está disponible un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET. Este valor debería estar establecido para las columnas que son valores `column_set`. La marca DBCOLUMNFLAGS se puede recuperar mediante el *dwFlags* parámetro de IColumnsInfo:: GetColumnsInfo y la columna DBCOLUMN_FLAGS del conjunto de filas devuelto por IColumnsRowset:: GetColumnsRowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadatos de catálogo OLE DB  
 Se han agregado dos columnas adicionales específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a DBSCHEMA_COLUMNS.  
  
|Nombre de columna|Tipo de datos|Valor/comentarios|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Si la columna es una columna dispersa, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Si la columna es la columna `column_set` dispersa, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
  
 También se han agregado dos conjuntos de filas de esquema adicionales. Estos conjuntos de filas tienen la misma estructura que DBSCHEMA_COLUMNS pero devuelven contenido diferente. DBSCHEMA_COLUMNS_EXTENDED devuelve todas las columnas sin tener en cuenta la pertenencia a `column_set`. DBSCHEMA_SPARSE_COLUMN_SET únicamente devuelve columnas que son miembros de las columnas `column_set`dispersas.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamiento de OLE DB DataTypeCompatibility  
 El comportamiento con `DataTypeCompatibility=80` (en la cadena de conexión) es constante con un cliente de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], como sigue:  
  
-   Los nuevos conjuntos de filas de esquema no están visibles y no hay ninguna fila para ellos en el conjunto de filas de conjuntos de filas de esquema.  
  
-   Las columnas nuevas en el conjunto de filas COLUMNS no están visibles.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET no está establecido para las columnas `column_set`.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED está establecido para las columnas `column_set`.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Compatibilidad de OLE DB con columnas dispersas  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, se modificaron las siguientes interfaces OLE DB para admitir columnas dispersas:  
  
|Tipo o función de miembro|Descripción|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|DBCOLUMNFLAGS_SS_ISCOLUMNSET está establecido para el valor de marca de un nuevo DBCOLUMNFLAGS `column_set` columnas en *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE está establecido para las columnas `column_set`.|  
|IColumsRowset::GetColumnsRowset|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas `column_set` en DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE está establecido en DBCOMPUTEMODE_DYNAMIC para las columnas `column_set`.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS devuelve dos nuevas columnas: SS_IS_COLUMN_SET y SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS únicamente devuelve las columnas que no son miembros de `column_set`.<br /><br /> Se han agregado dos nuevos conjuntos de filas de esquema: DBSCHEMA_COLUMNS_EXTENDED devolverá todas las columnas independientemente de la dispersión de `column_set` pertenencia. DBSCHEMA_SPARSE_COLUMN_SET únicamente devuelve columnas que son miembros de `column_set`. Estos nuevos conjuntos de filas tienen las mismas columnas y restricciones que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas incluye los GUID para los nuevos conjuntos de filas DBSCHEMA_COLUMNS_EXTENDED y DBSCHEMA_SPARSE_COLUMN_SET en la lista de conjuntos de filas de esquema disponibles.|  
|ICommand::Execute|Si **seleccione \* desde** *tabla* es utilizada, devuelve todas las columnas que no son miembros de disperso `column_set`, más una columna XML que contiene los valores de todas las columnas no nulas que son los miembros de disperso `column_set`, si está presente.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OpenRowset devuelve un conjunto de filas con las mismas columnas que ICommand:: Execute, con un **seleccione \***  consulta en la misma tabla.|  
|ITableDefinition|No hay ningún cambio a esta interfaz para las columnas dispersas o para las columnas `column_set`. Las aplicaciones que tienen que realizar modificaciones de esquema deben ejecutar directamente el [!INCLUDE[tsql](../../../includes/tsql-md.md)] adecuado.|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)  
  
  
