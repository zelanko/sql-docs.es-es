---
title: Realizar operaciones de copia masiva | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [SQL Server Native Client]
- data access [SQL Server Native Client], bulk copy operations
- SQL Server Native Client, bulk copy operations
- SQLNCLI, bulk copy operations
ms.assetid: 50d8456b-e6a1-4b25-bc7e-56946ed654a7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cce9b961c2830b670bb862dee88284a18ed7eb6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363307"
---
# <a name="performing-bulk-copy-operations"></a>Realizar operaciones de copia masiva
  La característica de copia masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite la transferencia de grandes cantidades de datos a una tabla o vista de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o desde ella. Los datos también pueden transferirse especificando una instrucción SELECT. Los datos pueden moverse entre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y un archivo de datos del sistema operativo, como un archivo ASCII. El archivo de datos puede tener diferentes formatos; el formato para una copia masiva se define en un archivo de formato. Opcionalmente, los datos pueden cargarse en variables de programa y transferirse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante funciones y métodos de copia masiva.  
  
 Para una aplicación de ejemplo que ilustra esta característica, consulte [Bulk Copy datos utilizando IRowsetFastLoad &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/irowsetfastload-ole-db.md).  
  
 Normalmente, una aplicación utiliza la copia masiva de una de las siguientes formas:  
  
-   Copia masiva de una tabla, una vista o el conjunto de resultados de una instrucción Transact-SQL a un archivo de datos donde los datos se almacenan en el mismo formato que la tabla o vista.  
  
     Recibe el nombre de archivo de datos en modo nativo.  
  
-   Copia masiva de una tabla, una vista o el conjunto de resultados de una instrucción Transact-SQL a un archivo de datos donde los datos se almacenan en un formato distinto al de la tabla o vista.  
  
     En este caso, se crea un archivo de formato independiente que define las características (tipo de datos, posición, longitud, terminador, etc.) de cada columna cuando se almacena en el archivo de datos. Si todas las columnas se convierten a un formato de caracteres, el archivo resultante se denomina archivo de datos en modo de carácter.  
  
-   Copia masiva de un archivo de datos a una tabla o vista.  
  
     Si es necesario, se usa un archivo de formato para determinar el diseño del archivo de datos.  
  
