---
title: Realización de operaciones asincrónicas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d3bd1ee2baf56a92068d58fffd783cd492609c71
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420494"
---
# <a name="performing-asynchronous-operations"></a>Realizar operaciones asincrónicas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite a las aplicaciones realizar operaciones de base de datos asincrónicas. El procesamiento asincrónico permite a los métodos devolver resultados inmediatamente sin bloquear el subproceso que hace la llamada. Esto hace posible gran parte de la potencia y la flexibilidad del subprocesamiento múltiple, sin que el programador tenga que crear explícitamente subprocesos o administrar la sincronización. Las aplicaciones solicitan el procesamiento asincrónico al inicializar una conexión a la base de datos, o al inicializar el resultado de la ejecución de un comando.  
  
## <a name="opening-and-closing-a-database-connection"></a>Abrir y cerrar una conexión a la base de datos  
 Cuando se usa el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, las aplicaciones diseñadas para inicializar un objeto de origen de datos de forma asincrónica pueden establecer el bit DBPROPVAL_ASYNCH_INITIALIZE en la propiedad DBPROP_INIT_ASYNCH antes de llamar a  **IDBInitialize:: Initialize**. Cuando se establece esta propiedad, el proveedor devuelve inmediatamente de la llamada a **inicializar** con S_OK si se ha completado la operación inmediatamente, o DB_S_ASYNCHRONOUS si la inicialización continúa de forma asincrónica. Las aplicaciones pueden consultar para la **IDBAsynchStatus** o [ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)interfaz en el objeto de origen de datos y, a continuación, llame a **idbasynchstatus:: GetStatus** o[ Issasynchstatus:: Waitforasynchcompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) para obtener el estado de la inicialización.  
  
 Además, se ha agregado la propiedad SSPROP_ISSAsynchStatus al conjunto de propiedades DBPROPSET_SQLSERVERROWSET. Los proveedores que admiten el **ISSAsynchStatus** interfaz debe implementar esta propiedad con un valor de VARIANT_TRUE.  
  
 **Idbasynchstatus:: Abort** o [issasynchstatus:: Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) se puede llamar para cancelar la asincrónica **inicializar** llamar. El consumidor debe solicitar explícitamente la inicialización de origen de datos asincrónica. En caso contrario, **IDBInitialize:: Initialize** no vuelve hasta que se inicialice completamente el objeto de origen de datos.  
  
> [!NOTE]  
>  Objetos de origen de datos utilizados para la agrupación de conexiones no pueden llamar a la **ISSAsynchStatus** interfaz en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB. El **ISSAsynchStatus** no se expone la interfaz de objetos de origen de datos agrupados.  
>   
>  Si una aplicación obliga explícitamente el uso del motor de cursor, **IOpenRowset:: OpenRowset** y **IMultipleResults:: GetResult** no será compatible con el procesamiento asincrónico.  
>   
>  Además, no se puede llamar la dll de proxy/código auxiliar de comunicación remota (en MDAC 2.8) el **ISSAsynchStatus** en la interfaz [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. El **ISSAsynchStatus** interfaz no se expone a través de comunicación remota.  
>   
>  Componentes de servicio no admiten **ISSAsynchStatus**.  
  
## <a name="execution-and-rowset-initialization"></a>Ejecución e inicialización de conjuntos de filas  
 Las aplicaciones diseñadas para abrir de forma asincrónica el resultado de la ejecución de un comando pueden establecer el bit DBPROPVAL_ASYNCH_INITIALIZE en la propiedad DBPROP_ROWSET_ASYNCH. Al establecer este bit antes de llamar a **IDBInitialize:: Initialize**, **ICommand:: Execute**, **IOpenRowset:: OpenRowset** o **IMultipleResults:: GetResult**, *riid* argumento debe establecerse en IID_IDBAsynchStatus, IID_ISSAsynchStatus o IID_IUnknown.  
  
 El método devuelve inmediatamente S_OK si se completa la inicialización del conjunto de filas inmediatamente, o DB_S_ASYNCHRONOUS si el conjunto de filas sigue inicializándose de forma asincrónica, con *ppRowset* establecer a la interfaz solicitada en el conjunto de filas. Para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, esta interfaz solo puede ser **IDBAsynchStatus** o **ISSAsynchStatus**. Hasta que el conjunto de filas está completamente inicializado, esta interfaz se comporta como si estuviera en un estado suspendido y llamar al método **QueryInterface** para interfaces distintas de **IID_IDBAsynchStatus** o **IID_ ISSAsynchStatus** pueden devolver E_NOINTERFACE. A menos que el consumidor solicite explícitamente el procesamiento asincrónico, el conjunto de filas se inicializa de forma sincrónica. Todas las interfaces solicitadas están disponibles cuando **idbasynchstaus:: GetStatus** o **issasynchstatus:: Waitforasynchcompletion** devuelve la indicación de que la operación asincrónica está completa. Esto no significa necesariamente que el conjunto de filas esté totalmente rellenado, pero está completo y es totalmente funcional.  
  
 Si el comando ejecutado no devuelve un conjunto de filas, sigue devolviendo inmediatamente con un objeto que admite **IDBAsynchStatus**.  
  
 Si necesita recibir varios resultados de la ejecución de comandos asincrónica, debe hacer lo siguiente:  
  
-   Establezca el bit DBPROPVAL_ASYNCH_INITIALIZE de la propiedad DBPROP_ROWSET_ASYNCH antes de ejecutar el comando.  
  
-   Llame a **ICommand:: Execute**y solicitud **IMultipleResults**.  
  
 El **IDBAsynchStatus** y **ISSAsynchStatus** interfaces, a continuación, pueden obtenerse consultando la interfaz de resultados múltiples con **QueryInterface**.  
  
 Cuando el comando ha terminado de ejecutarse, **IMultipleResults** puede usarse como normal, con una excepción en el caso sincrónico: se puede devolver DB_S_ASYNCHRONOUS, en cuyo caso **IDBAsynchStatus** o **ISSAsynchStatus** puede usarse para determinar cuándo se completa la operación.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, la aplicación llama a un método de no bloqueo, realiza algún otro procesamiento y, después, vuelve a procesar los resultados. **Issasynchstatus:: Waitforasynchcompletion** espera en el objeto de evento interno hasta que se realiza la operación de ejecución asincrónica o la cantidad de tiempo especificado por *dwMilisecTimeOut* se pasa.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **Issasynchstatus:: Waitforasynchcompletion** espera en el objeto de evento interno hasta que se realiza la operación de ejecución asincrónica o el *dwMilisecTimeOut* valor se pasa.  
  
 En el ejemplo siguiente se muestra el procesamiento asincrónico con varios conjuntos de resultados:  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 Para evitar bloqueos, el cliente puede comprobar el estado de una operación asincrónica en ejecución, como en el ejemplo siguiente:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 El ejemplo siguiente muestra cómo puede cancelar la operación asincrónica que se está ejecutando en este momento:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Propiedades y comportamientos de conjuntos de filas](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
