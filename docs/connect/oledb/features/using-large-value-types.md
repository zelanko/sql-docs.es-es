---
title: Uso de tipos de valor grande | Documentos de Microsoft
description: Utilizar tipos de valor grande con controlador OLE DB para SQL Server
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
- large value data types
- MSOLEDBSQL, large value types
- OLE DB Driver for SQL Server, large value types
- data access [OLE DB Driver for SQL Server], large value types
- OLE DB Driver for SQL Server, large value data types
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e41b35c8ea552708aa53f3cb8810bbaae06ca680
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612100"
---
# <a name="using-large-value-types"></a>Usar tipos de valor grande
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], trabajar con tipos de datos de valores grandes requería un tratamiento especial. Tipos de datos de valores grandes son los tipos que superan el tamaño máximo de fila de 8 KB. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujo un **max** especificador para **varchar**, **nvarchar**, y **varbinary** tipos de datos para permitir el almacenamiento de valores tan grandes como 2 ^ 31 -1 bytes. Columnas de la tabla y [!INCLUDE[tsql](../../../includes/tsql-md.md)] pueden especificar variables **varchar (max)**, **nvarchar (max)**, o **varbinary (max)** tipos de datos.  
  
> [!NOTE]  
>  Tipos de datos de valores grandes pueden tener un tamaño máximo entre 1 KB y 8 KB, o puede especificarse como ilimitados.  
  
 Anteriormente, solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos como **texto**, **ntext** y **imagen** podían alcanzar tales longitudes. El **max** especificador para **varchar**, **nvarchar**, y **varbinary** realizado estos tipos de datos redundantes. Sin embargo, dado que los tipos de datos long siguen estando disponibles, la mayoría de las interfaces para los componentes de acceso a datos de OLE DB seguirá siendo el mismo. Por motivos de compatibilidad con versiones anteriores, la marca DBCOLUMNFLAGS_ISLONG en el controlador OLE DB para SQL Server se mantiene en uso. Los proveedores y controladores escritos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y versiones posteriores siguen utilizando estos términos para los tipos nuevos cuando se establecen en una longitud máxima ilimitada.  
  
> [!NOTE]  
>  También puede especificar **varchar (max)**, **nvarchar (max)**, y **varbinary (max)** tipos de valor devuelto de tipos de datos como tipos de parámetro de entrada y salida de procedimientos almacenados, función , o bien en [CAST y CONVERT](../../../t-sql/functions/cast-and-convert-transact-sql.md) funciones.  
  
> [!NOTE]  
>  Si va a replicar datos, debe configurar el [máximo de la opción de configuración de servidor de text repl size](../../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md) en -1.  
  
## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server 
 El controlador OLE DB para SQL Server expone la **varchar (max)**, **varbinary (max)**, y **nvarchar (max)** tipos como DBTYPE_STR, DBTYPE_BYTES y DBTYPE_WSTR, respectivamente .  
  
 Los tipos de datos **varchar (max)**, **varbinary (max)**, y **nvarchar (max)** en columnas con el **max** son de tamaño establecido en ilimitado representado como un ISLONG mediante el núcleo de conjuntos de filas de esquema de OLE DB y las interfaces que devuelven tipos de datos de columna.  
  
 El objeto de comando **IAccessor** ha modificado la implementación para permitir el enlace como DBTYPE_IUNKNOWN. Si el consumidor especifica DBTYPE_IUNKNOWN y establece *pObject* en null, el proveedor devolverá la **ISequentialStream** interfaz al consumidor para que éste pueda transmitir **varchar ( max)**, **nvarchar (max)**, o **varbinary (max)** datos fuera de variables de salida.  
  
 Los valores de los parámetros de salida transmitidos se devuelven después de las filas de resultados. Si la aplicación intenta avanzar al siguiente conjunto mediante una llamada de resultados **IMultipleResults:: GetResult** sin consumir todos los valores de parámetro de salida devuelto, se devolverá DB_E_OBJECTOPEN.  
  
 Para admitir la transmisión por secuencias, el controlador OLE DB para SQL Server requiere parámetros de longitud variable que se tenga acceso en orden secuencial. Esto significa que DBPROP_ACCESSORDER debe establecerse en DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS o DBPROPVAL_AO_SEQUENTIAL cada vez que **varchar (max)**, **nvarchchar (max)**, o  **varbinary (max)** columnas o parámetros de salida se enlazan a DBTYPE_IUNKNOWN. Las llamadas a **IRowset:: GetData** se producirá un error con DBSTATUS_E_UNAVAILABLE si no se cumple esta restricción de orden de acceso. Esta restricción no se aplica cuando no se realizan enlaces de salida mediante DBTYPE_IUNKNOWN.  
  
 El controlador OLE DB para SQL Server también admite el enlace de parámetros de salida como DBTYPE_IUNKNOWN para tipos de datos de valor grande facilitar los escenarios donde un procedimiento almacenado devuelve tipos de valores grandes como valores devueltos que se exponen como DBTYPE_IUNKNOWN al cliente.  
  
 Para trabajar con estos tipos, una aplicación dispone de las opciones siguientes:  
  
