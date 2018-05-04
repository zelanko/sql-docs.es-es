---
title: Realizar operaciones de copia masiva | Documentos de Microsoft
description: Realizar operaciones de copia masiva mediante el controlador OLE DB para SQL Server
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
- bulk copy [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], bulk copy operations
- OLE DB Driver for SQL Server, bulk copy operations
- MSOLEDBSQL, bulk copy operations
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 210aa79c589c241056aa6b7e342125553b6257b4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="performing-bulk-copy-operations"></a>Realizar operaciones de copia masiva
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La característica de copia masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite la transferencia de grandes cantidades de datos a una tabla o vista de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o desde ella. Los datos también pueden transferirse especificando una instrucción SELECT. Los datos pueden moverse entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y un archivo de datos del sistema operativo, como un archivo ASCII. El archivo de datos puede tener diferentes formatos; el formato para una copia masiva se define en un archivo de formato. Opcionalmente, los datos pueden cargarse en variables de programa y transferirse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante funciones y métodos de copia masiva.  
  
 Para una aplicación de ejemplo que muestra esta característica, consulte [datos masiva copia masiva con IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md).  
  
 Normalmente, una aplicación utiliza la copia masiva de una de las siguientes formas:  
  
-   Copia masiva de una tabla, una vista o el conjunto de resultados de una instrucción Transact-SQL a un archivo de datos donde los datos se almacenan en el mismo formato que la tabla o vista.  
  
     Recibe el nombre de archivo de datos en modo nativo.  
  
-   Copia masiva de una tabla, una vista o el conjunto de resultados de una instrucción Transact-SQL a un archivo de datos donde los datos se almacenan en un formato distinto al de la tabla o vista.  
  
     En este caso, se crea un archivo de formato independiente que define las características (tipo de datos, posición, longitud, terminador, etc.) de cada columna cuando se almacena en el archivo de datos. Si todas las columnas se convierten a un formato de caracteres, el archivo resultante se denomina archivo de datos en modo de carácter.  
  
-   Copia masiva de un archivo de datos a una tabla o vista.  
  
     Si es necesario, se usa un archivo de formato para determinar el diseño del archivo de datos.  
  
