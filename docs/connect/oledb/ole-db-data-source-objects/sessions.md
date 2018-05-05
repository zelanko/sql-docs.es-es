---
title: Las sesiones | Documentos de Microsoft
description: Sesiones de controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d5aed67da19db68097f57f689ad0a26692d75f63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sessions"></a>Sesiones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Un controlador de OLE DB para la sesión de SQL Server representa una conexión única a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El controlador OLE DB para SQL Server requiere que las sesiones delimiten el espacio de transacciones para un origen de datos. Todos los objetos de comando creados a partir de un objeto de sesión concreto participan en la transacción local o distribuida del objeto de sesión.  
  
 El primer objeto de sesión creado en el origen de datos inicializado recibe la conexión a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] establecida en la inicialización. Cuando se liberan todas las referencias en las interfaces del objeto de sesión, la conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pasa a estar disponible para otro objeto de sesión creado en el origen de datos.  
  
 Un objeto de sesión adicional creado en el origen de datos establece su propia conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tal como especifica el origen de datos. La conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se quita cuando la aplicación libera todas las referencias a los objetos creados en dicha sesión.  
  
 En el ejemplo siguiente se muestra cómo utilizar el controlador OLE DB para SQL Server para conectarse a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos:  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 Conectar el controlador OLE DB para los objetos de sesión de SQL Server a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede generar una sobrecarga significativa para las aplicaciones que continuamente crear y liberar objetos de sesión. Puede minimizar la sobrecarga al administrar eficazmente controlador OLE DB para los objetos de sesión de SQL Server. Controlador de OLE DB para las aplicaciones de SQL Server puede mantener el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conexión de un objeto de sesión activo si mantienen una referencia en al menos una interfaz del objeto.  
  
 Si se mantiene un grupo de referencias a objeto de creación de comando, por ejemplo, se mantienen conexiones activas para estos objetos de sesión en el grupo. Como los objetos de sesión son necesarios, el código de mantenimiento de grupo pasa válido **IDBCreateCommand** puntero de interfaz para el método de aplicación que requiere la sesión. Cuando el método de aplicación ya no requiere la sesión, devuelve el puntero de interfaz al código de mantenimiento de grupo en lugar de liberar la referencia de la aplicación al objeto de creación de comando.  
  
> [!NOTE]  
>  En el ejemplo anterior, el **IDBCreateCommand** interfaz se usa porque el **ICommand** implementa la interfaz la **GetDBSession**  /método siguiente, el único método en el ámbito de comando o conjunto de filas que permite que un objeto determinar la sesión en el que se creó. Por tanto, un objeto de comando, y solo un objeto de comando, permite a una aplicación recuperar un puntero de objeto de origen de datos a partir del cual se pueden crear sesiones adicionales.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de origen de datos & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