-   Enlazar como un tipo que incluye enlaces compatibles con el tipo base de la columna (por ejemplo, para nvarchar (max), enlazar como un tipo que puede enlazarse a nvarchar). Si el búfer no es grande suficientemente se producirá un truncamiento, exactamente igual que en el tipo base, pero que ahora están disponibles los valores mayores.  
  
-   Enlace como un tipo que incluye conversiones compatibles con el tipo base de la columna y también especificación de DBTYPE_BYREF.  
  
-   Enlazar como DBTYPE_IUNKNOWN y usar la transmisión por secuencias.  
  
 Al notificar el tamaño máximo de una columna, se notificarán el controlador OLE DB para SQL Server:  
  
-   El tamaño máximo definido, que, por ejemplo, es 2000 para una **varchar (** 2000 **)** columna, o  
  
-   El valor "ilimitado" que en el caso de un **varchar (max)** columna es igual a ~ 0. Este valor se establece para la propiedad de metadatos DBCOLUMN_COLUMNSIZE.  
  
 Se aplicarán las reglas de conversión estándar a un **varchar (max)** columna, lo que significa que cualquier conversión que sea válido para un **varchar (** 2000 **)** columna también será válida para un **varchar (max)** columna. Lo mismo puede decirse de **nvarchar (max)** y **varbinary (max)** columnas.  
  
 A la hora de recuperar tipos de valor grande, el enfoque más eficaz consiste en enlazar como DBTYPE_IUNKNOWN y establecer la propiedad DBPROP_ACCESSORDER del conjunto de filas en DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS. Esto hará que el valor se transmita directamente desde la red sin almacenarse en el búfer intermedio, como en el ejemplo siguiente:  
  