-   Carga de datos en variables de programa y, a continuación, importación de los datos en una tabla o vista mediante las funciones de copia masiva a fin de copiar de forma masiva una fila cada vez.  
  
 Los archivos de datos utilizados por las funciones de copia masiva no tienen que ser creados por otro programa de copia masiva. Cualquier otro sistema puede generar un archivo de datos y un archivo de formato según las definiciones de copia masiva; estos archivos pueden utilizarse posteriormente con un programa de copia masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para importar datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por ejemplo, puede exportar datos de una hoja de cálculo a un archivo delimitado por tabuladores, generar un archivo de formato que describa el archivo delimitado por tabuladores y, a continuación, usar un programa de copia masiva para importar rápidamente los datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los archivos de datos generados por la copia masiva también pueden importarse en otras aplicaciones. Por ejemplo, puede usar las funciones de copia masiva para exportar datos de una tabla o vista a un archivo delimitado por tabuladores que, a su vez, puede cargarse en una hoja de cálculo.  
  
 Los programadores que codifican aplicaciones para usar las funciones de copia masiva deben seguir las reglas generales para obtener un rendimiento adecuado de la copia masiva. Para obtener más información sobre la compatibilidad con operaciones de copia masiva en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [importación y exportación de datos &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Debe enlazarse un tipo definido por el usuario CLR (UDT) en forma de datos binarios. Aunque un archivo de formato especifique SQLCHAR como tipo de datos de una columna UDT de destino, la utilidad BCP considerará los datos como binarios.  
  
 No use SET FMTONLY OFF con operaciones de copia masiva. SET FMTONLY OFF puede hacer que la operación de copia masiva no se ejecute correctamente o genere resultados inesperados.  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server 
 El controlador OLE DB para SQL Server implementa dos métodos para realizar operaciones de copia masiva con un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos. El primer método implica el uso de la [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) interfaz para operaciones de copia masiva basadas en memoria; y el segundo implica el uso de la [IBCPSession](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md) interfaz para operaciones de copia masiva basadas en archivos.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>Usar operaciones de copia masiva basadas en memoria  
 El controlador OLE DB para SQL Server implementa la **IRowsetFastLoad** interfaz para exponer la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las operaciones de copia masiva basadas en memoria. El **IRowsetFastLoad** implementa la interfaz la [IRowsetFastLoad:: Commit](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md) y [IRowsetFastLoad:: insertRow](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) métodos.  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>Habilitar una sesión para IRowsetFastLoad  
 El consumidor notifica el controlador OLE DB para SQL Server de su necesidad de copia masiva estableciendo el controlador OLE DB para la propiedad de origen de datos SQL Server específica SSPROP_ENABLEFASTLOAD en VARIANT_TRUE. Con la propiedad establecida en el origen de datos, el consumidor crea un controlador de OLE DB para la sesión de SQL Server. La nueva sesión permite el acceso del consumidor a la **IRowsetFastLoad** interfaz.  
  
> [!NOTE]  
>  Si el **IDataInitialize** interfaz se usa para inicializar el origen de datos, entonces es necesario establecer la propiedad SSPROP_IRowsetFastLoad el *rgPropertySets* parámetro de la  **IOpenRowset:: OpenRowset** método; en caso contrario, la llamada a la **OpenRowset** método devolverá E_NOINTERFACE.  
  
 Al habilitar una sesión de copia masiva, restringe al controlador OLE DB para SQL Server admiten para las interfaces en la sesión. Una sesión habilitada para copia masiva solo expone las interfaces siguientes:  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 Para deshabilitar la creación de conjuntos de filas habilitados para copia masiva y hacer que el controlador OLE DB para la sesión de SQL Server revertir al procesamiento estándar, SSPROP_ENABLEFASTLOAD en VARIANT_FALSE.  
  
#### <a name="irowsetfastload-rowsets"></a>Conjuntos de filas IRowsetFastLoad  
 El controlador OLE DB para conjuntos de filas de copia de forma masiva de SQL Server son de solo escritura, pero exponen interfaces que permiten al consumidor determinar la estructura de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla. Se exponen las interfaces siguientes en una copia habilitada de forma masiva controlador OLE DB para el conjunto de filas de SQL Server:  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 Las propiedades específicas del proveedor SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS y SSPROP_FASTLOADKEEPIDENTITY controlan comportamientos de un controlador de OLE DB para el conjunto de filas de copia masiva de SQL Server. Las propiedades se especifican en el *rgProperties* miembro de un *rgPropertySets* **IOpenRowset** miembro de parámetro.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|Columna: no<br /><br /> L/E lectura/escritura<br /><br /> Tipo: VT_BOOL<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: mantiene valores de identidad suministrados por el consumidor.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera valores para una columna de identidad de la tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se omite cualquier valor enlazado para la columna por el controlador OLE DB para SQL Server.<br /><br /> VARIANT_TRUE: el consumidor enlaza un descriptor de acceso que proporciona un valor para una columna de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La propiedad identity no está disponible en las columnas que aceptan valores NULL, por lo que el consumidor proporciona un valor único en cada **IRowsetFastLoad:: Insert** llamar.|  
|SSPROP_FASTLOADKEEPNULLS|Columna: no<br /><br /> L/E lectura/escritura<br /><br /> Tipo: VT_BOOL<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: mantiene NULL en las columnas con una restricción DEFAULT. Solo afecta a las columnas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que aceptan valores NULL y tienen aplicada una restricción DEFAULT.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inserta el valor predeterminado de la columna cuando el controlador OLE DB para el consumidor de SQL Server se inserta una fila que contiene NULL para la columna.<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inserta NULL para el valor de columna cuando el controlador OLE DB para el consumidor de SQL Server se inserta una fila que contiene NULL para la columna.|  
|SSPROP_FASTLOADOPTIONS|Columna: no<br /><br /> L/E lectura/escritura<br /><br /> Tipo: VT_BSTR<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: Esta propiedad es el mismo que el **-h** "*sugerencia*[,... *n*] "opción de la **bcp** utilidad. Las cadenas que se indican a continuación pueden utilizarse como opciones para la copia masiva de datos en una tabla.<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,... *n*]): criterio de ordenación de datos en el archivo de datos. El rendimiento de la copia masiva mejora si el archivo de datos que se carga se ordena según el índice clúster de la tabla.<br /><br /> **ROWS_PER_BATCH** = *bb*: número de filas de datos por lote (como *bb*). El servidor optimiza la carga masiva según el valor *bb*. De forma predeterminada, **ROWS_PER_BATCH** es desconocido.<br /><br /> **Valor de KILOBYTES_PER_BATCH** = *cc*: número de kilobytes (KB) de datos por lote (como cc). De forma predeterminada, **KILOBYTES_PER_BATCH** es desconocido.<br /><br /> **TABLOCK**: se adquiere un bloqueo de nivel de tabla para la duración de la operación de copia masiva. Esta opción mejora notablemente el rendimiento ya que, al mantenerse el bloqueo solamente durante la operación de copia masiva, se reduce la contención en la tabla por bloqueo. Una tabla pueden cargar mediante varios clientes simultáneamente si la tabla no tiene índices y **TABLOCK** se especifica. De forma predeterminada, el comportamiento de bloqueo está determinado por la opción de tabla **bloqueo en una carga masiva de tabla**.<br /><br /> **Check_constraints**: las restricciones en *table_name* durante la operación de copia masiva se comprueban. De forma predeterminada, se omiten las restricciones.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa las versiones de fila para los desencadenadores y almacena las versiones de fila en el almacén de versiones en **tempdb**. Por lo tanto, las optimizaciones de registro masivo están disponibles incluso si están habilitados los desencadenadores. Antes de realizar una importación masiva con un gran número de filas con los desencadenadores habilitados, puede que necesite ampliar el tamaño de **tempdb**.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>Usar operaciones de copia masiva basadas en archivos  
 El controlador OLE DB para SQL Server implementa la **IBCPSession** interfaz para exponer la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operaciones de copia masiva basadas en archivos. El **IBCPSession** implementa la interfaz la [ibcpsession:: BCPColFmt](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [ibcpsession:: BCPColumns](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [ibcpsession:: Bcpcontrol](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [IBCPSession::BCPDone](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [Ibcpsession](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [ibcpsession:: BCPInit](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [ibcpsession:: Bcpreadfmt](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md), y [ibcpsession:: Bcpwritefmt](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)métodos.  
  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [Propiedades del origen de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-ole-db.md)   
 [Optimizar el rendimiento de la importación masiva](http://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  

