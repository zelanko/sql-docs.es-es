---
title: Información en interfaces de error | Microsoft Docs
description: Información en interfaces de error
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ff18864e37575f78d129abb1569b0ffe83d4685
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994934"
---
# <a name="information-in-error-interfaces"></a>Información en interfaces de error
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El controlador OLE DB para SQL Server notifica alguna información de error y estado en las interfaces de error definidas por OLE DB **IErrorInfo**, **IErrorRecords** e **ISQLErrorInfo**.  
  
 El controlador de OLE DB para SQL Server admite las funciones miembro de **IErrorInfo** como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetDescription**|Cadena de mensaje de error descriptiva.|  
|**GetGUID**|GUID de la interfaz que definió el error.|  
|**GetHelpContext**|No compatible. Siempre devuelve cero.|  
|**GetHelpFile**|No compatible. Siempre devuelve NULL.|  
|**GetSource**|Cadena "Controlador Microsoft OLE DB para SQL Server".|  
  
 El controlador de OLE DB para SQL Server admite funciones miembro de **IErrorRecords** disponibles para el consumidor como se indica a continuación.  
  
|Función de miembro|Descripción|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Llena una estructura ERRORINFO con información básica acerca de un error. Una estructura ERRORINFO contiene miembros que identifican el valor devuelto HRESULT del error así como el proveedor y la interfaz a los que se aplica el error.|  
|**GetCustomErrorObject**|Devuelve una referencia en las interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Devuelve una referencia en una interfaz **IErrorInfo**.|  
|**GetErrorParameters**|El controlador de OLE DB para SQL Server no devuelve parámetros al consumidor a través de **GetErrorParameters**.|  
|**GetRecordCount**|Recuento de registros de error disponibles.|  
  
 El controlador de OLE DB para SQL Server admite los parámetros **ISQLErrorInfo:: GetSQLInfo** como se indica a continuación.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*pbstrSQLState*|Devuelve un valor SQLSTATE para el error. Los valores SQLSTATE se definen en las especificaciones SQL 92, ODBC e ISO SQL y API. Ni [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni el controlador de OLE DB para los valores SQLSTATE específicos de la implementación definidos por el SQL Server.|  
|*plNativeError*|Devuelve el número de error de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] procedente de **master.dbo.sysmessages** cuando está disponible. Los errores nativos están disponibles después de un intento correcto de inicializar un controlador de OLE DB para SQL Server origen de datos. Antes del intento, el controlador de OLE DB para SQL Server siempre devuelve cero.|  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
