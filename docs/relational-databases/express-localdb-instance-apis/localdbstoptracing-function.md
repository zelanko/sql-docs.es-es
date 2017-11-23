---
title: "Función LocalDBStopTracing | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: LocalDBStopTracing
apilocation: sqluserinstance.dll
apitype: DLLExport
ms.assetid: 1d50e040-8602-4ffa-be8f-b8633fdfa7ff
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e1a7234f5eef5349cb9843321c27412bedecd2a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="localdbstoptracing-function"></a>Función LocalDBStopTracing
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Deshabilita el seguimiento de API de llamadas para todas las instancias de SQL Server Express LocalDB pertenecen al usuario de Windows actual.  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT LocalDBStopTracing();  
```  
  
## <a name="returns"></a>Devuelve  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
