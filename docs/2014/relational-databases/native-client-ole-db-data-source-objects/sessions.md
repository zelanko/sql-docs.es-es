---
title: Sesiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 3a980816-675c-4fba-acc9-429297d85bbd
author: rothja
ms.author: jroth
ms.openlocfilehash: b3b31c9ee3d14dcc65b44194b5e9cc2aff85215b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056345"
---
# <a name="sessions"></a>Sesiones
  Una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión de proveedor de OLE DB de cliente nativo representa una conexión única a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client requiere que las sesiones delimiten el espacio de transacciones para un origen de datos. Todos los objetos de comando creados a partir de un objeto de sesión concreto participan en la transacción local o distribuida del objeto de sesión.  
  
 El primer objeto de sesión creado en el origen de datos inicializado recibe la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establecida en la inicialización. Cuando se liberan todas las referencias en las interfaces del objeto de sesión, la conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pasa a estar disponible para otro objeto de sesión creado en el origen de datos.  
  
 Un objeto de sesión adicional creado en el origen de datos establece su propia conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tal como especifica el origen de datos. La conexión a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quita cuando la aplicación libera todas las referencias a los objetos creados en dicha sesión.  
  
 En el ejemplo siguiente se muestra cómo utilizar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client para conectarse a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos:  
  
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
    if (FAILED(CoCreateInstance(CLSID_SQLNCLI10, NULL,  
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
  
 La conexión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de los objetos de sesión del proveedor de OLE DB Native Client a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede generar una sobrecarga significativa para las aplicaciones que crean y liberan continuamente objetos de sesión. La sobrecarga se puede minimizar mediante la administración [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eficaz de los objetos de sesión del proveedor OLE DB Native Client. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Las aplicaciones de proveedor de OLE DB de Native Client pueden mantener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa la conexión de un objeto de sesión manteniendo una referencia en al menos una interfaz del objeto.  
  
 Si se mantiene un grupo de referencias a objeto de creación de comando, por ejemplo, se mantienen conexiones activas para estos objetos de sesión en el grupo. Como los objetos de sesión son necesarios, el código de mantenimiento de grupo pasa un puntero de interfaz **IDBCreateCommand** válido al método de aplicación que requiere la sesión. Cuando el método de aplicación ya no requiere la sesión, devuelve el puntero de interfaz al código de mantenimiento de grupo en lugar de liberar la referencia de la aplicación al objeto de creación de comando.  
  
> [!NOTE]  
>  En el ejemplo anterior, se usa la interfaz **IDBCreateCommand** porque la interfaz **ICommand** implementa el método **GetDBSession**, el único método en el ámbito de comando o de conjunto de filas que permite a un objeto determinar la sesión en la que se ha creado. Por tanto, un objeto de comando, y solo un objeto de comando, permite a una aplicación recuperar un puntero de objeto de origen de datos a partir del cual se pueden crear sesiones adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Objetos de origen de datos &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
