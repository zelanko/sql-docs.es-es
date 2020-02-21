---
title: Compatibilidad con columnas dispersas (OLE DB) | Microsoft Docs
description: Compatibilidad con columnas dispersas (OLE DB)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 701b2d9e7a6d51b7fa13f797c6c5c9de75bed5d6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993862"
---
# <a name="sparse-columns-support-ole-db"></a>Compatibilidad con columnas dispersas (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este tema se proporciona información sobre la compatibilidad de OLE DB Driver for SQL Server con columnas dispersas. Para más información sobre las columnas dispersas, consulte [Compatibilidad con columnas dispersas en OLE DB Driver for SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md). Por ejemplo, consulte [Mostrar metadatos de columna y del catálogo para columnas dispersas &#40;OLE DB&#41;](../../oledb/ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
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
 Las siguientes interfaces de OLE DB se modificaron en OLE DB driver for SQL Server para admitir columnas dispersas:  
  
|Tipo o función de miembro|Descripción|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE está establecido para las columnas **column_set**.|  
|IColumsRowset::GetColumnsRowset|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE está establecido en DBCOMPUTEMODE_DYNAMIC para las columnas **column_set**.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS devuelve dos nuevas columnas: SS_IS_COLUMN_SET y SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS solo devuelve las columnas que no son miembros de **column_set**.<br /><br /> Se han agregado dos nuevos conjuntos de filas de esquema: DBSCHEMA_COLUMNS_EXTENDED devolvió todas las columnas con independencia del nivel de dispersión de la pertenencia a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET solo devuelve columnas que son miembros de **column_set**. Estos nuevos conjuntos de filas tienen las mismas columnas y restricciones que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas incluye los GUID para los nuevos conjuntos de filas DBSCHEMA_COLUMNS_EXTENDED y DBSCHEMA_SPARSE_COLUMN_SET en la lista de conjuntos de filas de esquema disponibles.|  
|ICommand::Execute|Si se usa **select \* from***table*, se devuelven todas las columnas que no son miembros de las columnas dispersas **column_set**, más una columna XML que contiene valores de todas las columnas distintas de NULL que son miembros de las columnas dispersas **column_set**, si existe.|  
|IOpenRowset::OpenRowset|IOpenRowset::OpenRowset devuelve un conjunto de filas con las mismas columnas que ICommand::Execute, con una consulta **select \*** en la misma tabla.|  
|ITableDefinition|No se ha realizado ningún cambio en esta interfaz para las columnas dispersas ni para las columnas **column_set**. Las aplicaciones que tienen que realizar modificaciones de esquema deben ejecutar directamente el [!INCLUDE[tsql](../../../includes/tsql-md.md)] adecuado.|  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
