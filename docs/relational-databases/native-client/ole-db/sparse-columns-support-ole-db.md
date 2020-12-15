---
description: Compatibilidad con columnas dispersas en SQL Server Native Client (OLE DB)
title: Compatibilidad con columnas dispersas (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c1acd979138ec96ded25ecbead978b7ff18c9d30
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467566"
---
# <a name="sparse-columns-support-in-sql-server-native-client-ole-db"></a>Compatibilidad con columnas dispersas en SQL Server Native Client (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En este tema se proporciona información acerca de la compatibilidad con columnas dispersas OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para obtener más información sobre las columnas dispersas, consulte [compatibilidad con columnas dispersas en SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md). Por ejemplo, consulte [Mostrar metadatos de columna y del catálogo para columnas dispersas &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>Metadatos de instrucción OLE DB  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], está disponible un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET. Este valor tiene que establecerse para las columnas que son valores **column_set**. La marca DBCOLUMNFLAGS se puede recuperar mediante el parámetro *dwFlags* de IColumnsInfo::GetColumnsInfo y la columna DBCOLUMN_FLAGS del conjunto de filas devuelto por IColumnsRowset::GetColumnsRowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadatos de catálogo OLE DB  
 Se han agregado dos columnas adicionales específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a DBSCHEMA_COLUMNS.  
  
|Nombre de la columna|Tipo de datos|Valor/comentarios|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Si la columna es una columna dispersa, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Si la columna es la columna dispersa **column_set**, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
  
 También se han agregado dos conjuntos de filas de esquema adicionales. Estos conjuntos de filas tienen la misma estructura que DBSCHEMA_COLUMNS pero devuelven contenido diferente. DBSCHEMA_COLUMNS_EXTENDED devuelve todas las columnas sin tener en cuenta la pertenencia a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET solo devuelve columnas que son miembros de columnas dispersas **column_set**.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamiento de OLE DB DataTypeCompatibility  
 El comportamiento con **DataTypeCompatibility=80** (en la cadena de conexión) es coherente con un cliente de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)], de la manera siguiente:  
  
-   Los nuevos conjuntos de filas de esquema no están visibles y no hay ninguna fila para ellos en el conjunto de filas de conjuntos de filas de esquema.  
  
-   Las columnas nuevas en el conjunto de filas COLUMNS no están visibles.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET no está establecido para las columnas **column_set**.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED está establecido para las columnas **column_set**.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Compatibilidad de OLE DB con columnas dispersas  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, se modificaron las siguientes interfaces OLE DB para admitir columnas dispersas:  
  
|Tipo o función de miembro|Descripción|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE está establecido para las columnas **column_set**.|  
|IColumsRowset::GetColumnsRowset|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE está establecido en DBCOMPUTEMODE_DYNAMIC para las columnas **column_set**.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS devuelve dos nuevas columnas: SS_IS_COLUMN_SET y SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS solo devuelve las columnas que no son miembros de **column_set**.<br /><br /> Se han agregado dos nuevos conjuntos de filas de esquema: DBSCHEMA_COLUMNS_EXTENDED devolverá todas las columnas, independientemente de la dispersión de la pertenencia a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET solo devuelve columnas que son miembros de **column_set**. Estos nuevos conjuntos de filas tienen las mismas columnas y restricciones que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas incluye los GUID para los nuevos conjuntos de filas DBSCHEMA_COLUMNS_EXTENDED y DBSCHEMA_SPARSE_COLUMN_SET en la lista de conjuntos de filas de esquema disponibles.|  
|ICommand::Execute|Si se usa **select \* from***table*, se devuelven todas las columnas que no son miembros de las columnas dispersas **column_set**, más una columna XML que contiene valores de todas las columnas distintas de NULL que son miembros de las columnas dispersas **column_set**, si existe.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OpenRowset devuelve un conjunto de filas con las mismas columnas que ICommand:: Execute, con una consulta **SELECT \** _ en la misma tabla.|  
|ITableDefinition|No hay ningún cambio en esta interfaz para las columnas dispersas o para las columnas _ *COLUMN_SET**. Las aplicaciones que tienen que realizar modificaciones de esquema deben ejecutar directamente el [!INCLUDE[tsql](../../../includes/tsql-md.md)] adecuado.|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