```  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
#define OLEDBVER 0x0250  // To include the correct interfaces.  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <iostream>  
  
using std::cout;  
using std::endl;  
  
#include <windows.h>  
  
#include <oledb.h>  
#include "msoledbsql.h"  
#include <oledberr.h>  
  
#define CHKHR_GOTO(hr, errMsg, Label) \  
   if (FAILED(hr)) \  
   { \  
      cout << errMsg << endl; \  
      goto Label; \  
   }  
  
#define MAX_COL_SIZE 8000  
  
// ROUNDUP on all platforms pointers must be aligned properly.  
#define ROUNDUP_AMOUNT 8  
#define ROUNDUP_(size,amount) (((ULONG)(size)+((amount)-1))&~((amount)-1))  
#define ROUNDUP(size) ROUNDUP_(size, ROUNDUP_AMOUNT)  
  
HRESULT InitializeAndEstablishConnection(IDBInitialize** ppIDBInitialize);  
void UnInitializeConnection(IDBInitialize* pIDBInitialize);  
HRESULT CreateAndSetCommand(IDBInitialize* pIDBInitialize, ICommandText** ppICommandText);  
HRESULT ProcessResultSet(IRowset* pIRowset);  
  
void DisplayTime()  
{  
   SYSTEMTIME st;  
   GetSystemTime(&st);  
   cout<< st.wHour << ":" << st.wMinute << ":" << st.wSecond << "." << st.wMilliseconds << endl;  
}  
  
void main()  
{  
   HRESULT hr;  
   IDBInitialize* pIDBInitialize = NULL;  
   ICommandText* pICommandText = NULL;  
   IMultipleResults* pIMultipleResults = NULL;  
   IRowset* pIRowset = NULL;  
  
   hr = InitializeAndEstablishConnection(&pIDBInitialize);  
   CHKHR_GOTO(hr, L"Failed to establish connection.", _ExitMain);  
  
   hr = CreateAndSetCommand(pIDBInitialize, &pICommandText);  
   CHKHR_GOTO(hr, L"Failed to set up command object.", _ExitMain);  
  
   DisplayTime();  
  
   hr = pICommandText->Execute(NULL,   
      IID_IMultipleResults,   
      NULL,   
      NULL,   
     (IUnknown **) &pIMultipleResults);  
  
   CHKHR_GOTO(hr, L"Failed to execute command.", _ExitMain);  
  
   while (1)  
   {  
      hr = pIMultipleResults->GetResult(  
         NULL,   
         DBRESULTFLAG_DEFAULT,   
         IID_IRowset,   
         NULL,   
         (IUnknown**)&pIRowset);  
  
   CHKHR_GOTO(hr, L"Failed to obtain a results from MR object.", _ExitMain);  
  
   if (hr == DB_S_NORESULT)  
      break;  
  
      if (pIRowset)  
      {  
         hr = ProcessResultSet(pIRowset);   
         CHKHR_GOTO(hr, L"Failed to process the current Rowset.", _ExitMain);  
  
         pIRowset->Release();  
         pIRowset = NULL;  
      }  
   }  
  
   DisplayTime();  
  
_ExitMain:  
  
   if (pIRowset)  
   {  
      pIRowset->Release();  
      pIRowset = NULL;  
   }  
  
   if (pIMultipleResults)  
   {  
      pIMultipleResults->Release();  
      pIMultipleResults = NULL;  
   }  
  
   if (pICommandText)  
   {  
      pICommandText->Release();  
      pICommandText = NULL;  
   }  
  
   UnInitializeConnection(pIDBInitialize);  
   return;  
};  
  
HRESULT InitializeAndEstablishConnection(IDBInitialize** ppIDBInitialize)  
{  
   HRESULT hr;  
   IDBInitialize* pIDBInitialize = NULL;  
   IDBProperties* pIDBProperties = NULL;  
  
   const int NUM_DBINIT_PROPS = 3;  
   const wchar_t* const g_wszServer = L".";  
   const wchar_t* const g_wszCatalog = L"AdventureWorks";  
   const wchar_t* const g_wszSecurity = L"SSPI";  
  
   DBPROPSET rgdbPropSetInit[1];  
   DBPROP rgdbPropInit [NUM_DBINIT_PROPS];  
  
   *ppIDBInitialize = NULL;  
   hr = CoInitialize(NULL);  
   CHKHR_GOTO(hr, L"Failed to initialize COM.", _ExitInitialize);  
  
   hr = CoCreateInstance(CLSID_MSOLEDBSQL,   
      NULL,   
      CLSCTX_INPROC_SERVER,  
      IID_IDBInitialize,   
      (void**)&pIDBInitialize);  
  
   CHKHR_GOTO(hr, L"Failed to create MSOLEDBSQL DataSource object.", _ExitInitialize);  
  
   for(int idxProp = 0; idxProp < NUM_DBINIT_PROPS; idxProp++)   
   {  
      VariantInit(&rgdbPropInit[idxProp].vValue);  
   }  
  
   rgdbPropInit[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   rgdbPropInit[0].vValue.vt = VT_BSTR;  
   rgdbPropInit[0].vValue.bstrVal= SysAllocString(g_wszServer);  
   rgdbPropInit[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgdbPropInit[0].colid = DB_NULLID;  
  
   if (rgdbPropInit[0].vValue.bstrVal == NULL)  
   {  
      hr = E_OUTOFMEMORY;  
      goto _ExitInitialize;  
   }  
  
   rgdbPropInit[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   rgdbPropInit[1].vValue.vt = VT_BSTR;  
   rgdbPropInit[1].vValue.bstrVal= SysAllocString(g_wszCatalog);  
   rgdbPropInit[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgdbPropInit[1].colid = DB_NULLID;  
  
   if (rgdbPropInit[1].vValue.bstrVal == NULL)  
   {  
      hr = E_OUTOFMEMORY;  
      goto _ExitInitialize;  
   }  
  
   rgdbPropInit[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   rgdbPropInit[2].vValue.vt = VT_BSTR;  
   rgdbPropInit[2].vValue.bstrVal= SysAllocString(g_wszSecurity);  
   rgdbPropInit[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgdbPropInit[2].colid = DB_NULLID;  
  
   if (rgdbPropInit[2].vValue.bstrVal == NULL)  
   {  
      hr = E_OUTOFMEMORY;  
      goto _ExitInitialize;  
   }  
  
   rgdbPropSetInit[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgdbPropSetInit[0].cProperties = NUM_DBINIT_PROPS;  
   rgdbPropSetInit[0].rgProperties = rgdbPropInit;  
  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   CHKHR_GOTO(hr, L"Failed to QI DataSource object for IDBProperties.", _ExitInitialize);  
  
   hr = pIDBProperties->SetProperties(1, rgdbPropSetInit);   
   CHKHR_GOTO(hr, L"Failed to set DataSource object Properties.", _ExitInitialize);  
  
   pIDBProperties->Release();  
   pIDBProperties = NULL;  
  
   hr = pIDBInitialize->Initialize();  
   CHKHR_GOTO(hr, L"Failed to establish connection with the server.", _ExitInitialize);  
  
_ExitInitialize:  
  
   if (pIDBProperties)  
   {  
      pIDBProperties->Release();  
      pIDBProperties = NULL;  
   }  
  
   if (FAILED(hr))  
   {  
      if (pIDBInitialize)  
      {  
         pIDBInitialize->Release();  
         pIDBInitialize = NULL;  
      }  
   }  
  
   *ppIDBInitialize = pIDBInitialize;  
   return hr;  
}  
  
void UnInitializeConnection(IDBInitialize* pIDBInitialize)  
{  
   if (pIDBInitialize)  
   {  
      pIDBInitialize->Uninitialize();  
      pIDBInitialize->Release();  
      pIDBInitialize = NULL;  
   }  
   CoUninitialize();  
}  
  
HRESULT CreateAndSetCommand(IDBInitialize* pIDBInitialize, ICommandText** ppICommandText)  
{  
   HRESULT hr;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
   ICommandText* pICommandText = NULL;  
   ICommandProperties* pICommandProperties = NULL;  
   DBPROPSET rgCmdPropSet[1];  
   DBPROP rgCmdProperties[1];  
  
const wchar_t* const g_wCmdString = L"declare @x xml, @y nvarchar(max); select @x = (SELECT * FROM Sales.SalesOrderHeader FOR XML AUTO); select @x;";  
  
   *ppICommandText = NULL;  
  
   if (!pIDBInitialize)  
   {  
      hr = E_FAIL;  
      goto _ExitCreateAndSetCommand;  
   }  
  
   hr = pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
   CHKHR_GOTO(hr, L"Failed to obtain IDBCreateSession interface from DSO.", _ExitCreateAndSetCommand);  
  
   hr = pIDBCreateSession->CreateSession(  
      NULL,   
      IID_IDBCreateCommand,   
      (IUnknown**) &pIDBCreateCommand);  
  
   CHKHR_GOTO(hr, L"Failed to Create a Session for command execution.", _ExitCreateAndSetCommand);  
  
   hr = pIDBCreateCommand->CreateCommand(  
      NULL,   
      IID_ICommandText,   
      (IUnknown**)&pICommandText);  
  
   CHKHR_GOTO(hr, L"Failed to Create a Command object.", _ExitCreateAndSetCommand);  
  
   hr = pICommandText->SetCommandText(DBGUID_DBSQL, g_wCmdString);  
   CHKHR_GOTO(hr, L"Failed to Set Command Text.", _ExitCreateAndSetCommand);  
  
   hr = pICommandText->QueryInterface(IID_ICommandProperties, (void**) &pICommandProperties);  
   CHKHR_GOTO(hr, L"Failed to obtain ICommandProperties interface from the command object.", _ExitCreateAndSetCommand);  
  
   rgCmdProperties[0].dwPropertyID = DBPROP_ACCESSORDER;  
   rgCmdProperties[0].vValue.vt = VT_I4;  
   rgCmdProperties[0].vValue.lVal = DBPROPVAL_AO_SEQUENTIAL;  
   rgCmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   rgCmdProperties[0].colid = DB_NULLID;  
  
   rgCmdPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
   rgCmdPropSet[0].cProperties = 1;  
   rgCmdPropSet[0].rgProperties = rgCmdProperties;  
  
   hr = pICommandProperties->SetProperties(1, rgCmdPropSet);   
   CHKHR_GOTO(hr, L"Failed to Set Command object Properties.", _ExitCreateAndSetCommand);  
  
_ExitCreateAndSetCommand:  
  
   if (pICommandProperties)  
   {  
      pICommandProperties->Release();  
      pICommandProperties = NULL;  
   }  
  
   if (pIDBCreateCommand)  
   {  
      pIDBCreateCommand->Release();  
      pIDBCreateCommand = NULL;  
   }  
  
   if (pIDBCreateSession)  
   {  
      pIDBCreateSession->Release();  
      pIDBCreateSession = NULL;  
   }  
  
   if (FAILED(hr))  
   {  
      if (pICommandText)  
      {  
         pICommandText->Release();  
         pICommandText = NULL;  
      }  
   }  
  
   *ppICommandText = pICommandText;  
   return hr;  
}  
  
HRESULT ProcessResultSet(IRowset* pIRowset)  
{  
   HRESULT hr;  
  
   IColumnsInfo* pIColumnsInfo = NULL;  
   DBCOLUMNINFO* pDBColumnInfo = NULL;  
   ULONG lNumCols = 0;  
   wchar_t* pStringsBuffer = NULL;  
  
   DBBINDING* pBindings = NULL;  
   DBOBJECT dbobj;  
   ULONG idxBinding;  
   IAccessor* pIAccessor = NULL;  
   HACCESSOR hAccessor = DB_NULL_HACCESSOR;  
   HROW hRows[1] = {DB_NULL_HROW};  
   HROW* pRow = &hRows[0];  
   BYTE* pBuffer = NULL;  
  
   ULONG lNumRowsRetrieved;  
   DBLENGTH dwOffset = 0;  
  
   hr = pIRowset->QueryInterface(IID_IColumnsInfo, (void **)&pIColumnsInfo);  
   CHKHR_GOTO(hr, L"Failed to QI Rowset for IColumnsInfo.", _ExitProcessResultSet);  
  
   hr = pIColumnsInfo->GetColumnInfo(&lNumCols, &pDBColumnInfo, &pStringsBuffer);  
   CHKHR_GOTO(hr, L"Failed to obtain Column Information.", _ExitProcessResultSet);  
  
   pBindings = new DBBINDING[lNumCols];  
  
   if (!pBindings)  
   {  
      hr = E_OUTOFMEMORY;  
      goto _ExitProcessResultSet;  
   }  
  
   memset(pBindings, 0, sizeof(DBBINDING) * lNumCols);  
  
   dbobj.dwFlags = STGM_READ;  
   dbobj.iid = IID_ISequentialStream;  
  
   for (idxBinding = 0; idxBinding < lNumCols; idxBinding++)   
   {  
      pBindings[idxBinding].iOrdinal = idxBinding + 1;  
      pBindings[idxBinding].obStatus = dwOffset;  
      pBindings[idxBinding].obLength = dwOffset + sizeof(DBSTATUS);  
      pBindings[idxBinding].obValue = dwOffset + sizeof(DBSTATUS) + sizeof(DBLENGTH);  
  
      pBindings[idxBinding].pTypeInfo = NULL;  
      pBindings[idxBinding].pBindExt = NULL;  
      pBindings[idxBinding].dwPart = DBPART_VALUE | DBPART_LENGTH | DBPART_STATUS;  
      pBindings[idxBinding].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
      pBindings[idxBinding].eParamIO = DBPARAMIO_NOTPARAM;  
      pBindings[idxBinding].bPrecision = pDBColumnInfo[idxBinding].bPrecision;  
      pBindings[idxBinding].bScale = pDBColumnInfo[idxBinding].bScale;  
  
      pBindings[idxBinding].cbMaxLen = 0;  
      pBindings[idxBinding].wType = DBTYPE_WSTR;  
  
   // Determine the maximum number of bytes required in our buffer to  
   // contain the Unicode string representation of the provider's native  
   // data type, including room for the NULL-termination character  
   switch( pDBColumnInfo[idxBinding].wType )  
   {  
      case DBTYPE_NULL:  
      case DBTYPE_EMPTY:  
      case DBTYPE_I1:  
      case DBTYPE_I2:  
      case DBTYPE_I4:  
      case DBTYPE_UI1:  
      case DBTYPE_UI2:  
      case DBTYPE_UI4:  
      case DBTYPE_R4:  
      case DBTYPE_BOOL:  
      case DBTYPE_I8:  
      case DBTYPE_UI8:  
      case DBTYPE_R8:  
      case DBTYPE_CY:  
      case DBTYPE_ERROR:  
      // When the above types are converted to a string, they  
      // will all fit into 25 characters, so use that plus space  
      // for the NULL-terminator.  
  
      pBindings[idxBinding].cbMaxLen = (25 + 1) * sizeof(WCHAR);  
      break;  
  
      case DBTYPE_DECIMAL:  
      case DBTYPE_NUMERIC:  
      case DBTYPE_DATE:  
      case DBTYPE_DBDATE:  
      case DBTYPE_DBTIMESTAMP:  
      case DBTYPE_GUID:  
      // Converted to a string, the above types will all fit into  
      // 50 characters, so use that plus space for the terminator.  
  
      pBindings[idxBinding].cbMaxLen = (50 + 1) * sizeof(WCHAR);  
      break;  
  
      case DBTYPE_BYTES:  
      // In converting DBTYPE_BYTES to a string, each byte  
      // becomes two characters (e.g. 0xFF -> "FF"), so we  
      // will use double the maximum size of the column plus  
      // include space for the NULL-terminator.  
  
      pBindings[idxBinding].cbMaxLen = (pDBColumnInfo[idxBinding].ulColumnSize * 2 + 1) * sizeof(WCHAR);  
      break;  
  
      case DBTYPE_STR:  
      case DBTYPE_WSTR:  
      case DBTYPE_BSTR:  
      // Going from a string to our string representation,  
      // we can just take the maximum size of the column,  
      // a count of characters, and include space for the  
      // terminator, which is not included in the column size.  
  
      pBindings[idxBinding].cbMaxLen = (pDBColumnInfo[idxBinding].ulColumnSize + 1) * sizeof(WCHAR);  
      break;  
  
      default:  
      // For any other type, we will simply use our maximum  
      // column buffer size, since the display size of these  
      // columns may be variable (e.g. DBTYPE_VARIANT) or  
      // unknown (e.g. provider-specific types).  
      pBindings[idxBinding].cbMaxLen = MAX_COL_SIZE;  
      break;  
   }  
  
   // If the provider's native data type for this column is  
   // DBTYPE_IUNKNOWN or this is a BLOB column and the user  
   // has requested that we bind BLOB columns as ISequentialStream  
   // objects, bind this column as an ISequentialStream object if  
   // the provider supports our creating another ISequentialStream  
   // binding.  
   if(pDBColumnInfo[idxBinding].dwFlags & DBCOLUMNFLAGS_ISLONG)  
   {  
      pBindings[idxBinding].wType = DBTYPE_IUNKNOWN;  
  
      pBindings[idxBinding].cbMaxLen = sizeof(ISequentialStream*);  
  
      pBindings[idxBinding].pObject = (DBOBJECT *)CoTaskMemAlloc(sizeof(DBOBJECT));  
  
      if (!pBindings[idxBinding].pObject)  
      {  
         hr = E_OUTOFMEMORY;  
         goto _ExitProcessResultSet;  
      }  
  
      // Direct the provider to create an ISequentialStream  
      // object over the data for this column.  
      pBindings[idxBinding].pObject->iid = IID_ISequentialStream;  
  
      // We want read access on the ISequentialStream  
      // object that the provider will create for us  
      pBindings[idxBinding].pObject->dwFlags = STGM_READ;  
      }  
  
      // Ensure that the bound maximum length is no more than the  
      // maximum column size in bytes that we've defined.  
      pBindings[idxBinding].cbMaxLen = min(pBindings[idxBinding].cbMaxLen, MAX_COL_SIZE);  
  
      // Update the offset past the end of this column's data, so  
      // that the next column will begin in the correct place in  
      // the buffer.  
      dwOffset = pBindings[idxBinding].cbMaxLen + pBindings[idxBinding].obValue;  
  
      // Ensure that the data for the next column will be correctly  
      // aligned for all platforms, or, if we're done with columns,  
      // that if we allocate space for multiple rows that the data  
      // for every row is correctly aligned.  
      dwOffset = ROUNDUP(dwOffset);  
   }  
  
   hr = pIRowset->QueryInterface(IID_IAccessor, (void **) &pIAccessor);  
   CHKHR_GOTO(hr, L"Failed to obtain Accessor interface", _ExitProcessResultSet);  
  
   hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA,  
      lNumCols,  
      pBindings,  
      0,  
      &hAccessor,  
      NULL);  
  
   CHKHR_GOTO(hr, L"Failed to create Accessor", _ExitProcessResultSet);  
   for (idxBinding = 0; idxBinding < lNumCols; idxBinding++)   
   {  
      cout << pDBColumnInfo[idxBinding].pwszName << endl;  
   }  
  
   lNumRowsRetrieved = 0;  
  
   hr = pIRowset->GetNextRows(  
      NULL,  
      0,  
      1,  
      &lNumRowsRetrieved,  
      &pRow);  
  
   CHKHR_GOTO(hr, L"Failed to fetch a row from the rowset", _ExitProcessResultSet);  
  
   pBuffer = new BYTE[sizeof(DBSTATUS) + sizeof(DBLENGTH) + sizeof(IUnknown*)];  
  
   if (!pBuffer)  
   {  
      hr = E_OUTOFMEMORY;  
      goto _ExitProcessResultSet;  
   }  
  
   while(lNumRowsRetrieved && hr != DB_S_ENDOFROWSET)   
   {  
      memset(pBuffer, 0, sizeof(DBSTATUS) + sizeof(DBLENGTH) + sizeof(IUnknown*));  
  
      hr = pIRowset->GetData(hRows[0], hAccessor, pBuffer);  
      CHKHR_GOTO(hr, L"Failed to obtain row data", _ExitProcessResultSet);  
  
      for (idxBinding = 0; idxBinding < lNumCols; idxBinding++)  
      {  
         if (pBindings[idxBinding].wType == DBTYPE_IUNKNOWN)  
         {  
            BYTE pbBuff[3000];  
            ULONG cbNeeded = sizeof(pbBuff)/sizeof(BYTE);  
            ULONG cbRead;  
            ULONG cbReadTotal = 0;  
            ISequentialStream* pISequentialStream = NULL;  
  
            IUnknown* pIUnknown = *((IUnknown**)(pBuffer + pBindings[idxBinding].obValue));  
            pIUnknown->QueryInterface(IID_ISequentialStream, (void**)&pISequentialStream);  
  
            do  
            {  
               hr = pISequentialStream->Read(pbBuff, cbNeeded, &cbRead);  
               cbReadTotal += cbRead;  
            }  
            while (SUCCEEDED(hr) && hr != S_FALSE && cbRead == cbNeeded);  
  
               cout << "Total Bytes Read: " << cbReadTotal << endl;  
  
               pISequentialStream->Release();  
               pISequentialStream = NULL;  
               pIUnknown->Release();  
               pIUnknown = NULL;  
            }  
         }  
  
         pIRowset->ReleaseRows(1, pRow, NULL, NULL, NULL);  
  
         hr = pIRowset->GetNextRows(NULL,  
            0,  
            1,  
            &lNumRowsRetrieved,  
            &pRow);  
  
         CHKHR_GOTO(hr, L"Failed to fetch a row from the rowset.", _ExitProcessResultSet);  
   }  
  
_ExitProcessResultSet:  
  
   pIRowset->ReleaseRows(1, pRow, NULL, NULL, NULL);  
   delete [] pBuffer;  
  
   if (pIAccessor)  
   {  
      if (hAccessor != DB_NULL_HACCESSOR)  
      {  
         pIAccessor->ReleaseAccessor(hAccessor, NULL);  
      }  
  
      pIAccessor->Release();  
      pIAccessor = NULL;  
   }  
  
   if (pBindings)  
   {  
      for (idxBinding = 0; idxBinding < lNumCols; idxBinding++)  
      {  
         if (pBindings[idxBinding].pObject)  
         CoTaskMemFree(pBindings[idxBinding].pObject);  
      }  
   }  
  
   delete [] pBindings;  
  
   CoTaskMemFree(pDBColumnInfo);  
   CoTaskMemFree(pStringsBuffer);  
  
   if (pIColumnsInfo)  
   {  
      pIColumnsInfo->Release();  
      pIColumnsInfo = NULL;  
   }  
  
   return hr;  
}  
```  
  
 Para obtener más información acerca de cómo el controlador OLE DB para SQL Server expone los tipos de datos de valor grande, consulte [objetos BLOB y OLE](../../oledb/ole-db-blobs/blobs-and-ole-objects.md).  

  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
