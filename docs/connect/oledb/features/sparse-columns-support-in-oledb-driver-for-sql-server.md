---
title: Compatibilidad de columnas dispersas con el controlador OLE DB para SQL Server | Microsoft Docs
description: Obtenga información sobre cómo OLE DB Driver for SQL Server admite columnas dispersas y consulte información al respecto en SQL Server.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1397d69f72cfc1362decf84959046d581befea5b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862280"
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad de columnas dispersas con el controlador OLE DB para SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server admite las columnas dispersas. Para más información sobre columnas dispersas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Usar columnas dispersas](../../../relational-databases/tables/use-sparse-columns.md) y [Usar conjuntos de columnas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para más información sobre las columnas dispersas en OLE DB Driver for SQL Server, consulte [Compatibilidad con las columnas dispersas &#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>Escenarios de usuarios de columnas dispersas y OLE DB Driver for SQL Server  
 En la tabla siguiente se resumen los escenarios comunes de usuario para los usuarios de OLE DB Driver for SQL Server con columnas dispersas:  
  
|Escenario|Comportamiento|  
|--------------|--------------|  
|**select \* from table** o IOpenRowset::OpenRowset.|Devuelve todas las columnas que no son miembros del **column_set** disperso, más una columna XML que contiene los valores de todas las columnas no nulas que son miembros del **column_set** disperso.|  
|Hacer referencia a una columna por nombre.|Se puede hacer referencia a la columna independientemente de su estado de columna dispersa o la pertenencia al **column_set**.|  
|Obtener acceso a las columnas miembro del **column_set** a través de una columna XML calculada.|Se puede acceder a las columnas que son miembros del **column_set** disperso al seleccionar el **column_set** por nombre y se puede hacer que se inserten y actualicen los valores al actualizar el XML de la columna **column_set**.<br /><br /> El valor debe cumplir el esquema de las columnas **column_set**.|  
|Recuperar los metadatos de todas las columnas de una tabla mediante el conjunto de filas de esquema DBSCHEMA_COLUMNS sin restricción de columnas (OLE DB).|Devuelve una fila para todas las columnas que no son miembros del **column_set**. Si la tabla tiene un **column_set** disperso, se devolverá una fila.<br /><br /> Observe que esto no devuelve los metadatos de las columnas que son miembros del **column_set**.|  
|Recuperar los metadatos de todas las columnas, independientemente de la dispersión o pertenencia en un **column_set**. Esto podría devolver un número muy grande de filas.|Llame a IDBSchemaRowset::GetRowset para el conjunto de filas de esquema DBSCHEMA_COLUMNS_EXTENDED.|  
|Recuperar únicamente los metadatos de las columnas que son miembros del **column_set**. Esto podría devolver un número muy grande de filas.|Llame a IDBSchemaRowset::GetRowset para el conjunto de filas de esquema DBSCHEMA_SPARSE_COLUMN_SET.|  
|Determinar si una columna es dispersa.|Consulte la columna SS_IS_SPARSE del conjunto de filas de esquema DBSCHEMA_COLUMNS (OLE DB).|  
|Determine si una columna es **column_set**.|Consulte la columna SS_IS_COLUMN_SET del conjunto de filas de esquema DBSCHEMA_COLUMNS. O bien, consulte *dwFlags* devuelto por IColumnsinfo::GetColumnInfo o DBCOLUMNFLAGS en el conjunto de filas devuelto por IColumnsRowset::GetColumnsRowset. Para las columnas **column_set**, se establecerá DBCOLUMNFLAGS_SS_ISCOLUMNSET.|  
|Importar y exportar columnas dispersas en BCP de una tabla sin **column_set**.|Ningún cambio en el comportamiento desde las versiones anteriores de OLE DB Driver for SQL Server.|  
|Importar y exportar columnas dispersas en BCP de una tabla con **column_set**.|**column_set** se importa y se exporta de la misma forma que una columna XML; es decir, como **varbinary(max)** si se enlaza como un tipo binario, o como **nvarchar(max)** si se enlaza como un tipo **char** o **wchar**.<br /><br /> Las columnas que son miembro del **column_set** disperso no se exportan como columnas distintas; se exportan solo en el valor del **column_set**.|  
|Comportamiento de **queryout** para BCP.|Ningún cambio en el tratamiento de columnas nombradas explícitamente desde las versiones anteriores de OLE DB Driver for SQL Server.<br /><br /> Los escenarios que implican la importación y exportación entre tablas con esquemas diferentes pueden requerir un tratamiento especial.<br /><br /> Para obtener más información acerca de BCP, vea Compatibilidad de la copia masiva (BCP) con columnas dispersas, más adelante en este tema.|  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Los clientes de nivel inferior solo devolverán los metadatos de las columnas que no son miembro del **column_set** disperso para SQLColumns y DBSCHMA_COLUMNS.
  
 Los clientes de nivel inferior pueden acceder a las columnas que son miembros del **column_set** disperso por nombre, y la columna del **column_set** será accesible como una columna XML para los clientes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Compatibilidad de la copia masiva (BCP) con columnas dispersas  
 No hay ningún cambio en la API BCP en OLE DB para las columnas dispersas o características del **column_set**.  
  
 Si una tabla tiene un **column_set**, las columnas dispersas no se tratan como columnas distintas. Los valores de todas las columnas dispersas están incluidos en el valor de **column_set**, que se exporta de la misma manera que una columna XML; es decir, como **varbinary(max)** si se enlaza como un tipo binario, o como **nvarchar(max)** si se enlaza como un tipo **char** o **wchar**. En la importación, el valor de **column_set** debe cumplir el esquema de **column_set**.  
  
 Para las operaciones **queryout**, no hay ningún cambio en la manera en que se tratan las columnas a las que se hace referencia. Las columnas **column_set** tienen el mismo comportamiento que las columnas XML y la dispersión no tiene ningún efecto en el tratamiento de las columnas dispersas indicadas.  
  
 En cambio, si se usa **queryout** para la exportación y hace referencia a las columnas dispersas que son miembros de la columna dispersa establecida por nombre, no puede realizar una importación directa en una tabla con estructura similar. Esto se debe a que BCP usa los metadatos de forma coherente con una operación **select \*** para la importación y no puede ajustar las columnas miembro del **column_set** a estos metadatos. Para importar individualmente las columnas miembro del **column_set**, debe definir una vista en la tabla que haga referencia a las columnas **column_set** deseadas y debe realizar la operación de importación mediante la vista.  
  
## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)  
  
  
