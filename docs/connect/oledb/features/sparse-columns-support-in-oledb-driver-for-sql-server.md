---
title: Compatibilidad con columnas dispersas en el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Compatibilidad con columnas dispersas en el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 08de456a687ffdde2889cb3bd26bd5dbfa39a5dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad con columnas dispersas en el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Controlador de OLE DB para SQL Server admite columnas dispersas. Para obtener más información sobre las columnas dispersas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [usar columnas dispersas](../../../relational-databases/tables/use-sparse-columns.md) y [usar conjuntos de columnas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para obtener más información sobre la compatibilidad con columnas dispersas en controlador OLE DB de SQL Server, [columnas dispersas son compatibles con &#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obtener información acerca de las aplicaciones de ejemplo que muestran esta característica, consulte [ejemplos de programación de datos de SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>Escenarios de usuario para las columnas dispersas y controlador OLE DB para SQL Server  
 La siguiente tabla resume los escenarios de usuario habituales para el controlador OLE DB para los usuarios de SQL Server con columnas dispersas:  
  
|Escenario|Comportamiento|  
|--------------|--------------|  
|**Seleccione \* de tabla** o IOpenRowset:: OpenRowset.|Devuelve todas las columnas que no son miembros de disperso **column_set**, más una columna XML que contiene los valores de todas las columnas no nulas que son miembros de disperso **column_set**.|  
|Hacer referencia a una columna por nombre.|Puede hacer referencia a la columna independientemente de su estado de columna dispersa o **column_set** pertenencia.|  
|Acceso **column_set** columnas de miembro en una columna XML calculada.|Columnas que son miembros de disperso **column_set** puede obtenerse acceso seleccionando la **column_set** por su nombre y pueden tener valores de insertar y actualizar mediante la actualización de los datos XML de la **column_set** columna.<br /><br /> El valor debe ajustarse al esquema de **column_set** columnas.|  
|Recuperar metadatos para todas las columnas de una tabla mediante el conjunto de filas de esquema DBSCHEMA_COLUMNS sin restricción de columna (OLE DB).|Devuelve una fila para todas las columnas que no son miembros de un **column_set**. Si la tabla tiene un dispersas **column_set**, se devolverá una fila para él.<br /><br /> Tenga en cuenta que esto no devuelve los metadatos de las columnas que son miembros de un **column_set**.|  
|Recuperar metadatos para todas las columnas, independientemente de la dispersión o la pertenencia a una **column_set**. Esto podría devolver un número muy grande de filas.|Llame a IDBSchemaRowset:: GetRowset para el conjunto de filas de esquema DBSCHEMA_COLUMNS_EXTENDED.|  
|Recuperar metadatos solamente para las columnas que son miembros de un **column_set**. Esto podría devolver un número muy grande de filas.|Llame a IDBSchemaRowset:: GetRowset para el conjunto de filas de esquema DBSCHEMA_SPARSE_COLUMN_SET.|  
|Determinar si una columna es dispersa.|Consulte la columna SS_IS_SPARSE del conjunto de filas de esquema DBSCHEMA_COLUMNS (OLE DB).|  
|Determinar si una columna es una **column_set**.|Consulte la columna SS_IS_COLUMN_SET del conjunto de filas de esquema DBSCHEMA_COLUMNS. O bien, consulte *dwFlags* devueltos por IColumnsInfo:: GetColumnInfo o DBCOLUMNFLAGS del conjunto de filas devuelto por IColumnsRowset:: GetColumnsRowset. Para **column_set** columnas, se establecerá DBCOLUMNFLAGS_SS_ISCOLUMNSET.|  
|Importación y exportación de columnas dispersas en BCP de una tabla sin **column_set**.|Ningún cambio de comportamiento respecto a versiones anteriores del controlador de OLE DB para SQL Server.|  
|Importación y exportación de columnas dispersas en BCP de una tabla con un **column_set**.|El **column_set** se importa y exporta de la misma manera que XML; es decir, como **varbinary (max)** si enlaza como un tipo binario, o como **nvarchar (max)** si enlaza como un **char** o **wchar** tipo.<br /><br /> Columnas que son miembros de disperso **column_set** no se exportan como columnas distintas; sólo se exportan en el valor de la **column_set**.|  
|**Queryout** comportamiento de bcp.|Ningún cambio en el control de columnas nombradas explícitamente desde versiones anteriores del controlador de OLE DB para SQL Server.<br /><br /> Los escenarios que implican la importación y exportación entre tablas con esquemas diferentes pueden requerir un tratamiento especial.<br /><br /> Para obtener más información acerca de BCP, vea Compatibilidad de la copia masiva (BCP) con columnas dispersas, más adelante en este tema.|  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Los clientes de nivel inferior devolverá únicamente los metadatos de las columnas que no son miembros de disperso **column_set** de SQLColumns y DBSCHMA_COLUMNS.
  
 Los clientes de nivel inferior pueden tener acceso a las columnas que son miembros de disperso **column_set** por su nombre y el **column_set** columna será accesible como una columna XML para [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] los clientes.  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Compatibilidad de la copia masiva (BCP) con columnas dispersas  
 No hay ningún cambio en la API de BCP en OLE DB para las columnas dispersas o **column_set** características.  
  
 Si una tabla tiene un **column_set**, las columnas dispersas no se tratan como columnas distintas. Los valores de todas las columnas dispersas están incluidos en el valor de la **column_set**, que se exporta de la misma manera que una columna XML; es decir, como **varbinary (max)** si enlaza como un tipo binario, o como  **nvarchar (max)** si enlaza como un **char** o **wchar** tipo). Durante la importación, el **column_set** el valor debe ajustarse al esquema de la **column_set**.  
  
 Para **queryout** operaciones, no hay ningún cambio en la forma en que se tratan las columnas que los que se hace referencia explícitamente. **COLUMN_SET** columnas tienen el mismo comportamiento que las columnas XML y dispersión no tiene ningún efecto en el tratamiento de las columnas dispersas indicadas.  
  
 Sin embargo, si **queryout** se utiliza para la exportación y hace referencia a las columnas dispersas que son miembros de la columna dispersa establecida por su nombre, no se puede realizar una importación directa en una tabla con estructura similar. Esto es porque BCP utiliza los metadatos de forma coherente con una **seleccione \***  operación para la importación y no se puede hacer coincidir **column_set** columnas de miembros con estos metadatos. Para importar **column_set** las columnas miembro individualmente, debe definir una vista en la tabla que hace referencia a lo que se desea **column_set** columnas y se debe realizar la operación de importación mediante la vista.  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server](../../oledb/oledb-driver-for-sql-server.md)  
  
  
