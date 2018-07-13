---
title: Información en Interfaces de Error | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a121dc2e94c67637e867398bfa40c7fe230cd411
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419024"
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client notifica alguna información de error y de estado en las interfaces de error definido por OLE DB **IErrorInfo**, **IErrorRecords**, y **ISQLErrorInfo** .  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el proveedor OLE DB de Native Client **IErrorInfo** funciones miembro como sigue.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No compatible. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "Microsoft SQL Server Native Client".|  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite disponibles para el consumidor **IErrorRecords** funciones miembro como sigue.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en las interfaces **ISQLErrorInfo,** y [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md).|  
|**GetErrorInfo**|Devuelve una referencia en un **IErrorInfo** interfaz.|  
|**GetErrorParameters**|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el proveedor OLE DB de Native Client **ISQLErrorInfo:: GetSQLInfo** parámetros como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define valores SQLSTATE específicos de la implementación.|  
|*plNativeError*|Devuelve el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] número de error **master.dbo.sysmessages** cuando esté disponible. Errores nativos están disponibles después de un intento correcto para inicializar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] origen de datos del proveedor OLE DB de Native Client. Antes del intento, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client siempre devuelve cero.|  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)  
  
  
