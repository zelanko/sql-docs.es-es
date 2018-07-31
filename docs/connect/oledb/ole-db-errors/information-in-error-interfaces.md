---
title: Información en Interfaces de Error | Microsoft Docs
description: Información en interfaces de error
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 3f5b9334beae9c3a65c290adffae1075788191c4
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39106031"
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server notifica alguna información de error y estado en las interfaces de error definidas por OLE DB **IErrorInfo**, **IErrorRecords** e **ISQLErrorInfo**.  
  
 El controlador OLE DB para SQL Server admite **IErrorInfo** funciones miembro como sigue.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No compatible. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "Controlador Microsoft OLE DB para SQL Server".|  
  
 El controlador OLE DB para SQL Server admite disponibles para el consumidor **IErrorRecords** funciones miembro como sigue.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en las interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Devuelve una referencia en una interfaz **IErrorInfo**.|  
|**GetErrorParameters**|El controlador OLE DB para SQL Server no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El controlador OLE DB para SQL Server admite **ISQLErrorInfo:: GetSQLInfo** parámetros como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni el controlador OLE DB para SQL Server se definen valores SQLSTATE específicos de la implementación.|  
|*plNativeError*|Devuelve el número de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procedente de **master.dbo.sysmessages** cuando está disponible. Errores nativos están disponibles después de un intento correcto para inicializar un controlador de OLE DB para el origen de datos de SQL Server. Antes del intento, el controlador OLE DB para SQL Server siempre devuelve cero.|  
  
## <a name="see-also"></a>Ver también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
