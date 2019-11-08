---
title: Información en interfaces de error | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 256c11c46d24998808821002d3a63bbc17c40931
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73769464"
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client notifica información de error y de estado en las interfaces de error definidas por OLE DB **IErrorInfo**, **IErrorRecords**y **ISQLErrorInfo**.  
  
 El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite las funciones miembro de **IErrorInfo** como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No compatible. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "Microsoft SQL Server Native Client".|  
  
 El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es compatible con las funciones miembro de **IErrorRecords** disponibles para el consumidor como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en las interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Devuelve una referencia en una interfaz **IErrorInfo**.|  
|**GetErrorParameters**|El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite los parámetros **ISQLErrorInfo:: GetSQLInfo** como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definen los valores SQLSTATE específicos de la implementación.|  
|*plNativeError*|Devuelve el número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedente de **master.dbo.sysmessages** cuando está disponible. Los errores nativos están disponibles después de un intento correcto de inicializar un origen de datos del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB. Antes del intento, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client siempre devuelve cero.|  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