-   Carga de datos en variables de programa y, a continuación, importación de los datos en una tabla o vista mediante las funciones de copia masiva a fin de copiar de forma masiva una fila cada vez.  
  
 Los archivos de datos utilizados por las funciones de copia masiva no tienen que ser creados por otro programa de copia masiva. Cualquier otro sistema puede generar un archivo de datos y un archivo de formato según las definiciones de copia masiva; estos archivos pueden utilizarse posteriormente con un programa de copia masiva de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para importar datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por ejemplo, puede exportar datos de una hoja de cálculo a un archivo delimitado por tabuladores, generar un archivo de formato que describa el archivo delimitado por tabuladores y, a continuación, usar un programa de copia masiva para importar rápidamente los datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los archivos de datos generados por la copia masiva también pueden importarse en otras aplicaciones. Por ejemplo, puede usar las funciones de copia masiva para exportar datos de una tabla o vista a un archivo delimitado por tabuladores que, a su vez, puede cargarse en una hoja de cálculo.  
  
 Los programadores que codifican aplicaciones para usar las funciones de copia masiva deben seguir las reglas generales para obtener un rendimiento adecuado de la copia masiva. Para obtener más información acerca del soporte para operaciones de copia masiva en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [importación masiva y la exportación de datos de &#40;de SQL Server&#41;](../../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Debe enlazarse un tipo definido por el usuario CLR (UDT) en forma de datos binarios. Aunque un archivo de formato especifique SQLCHAR como tipo de datos de una columna UDT de destino, la utilidad BCP considerará los datos como binarios.  
  
 No use SET FMTONLY OFF con operaciones de copia masiva. SET FMTONLY OFF puede hacer que la operación de copia masiva no se ejecute correctamente o genere resultados inesperados.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 La [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor implementa dos métodos para realizar operaciones de copia masiva con un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos. El primer método implica el uso de la interfaz [IRowsetFastLoad](../../native-client-ole-db-interfaces/irowsetfastload-ole-db.md) en operaciones de copia masiva basadas en memoria; el segundo, implica el uso de la interfaz [IBCPSession](../../native-client-ole-db-interfaces/ibcpsession-ole-db.md) en operaciones de copia masiva basadas en archivos.  
  
### <a name="using-memory-based-bulk-copy-operations"></a>Usar operaciones de copia masiva basadas en memoria  
 La [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor implementa la **IRowsetFastLoad** interfaz para exponer el soporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las operaciones de copia masiva basadas en memoria. La interfaz **IRowsetFastLoad** implementa los métodos [IRowsetFastLoad::Commit](../../native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) e [IRowsetFastLoad::InsertRow](../../native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md).  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>Habilitar una sesión para IRowsetFastLoad  
 El consumidor notifica al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client su necesidad de una copia masiva mediante el establecimiento de la propiedad SSPROP_ENABLEFASTLOAD de origen de datos específica del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client en VARIANT_TRUE. Con la propiedad establecida en el origen de datos, el consumidor crea una sesión de proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. La nueva sesión permite al consumidor acceder a la interfaz **IRowsetFastLoad**.  
  
> [!NOTE]  
>  Si se usa la interfaz **IDataInitialize** para inicializar el origen de datos, es necesario establecer la propiedad SSPROP_IRowsetFastLoad en el parámetro *rgPropertySets* del método **IOpenRowset::OpenRowset**; de lo contrario, la llamada al método **OpenRowset** devolverá E_NOINTERFACE.  
  
 Al habilitar una sesión para la copia masiva, se restringe la compatibilidad del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client con las interfaces en la sesión. Una sesión habilitada para copia masiva solo expone las interfaces siguientes:  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 Para deshabilitar la creación de conjuntos de filas habilitados para copia masiva y revertir la sesión del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client al procesamiento estándar, vuelva a establecer SSPROP_ENABLEFASTLOAD en VARIANT_FALSE.  
  
#### <a name="irowsetfastload-rowsets"></a>Conjuntos de filas IRowsetFastLoad  
 Los conjuntos de filas de copia masiva del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client son de solo escritura, pero exponen interfaces que permiten al consumidor determinar la estructura de una tabla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En un conjunto de filas del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client habilitado para copia masiva se exponen las siguientes interfaces:  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 Las propiedades específicas del proveedor SSPROP_FASTLOADOPTIONS, SSPROP_FASTLOADKEEPNULLS y SSPROP_FASTLOADKEEPIDENTITY controlan el comportamiento de los conjuntos de filas de copia masiva de proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Las propiedades se especifican en el *rgProperties* miembro de un * rgPropertySets ***IOpenRowset**miembro de parámetro.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|Columna: No<br /><br /> R/W: Lectura/escritura<br /><br /> Tipo: VT_BOOL<br /><br /> Predeterminado: VARIANT_FALSE<br /><br /> Descripción: Mantiene valores de identidad suministrados por el consumidor.<br /><br /> VARIANT_FALSE: Los valores para una columna de identidad de la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se generan por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cualquier valor enlazado de la columna no tiene en cuenta el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor.<br /><br /> VARIANT_TRUE: El consumidor enlaza un descriptor de acceso que proporciona un valor para una columna de identidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La propiedad de identidad no está disponible en las columnas que aceptan valores NULL, por lo que el consumidor proporciona un valor único en cada llamada a **IRowsetFastLoad::Insert**.|  
|SSPROP_FASTLOADKEEPNULLS|Columna: No<br /><br /> R/W: Lectura/escritura<br /><br /> Tipo: VT_BOOL<br /><br /> Predeterminado: VARIANT_FALSE<br /><br /> Descripción: Mantiene NULL en las columnas con una restricción DEFAULT. Solo afecta a las columnas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que aceptan valores NULL y tienen aplicada una restricción DEFAULT.<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inserta el valor predeterminado de la columna cuando el consumidor del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client inserta una fila que contiene NULL para la columna.<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inserta el valor NULL como valor de columna cuando el consumidor del proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client inserta una fila que contiene NULL para la columna.|  
|SSPROP_FASTLOADOPTIONS|Columna: No<br /><br /> R/W: Lectura/escritura<br /><br /> Tipo: VT_BSTR<br /><br /> Valor predeterminado: ninguno<br /><br /> Descripción: Esta propiedad es el mismo que el **-h** "*sugerencia*[,... *n*] "opción de la **bcp** utilidad. Las cadenas que se indican a continuación pueden utilizarse como opciones para la copia masiva de datos en una tabla.<br /><br /> **ORDEN**(*columna*[**ASC** &#124; **DESC**] [,... *n*]): Criterio de ordenación de los datos en el archivo de datos. El rendimiento de la copia masiva mejora si el archivo de datos que se carga se ordena según el índice clúster de la tabla.<br /><br /> **ROWS_PER_BATCH** = *bb*: Número de filas de datos por lote (como *bb*). El servidor optimiza la carga masiva según el valor *bb*. De forma predeterminada, el valor de **ROWS_PER_BATCH** es desconocido.<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: Número de kilobytes (KB) de datos por lote (como cc). De forma predeterminada, el valor de **KILOBYTES_PER_BATCH** es desconocido.<br /><br /> **TABLOCK**: Se adquiere un bloqueo de nivel de tabla durante la operación de copia masiva. Esta opción mejora notablemente el rendimiento ya que, al mantenerse el bloqueo solamente durante la operación de copia masiva, se reduce la contención en la tabla por bloqueo. Varios clientes pueden cargar una tabla de forma simultánea si esta no tiene índices y se especifica **TABLOCK**. De forma predeterminada, el comportamiento del bloqueo viene determinado por la opción de tabla **table lock on bulk load**.<br /><br /> **CHECK_CONSTRAINTS**: Todas las restricciones de *table_name* durante la operación de copia masiva se comprueban. De forma predeterminada, se omiten las restricciones.<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa las versiones de fila para los desencadenadores y almacena las versiones de fila en el almacén de versiones, en **tempdb**. Por lo tanto, las optimizaciones de registro masivo están disponibles incluso si están habilitados los desencadenadores. Antes de realizar una importación masiva de un lote con un número elevado de filas y los desencadenadores habilitados, puede que tenga que ampliar el tamaño de **tempdb**.|  
  
### <a name="using-file-based-bulk-copy-operations"></a>Usar operaciones de copia masiva basadas en archivos  
 La [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor implementa la **IBCPSession** interfaz para exponer el soporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operaciones de copia masiva basadas en archivos. La interfaz **IBCPSession** implementa los métodos [IBCPSession::BCPColFmt](../../native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md), [IBCPSession::BCPColumns](../../native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md), [IBCPSession::BCPControl](../../native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md), [IBCPSession::BCPDone](../../native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md), [IBCPSession::BCPExec](../../native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md), [IBCPSession::BCPInit](../../native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md), [IBCPSession::BCPReadFmt](../../native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md) e [IBCPSession::BCPWriteFmt](../../native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client mantiene la misma compatibilidad con las operaciones de copia masiva que formaban parte de las versiones anteriores del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener información sobre las operaciones de copia masiva con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC nativo de cliente, consulte [Performing Bulk Copy Operations &#40;ODBC&#41;](../../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)   
 [Propiedades del origen de datos &#40;OLE DB&#41;](../../native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [Importar y exportar datos en bloque &#40;SQL Server&#41;](../../import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/irowsetfastload-ole-db.md)   
 [IBCPSession &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [Optimizar el rendimiento de una importación en bloque](https://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  
  
  
