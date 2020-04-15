---
title: Compatibilidad con columnas dispersas en SQL Native Client
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 958424a4710b76e7e09ae15e10b612630f09eee3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303794"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>Compatibilidad con columnas dispersas en SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client admite las columnas dispersas. Para más información sobre columnas dispersas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Usar columnas dispersas](../../../relational-databases/tables/use-sparse-columns.md) y [Usar conjuntos de columnas](../../../relational-databases/tables/use-column-sets.md).  
  
 Para obtener más información acerca [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de la compatibilidad con columnas dispersas en Native Client, vea [Compatibilidad con columnas dispersas &#40;&#41;ODBC](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md) y Compatibilidad con columnas [dispersas &#40;&#41;OLE DB ](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md).  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>Escenarios de usuarios de columnas dispersas y SQL Server Native Client  
 En la tabla siguiente se resumen los escenarios comunes de usuario para los usuarios de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con columnas dispersas:  
  
|Escenario|Comportamiento|  
|--------------|--------------|  
|**select \* from table** o IOpenRowset::OpenRowset.|Devuelve todas las columnas que no son miembros del **column_set** disperso, más una columna XML que contiene los valores de todas las columnas no nulas que son miembros del **column_set** disperso.|  
|Hacer referencia a una columna por nombre.|Se puede hacer referencia a la columna independientemente de su estado de columna dispersa o la pertenencia al **column_set**.|  
|Obtener acceso a las columnas miembro del **column_set** a través de una columna XML calculada.|Se puede acceder a las columnas que son miembros del **column_set** disperso al seleccionar el **column_set** por nombre y se puede hacer que se inserten y actualicen los valores al actualizar el XML de la columna **column_set**.<br /><br /> El valor debe cumplir el esquema de las columnas **column_set**.|  
|Recuperar metadatos para todas las columnas de una tabla a través de SQLColumns con un patrón de búsqueda de columna de NULL o '%' (ODBC); o a través del conjunto de filas de esquema DBSCHEMA_COLUMNS sin restricción de columna (OLE DB).|Devuelve una fila para todas las columnas que no son miembros del **column_set**. Si la tabla tiene un **column_set** disperso, se devolverá una fila.<br /><br /> Observe que esto no devuelve los metadatos de las columnas que son miembros del **column_set**.|  
|Recuperar los metadatos de todas las columnas, independientemente de la dispersión o pertenencia en un **column_set**. Esto podría devolver un número muy grande de filas.|Establezca el campo descriptor SQL_SOPT_SS_NAME_SCOPE en SQL_SS_NAME_SCOPE_EXTENDED y llame a [SQLColumns](../../../relational-databases/native-client-odbc-api/sqlcolumns.md) (ODBC).<br /><br /> Llame a IDBSchemaRowset::GetRowset para el conjunto de filas de esquema de DBSCHEMA_COLUMNS_EXTENDED (OLE DB).<br /><br /> Este escenario no es posible en una aplicación que utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una versión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Sin embargo, este tipo de aplicación podría consultar directamente las vistas del sistema.|  
|Recuperar únicamente los metadatos de las columnas que son miembros del **column_set**. Esto podría devolver un número muy grande de filas.|Establezca el campo descriptor SQL_SOPT_SS_NAME_SCOPE en SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET y llame a SQLColumns (ODBC).<br /><br /> Llame a IDBSchemaRowset::GetRowset para el conjunto de filas de esquema de DBSCHEMA_SPARSE_COLUMN_SET (OLE DB).<br /><br /> Este escenario no es posible en una aplicación que utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una versión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Sin embargo, este tipo de aplicación podría consultar las vistas del sistema.|  
|Determinar si una columna es dispersa.|Consulte la columna SS_IS_SPARSE del conjunto de resultados SQLColumns (ODBC).<br /><br /> Consulte la columna SS_IS_SPARSE del conjunto de filas de esquema DBSCHEMA_COLUMNS (OLE DB).<br /><br /> Este escenario no es posible en una aplicación que utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una versión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Sin embargo, este tipo de aplicación podría consultar las vistas del sistema.|  
|Determine si una columna es **column_set**.|Consulte la columna SS_IS_COLUMN_SET del conjunto de resultados SQLColumns. O bien, consulte el atributo de columna SQL_CA_SS_IS_COLUMN_SET específico de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (ODBC).<br /><br /> Consulte la columna SS_IS_COLUMN_SET del conjunto de filas de esquema DBSCHEMA_COLUMNS. O bien, consulte *dwFlags* devuelto por IColumnsinfo::GetColumnInfo o DBCOLUMNFLAGS en el conjunto de filas devuelto por IColumnsRowset::GetColumnsRowset. Para **column_set** columnas, se establecerá DBCOLUMNFLAGS_SS_ISCOLUMNSET (OLE DB).<br /><br /> Este escenario no es posible en una aplicación que utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en una versión anterior a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. Sin embargo, este tipo de aplicación podría consultar las vistas del sistema.|  
|Importar y exportar columnas dispersas en BCP de una tabla sin **column_set**.|Ningún cambio en el comportamiento desde las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|Importar y exportar columnas dispersas en BCP de una tabla con **column_set**.|**column_set** se importa y se exporta de la misma forma que una columna XML; es decir, como **varbinary(max)** si se enlaza como un tipo binario, o como **nvarchar(max)** si se enlaza como un tipo **char** o **wchar**.<br /><br /> Las columnas que son miembro del **column_set** disperso no se exportan como columnas distintas; se exportan solo en el valor del **column_set**.|  
|Comportamiento de **queryout** para BCP.|Ningún cambio en el tratamiento de columnas nombradas explícitamente desde las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.<br /><br /> Los escenarios que implican la importación y exportación entre tablas con esquemas diferentes pueden requerir un tratamiento especial.<br /><br /> Para obtener más información acerca de BCP, vea Compatibilidad de la copia masiva (BCP) con columnas dispersas, más adelante en este tema.|  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Los clientes de nivel inferior solo devolverán los metadatos de las columnas que no son miembro del **column_set** disperso para SQLColumns y DBSCHMA_COLUMNS. Los conjuntos de filas de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] esquema OLE DB adicionales introducidos en Native Client no estarán disponibles, ni las modificaciones en SQLColumns en ODBC a través de SQL_SOPT_SS_NAME_SCOPE.  
  
 Los clientes de nivel inferior pueden acceder a las columnas que son miembros del **column_set** disperso por nombre, y la columna del **column_set** será accesible como una columna XML para los clientes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>Compatibilidad de la copia masiva (BCP) con columnas dispersas  
 No hay cambios en la API de BCP en ODBC u OLE DB para las columnas dispersas o **column_set** características.  
  
 Si una tabla tiene un **column_set**, las columnas dispersas no se tratan como columnas distintas. Los valores de todas las columnas dispersas están incluidos en el valor de **column_set**, que se exporta de la misma manera que una columna XML; es decir, como **varbinary(max)** si se enlaza como un tipo binario, o como **nvarchar(max)** si se enlaza como un tipo **char** o **wchar**. En la importación, el valor de **column_set** debe cumplir el esquema de **column_set**.  
  
 Para las operaciones **queryout**, no hay ningún cambio en la manera en que se tratan las columnas a las que se hace referencia. Las columnas **column_set** tienen el mismo comportamiento que las columnas XML y la dispersión no tiene ningún efecto en el tratamiento de las columnas dispersas indicadas.  
  
 En cambio, si se usa **queryout** para la exportación y hace referencia a las columnas dispersas que son miembros de la columna dispersa establecida por nombre, no puede realizar una importación directa en una tabla con estructura similar. Esto se debe a que BCP usa metadatos coherentes con una operación **de &#42;** de selección para la importación y no puede hacer coincidir **column_set** columnas de miembro con estos metadatos. Para importar individualmente las columnas miembro del **column_set**, debe definir una vista en la tabla que haga referencia a las columnas **column_set** deseadas y debe realizar la operación de importación mediante la vista.  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
