---
title: Información en interfaces de error | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 460a0a2cf58d5980b1265db91d053e3088b55a99
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704985"
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client notifica información de error y de estado en las interfaces de error definidas por el OLE DB **IErrorInfo**, **IErrorRecords**y **ISQLErrorInfo**.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite las funciones miembro de **IErrorInfo** como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No se admite. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "Microsoft SQL Server Native Client".|  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client es compatible con las funciones miembro de **IErrorRecords** disponibles para el consumidor como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en las interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md).|  
|**GetErrorInfo**|Devuelve una referencia en una interfaz **IErrorInfo**.|  
|**GetErrorParameters**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite los parámetros **ISQLErrorInfo:: GetSQLInfo** como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client definen los valores SQLSTATE específicos de la implementación.|  
|*plNativeError*|Devuelve el número de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedente de **master.dbo.sysmessages** cuando está disponible. Los errores nativos están disponibles después de un intento correcto de inicializar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos del proveedor de OLE DB de Native Client. Antes del intento, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client siempre devuelve cero.|  
  
## <a name="see-also"></a>Consulte también  
 [Errores](errors.md)  
  
  
