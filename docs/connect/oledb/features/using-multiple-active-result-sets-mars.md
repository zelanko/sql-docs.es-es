---
title: Uso de conjuntos de resultados activos múltiples (MARS) | Microsoft Docs
description: Utilizar conjuntos de resultados activos múltiples (MARS)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, MARS
- MSOLEDBSQL, MARS
- data access [OLE DB Driver for SQL Server], MARS
- Multiple Active Result Sets
- OLE DB Driver for SQL Server, MARS
- MARS [SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e51a3663504ae7910d53b493a54749a0a670503d
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109427"
---
# <a name="using-multiple-active-result-sets-mars"></a>Utilizar conjuntos de resultados activos múltiples (MARS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se ha introducido la compatibilidad con los conjuntos de resultados activos múltiples (MARS) para las aplicaciones que acceden a [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las aplicaciones de base de datos no podían mantener varias instrucciones activas en una conexión. La aplicación, cuando utilizaba conjuntos de resultados predeterminados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tenía que procesar o cancelar todos los conjuntos de resultados de un lote para poder ejecutar cualquier otro lote en esa conexión. En [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] se introdujo un nuevo atributo de conexión que permite a las aplicaciones tener más de una solicitud pendiente por conexión y, en particular, tener más de un conjunto de resultados predeterminado activo por conexión.  
  
 MARS simplifica el diseño de aplicaciones con una serie de capacidades nuevas que se indican a continuación:  
  
-   Las aplicaciones pueden tener varios conjuntos de resultados predeterminados abiertos e intercalar la lectura de los mismos.  
  
-   Las aplicaciones pueden ejecutar otras instrucciones (por ejemplo, INSERT, UPDATE, DELETE y llamadas a procedimientos almacenados) mientras los conjuntos de resultados predeterminados están abiertos.  
  
 Las aplicaciones que usan MARS encontrarán útiles las siguientes directrices:  
  
-   Los conjuntos de resultados predeterminados deben usarse para conjuntos de resultados cortos o de corta duración generados por instrucciones SQL únicas (SELECT, DML con OUTPUT, RECEIVE, READ TEXT, etc.).  
  
-   Los cursores de servidor deben usarse para conjuntos de resultados mayores o de mayor duración generados por instrucciones SQL únicas.  
  
-   Lea siempre los resultados hasta el final para las solicitudes de procedimientos, independientemente de que devuelvan o no resultados, y para los lotes que devuelven varios resultados.  
  
-   Siempre que sea posible, use llamadas a la API para cambiar las propiedades de conexión y administrar las transacciones con prioridad con respecto a las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
-   En MARS, está prohibida la suplantación de ámbito de sesión mientras se ejecutan lotes simultáneos.  
  
> [!NOTE]  
>  De forma predeterminada, no está habilitada la funcionalidad de MARS. Para usar MARS al conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con el controlador OLE DB para SQL Server, debe habilitarlo específicamente dentro de una cadena de conexión. Para obtener más información, vea el controlador OLE DB para las secciones de SQL Server, más adelante en este tema.  
  
 Controlador OLE DB para SQL Server no limita el número de instrucciones activas en una conexión.  
  
 Las aplicaciones típicas que no necesitan más de un único lote de varias instrucciones o un único procedimiento almacenado que se ejecute al mismo tiempo podrán beneficiarse de MARS sin necesidad de entender cómo se implementa MARS. No obstante, las aplicaciones con requisitos más complejos necesitan tener estas consideraciones en cuenta.  
  
 MARS habilita la ejecución intercalada de varias solicitudes dentro de una única conexión. Es decir, permite la ejecución de un lote y, dentro de su ejecución, permite que se ejecuten otras solicitudes. Tenga en cuenta, no obstante, que MARS se define en términos de intercalación, no de ejecución en paralelo.  
  
 La infraestructura de MARS permite la ejecución de varios lotes en modo intercalado, aunque la ejecución solo puede intercambiarse en puntos bien definidos. Además, la mayoría de las instrucciones deben ejecutarse de forma atómica dentro de un lote. Las instrucciones que devuelven filas al cliente, que también reciben el nombre de *puntos de rendimiento*, pueden intercalar la ejecución antes de completarse mientras se envían filas al cliente; por ejemplo:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Cualquier otra instrucción que se ejecute como parte de un procedimiento almacenado o de un lote deberá ejecutarse hasta completarse para poder cambiar la ejecución a otras solicitudes MARS.  
  
 La manera exacta en la que los lotes intercalan la ejecución se ve afectada por diversos factores, y es difícil predecir la secuencia exacta en la que se ejecutarán los comandos procedentes de varios lotes que contengan puntos de rendimiento. Tenga cuidado para evitar efectos secundarios no deseados debidos a la ejecución intercalada de esos lotes complejos.  
  
 Evite problemas utilizando llamadas a la API en lugar de instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] para administrar el estado de conexión (SET, USE) y las transacciones (BEGIN TRAN, COMMIT, ROLLBACK) no incluyendo estas instrucciones en lotes de varias instrucciones que también contengan puntos de rendimiento y serializando la ejecución de dichos lotes mediante el consumo o la cancelación de todos los resultados.  
  
