---
title: Información de Interfaces de Error | Documentos de Microsoft
description: Información de interfaces de error
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 4f79c469f40c778342e1093df0386acee80890de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server informa de cierta información de error y de estado en las interfaces de error definido por OLE DB **IErrorInfo**, **IErrorRecords**, y **ISQLErrorInfo**.  
  
 El controlador OLE DB para SQL Server admite **IErrorInfo** funciones miembro como se indica a continuación.  
  
|Función de miembro|Description|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No compatible. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "OLE DB de Microsoft Driver for SQL Server".|  
  
 El controlador OLE DB para SQL Server admite disponibles para el consumidor **IErrorRecords** funciones miembro como se indica a continuación.  
  
|Función de miembro|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en interfaces **ISQLErrorInfo,** y [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Devuelve una referencia en un **IErrorInfo** interfaz.|  
|**GetErrorParameters**|El controlador OLE DB para SQL Server no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El controlador OLE DB para SQL Server admite **ISQLErrorInfo:: GetSQLInfo** parámetros tal y como se indica a continuación.  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni el controlador OLE DB para SQL Server definido por los valores de SQLSTATE específico de la implementación.|  
|*plNativeError*|Devuelve el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] número de error de **master.dbo.sysmessages** cuando esté disponible. Errores nativos están disponibles después de un intento correcto de inicializar un controlador OLE DB para el origen de datos de SQL Server. Antes del intento, el controlador OLE DB para SQL Server siempre devuelve cero.|  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
