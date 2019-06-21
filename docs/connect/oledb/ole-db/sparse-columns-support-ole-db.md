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
manager: jroth
ms.openlocfilehash: cec78daf72a65bfc0d3b496a42d1e726f84a1778
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795920"
---
# <a name="sparse-columns-support-ole-db"></a>Compatibilidad con columnas dispersas (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este tema proporciona información sobre el controlador OLE DB para SQL Server admiten columnas dispersas. Para obtener más información sobre las columnas dispersas, vea [con las columnas dispersas en el controlador OLE DB para SQL Server](../../oledb/features/sparse-columns-support-in-oledb-driver-for-sql-server.md). Por ejemplo, consulte [Mostrar metadatos de columna y del catálogo para columnas dispersas &#40;OLE DB&#41;](../../oledb/ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md).  
  
## <a name="ole-db-statement-metadata"></a>Metadatos de instrucción OLE DB  
 A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], está disponible un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET. Este valor tiene que establecerse para las columnas que son valores **column_set**. La marca DBCOLUMNFLAGS se puede recuperar mediante el *dwFlags* parámetro de IColumnsInfo:: GetColumnsInfo y la columna DBCOLUMN_FLAGS del conjunto de filas devuelto por IColumnsRowset:: GetColumnsRowset.  
  
## <a name="ole-db-catalog-metadata"></a>Metadatos de catálogo OLE DB  
 Se han agregado dos columnas adicionales específicas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a DBSCHEMA_COLUMNS.  
  
|Nombre de columna|Tipo de datos|Valor/comentarios|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|Si la columna es una columna dispersa, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|Si la columna es la columna dispersa **column_set**, esto tiene el valor VARIANT_TRUE; de lo contrario, VARIANT_FALSE.|  
  
 También se han agregado dos conjuntos de filas de esquema adicionales. Estos conjuntos de filas tienen la misma estructura que DBSCHEMA_COLUMNS pero devuelven contenido diferente. DBSCHEMA_COLUMNS_EXTENDED devuelve todas las columnas sin tener en cuenta la pertenencia a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET solo devuelve columnas que son miembros de columnas dispersas **column_set**.  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>Comportamiento de OLE DB DataTypeCompatibility  
 Comportamiento con **DataTypeCompatibility = 80** (en la cadena de conexión) es coherente con un [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] cliente, como se indica a continuación:  
  
-   Los nuevos conjuntos de filas de esquema no están visibles y no hay ninguna fila para ellos en el conjunto de filas de conjuntos de filas de esquema.  
  
-   Las columnas nuevas en el conjunto de filas COLUMNS no están visibles.  
  
-   DBCOLUMNFLAGS_SS_ISCOLUMNSET no está establecido para las columnas **column_set**.  
  
-   DBCOMPUTEMODE_NOTCOMPUTED está establecido para las columnas **column_set**.  
  
## <a name="ole-db-support-for-sparse-columns"></a>Compatibilidad de OLE DB con columnas dispersas  
 Se han modificado las siguientes interfaces OLE DB en el controlador OLE DB para SQL Server admitir columnas dispersas:  
  
|Tipo o función de miembro|Descripción|  
|-----------------------------|-----------------|  
|IColumnsInfo::GetColumnsInfo|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en *dwFlags*.<br /><br /> DBCOLUMNFLAGS_WRITE está establecido para las columnas **column_set**.|  
|IColumsRowset::GetColumnsRowset|Un nuevo valor de marca DBCOLUMNFLAGS, DBCOLUMNFLAGS_SS_ISCOLUMNSET, está establecido para las columnas **column_set** en DBCOLUMN_FLAGS.<br /><br /> DBCOLUMN_COMPUTEMODE está establecido en DBCOMPUTEMODE_DYNAMIC para las columnas **column_set**.|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS devuelve dos nuevas columnas: SS_IS_COLUMN_SET y SS_IS_SPARSE.<br /><br /> DBSCHEMA_COLUMNS solo devuelve las columnas que no son miembros de **column_set**.<br /><br /> Se han agregado dos nuevos conjuntos de filas de esquema: DBSCHEMA_COLUMNS_EXTENDED devolverá todas las columnas, independientemente de la dispersión de la pertenencia a **column_set**. DBSCHEMA_SPARSE_COLUMN_SET solo devuelve columnas que son miembros de **column_set**. Estos nuevos conjuntos de filas tienen las mismas columnas y restricciones que DBSCHEMA_COLUMNS.|  
|IDBSchemaRowset::GetSchemas|IDBSchemaRowset::GetSchemas incluye los GUID para los nuevos conjuntos de filas DBSCHEMA_COLUMNS_EXTENDED y DBSCHEMA_SPARSE_COLUMN_SET en la lista de conjuntos de filas de esquema disponibles.|  
|ICommand::Execute|Si se usa **select \* from** *table*, devuelve todas las columnas que no son miembros de las **column_set** dispersas, más una columna XML que contiene valores de todas las columnas distintas de NULL que son miembros de las columnas dispersas **column_set**, si existe.|  
|IOpenRowset::OpenRowset|IOpenRowset:: OpenRowset devuelve un conjunto de filas con las mismas columnas que ICommand:: Execute, con un **seleccione \***  consulta en la misma tabla.|  
|ITableDefinition|No se ha realizado ningún cambio en esta interfaz para las columnas dispersas ni para las columnas **column_set**. Las aplicaciones que tienen que realizar modificaciones de esquema deben ejecutar directamente el [!INCLUDE[tsql](../../../includes/tsql-md.md)] adecuado.|  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