> [!NOTE]  
>  Un lote o un procedimiento almacenado que inicie una transacción manual o implícita cuando MARS esté habilitado debe completar la transacción antes de salir del lote. Si no lo hace, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] revierte todos los cambios realizados por la transacción cuando finaliza el lote. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] administra este tipo de transacción como una transacción de ámbito de lote. Se trata de un nuevo tipo de transacción que se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] para permitir el uso de procedimientos almacenados con comportamiento correcto cuando MARS está habilitado. Para obtener más información acerca de las transacciones de lote, vea [instrucciones Transaction &#40;Transact-SQL&#41;](../../../t-sql/statements/statements.md).  
  
 Para obtener un ejemplo del uso de MARS desde ADO, vea [utilizar ADO con el controlador OLE DB para SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
## <a name="in-memory-oltp"></a>OLTP en memoria  
 OLTP en memoria admite MARS mediante consultas y procedimientos almacenados compilados de forma nativa. MARS permite solicitantes datos de varias consultas sin necesidad de recuperar completamente cada conjunto antes de enviar una solicitud para capturar las filas de un nuevo conjunto de resultados de resultados. Para leer varios conjuntos de resultados abiertos correctamente, debe usar una conexión MARS habilitado.  
  
 MARS está deshabilitada de forma predeterminada, por lo que debe habilitar explícitamente mediante la adición de `MultipleActiveResultSets=True` en una cadena de conexión. El ejemplo siguiente muestra cómo conectarse a una instancia de SQL Server y especificar que MARS está habilitado:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS con OLTP en memoria es básicamente el mismo que MARS en el resto del motor de SQL. A continuación enumeran las diferencias al utilizar MARS en las tablas optimizadas para memoria y de forma nativa procedimientos almacenados compilados.  
  
 **Las tablas optimizadas para memoria y MARS**  
  
 Estas son las diferencias entre las tablas basadas en disco y optimizadas para memoria cuando el uso de un MARS habilitado conexión:  
  
-   Dos instrucciones pueden modificar los datos en el mismo objeto de destino, pero si intentan modificar el mismo registro un conflicto de escritura contra escritura hará que la operación de nuevo un error. Sin embargo, si ambas operaciones modifican distintos registros, las operaciones se realizará correctamente.  
  
-   Cada instrucción se ejecuta con aislamiento de instantánea para que nuevas operaciones no pueden ver los cambios realizados por las instrucciones existentes. Incluso si se ejecutan las instrucciones simultáneas en la misma transacción el motor SQL crea transacciones de lote para cada instrucción que están aisladas entre sí. Sin embargo, las transacciones de lote todavía se enlazan juntos para la reversión de una transacción de lote afecta a otros registros en el mismo lote.  
  
-   No se permiten operaciones de DDL en las transacciones de usuario inmediatamente generará un error.  
  
 **MARS y procedimientos almacenados compilados de forma nativa**  
  
 Procedimientos almacenados compilados de forma nativa se pueden ejecutar en las conexiones de MARS habilitado y pueden ceda la ejecución a otra instrucción solo cuando se encuentra un punto de rendimiento. Un punto de rendimiento requiere una instrucción SELECT, que es la única instrucción en un procedimiento almacenado compilado de forma nativa que puede ofrecer la ejecución a otra instrucción. Si una instrucción SELECT no está presente en el procedimiento no dará como resultado, se ejecutará hasta su finalización antes de comenzar otras instrucciones.  
  
 **Transacciones de MARS y OLTP en memoria**  
  
 Los cambios realizados por instrucciones y bloques atomic que se intercalan están aislados entre sí. Por ejemplo, si una instrucción o bloque atomic realiza algunos cambios y, a continuación, proporciona una ejecución a otra instrucción, la nueva instrucción no verán los cambios realizados por la primera instrucción. Además, cuando la primera instrucción reanuda la ejecución, no verán los cambios realizados por cualquier otra instrucción. Las instrucciones solo verá los cambios que se finaliza y confirma antes de que se inicia la instrucción.  
  
 Se puede iniciar una nueva transacción de usuario dentro de la transacción de usuario actual mediante la instrucción BEGIN TRANSACTION: Esto se admite solo en modo de interoperabilidad, por lo que solo se puede llamar a BEGIN TRANSACTION de una instrucción de Transact-SQL y no desde dentro de compilado de forma nativa almacenan procedimiento. Puede crear una operación de guardar punto en una transacción utilizando SAVE TRANSACTION o una llamada de API a la transacción. Save(save_point_name) para revertir al punto de retorno. Esta característica también se habilita solo desde las instrucciones de T-SQL y no desde dentro de forma nativa procedimientos almacenados compilados.  
  
 **MARS y los índices de almacén de columnas**  
  
 SQL Server (a partir de 2016) es compatible con MARS con índices de almacén de columnas. SQL Server 2014 usa MARS para las conexiones de solo lectura a las tablas con un índice de almacén de columnas.    Pero SQL Server 2014 no es compatible con MARS para operaciones simultáneas de lenguaje de manipulación de datos (DML) en una tabla con un índice de almacén de columnas. Cuando ocurre esto, SQL Server termina las conexiones y anula las transacciones.   SQL Server 2012 tiene índices de almacén de columnas de sólo lectura y MARS no se aplica a ellos.  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server  
 El controlador OLE DB para SQL Server admite MARS mediante la adición de la propiedad de inicialización de origen de datos SSPROP_INIT_MARSCONNECTION, que se implementa en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT. Además, se ha agregado una nueva palabra clave de cadena de conexión, **MarsConn**. Acepta **true** o **false** valores; **false** es el valor predeterminado.  
  
 El valor predeterminado de la propiedad de origen de datos DBPROP_MULTIPLECONNECTIONS es VARIANT_TRUE. Esto significa que el proveedor generará varias conexiones para admitir varios comandos y objetos de conjunto de filas simultáneos. Cuando MARS está habilitado, el controlador OLE DB para SQL Server puede admitir varios comandos y objetos de conjunto de filas en una única conexión, por lo que MULTIPLE_CONNECTIONS se establece de forma predeterminada en VARIANT_FALSE.  
  
 Para obtener más información acerca de las mejoras realizadas en el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT, vea [propiedades de inicialización y autorización](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="ole-db-driver-for-sql-server-example"></a>Ejemplo de controlador OLE DB para SQL Server  
 En este ejemplo, se crea un objeto de origen de datos con el controlador OLE DB para SQL Server y se habilita MARS con el conjunto de propiedades DBPROPSET_SQLSERVERDBINIT antes de crear el objeto de sesión.  
  
```  
#include <msoledbsql.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  

  
## <a name="see-also"></a>Ver también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 
  
  
