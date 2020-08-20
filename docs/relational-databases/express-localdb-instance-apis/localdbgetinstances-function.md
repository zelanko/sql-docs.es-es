---
description: Función LocalDBGetInstances
title: Función LocalDBGetInstances | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetInstances
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: f95a9980-8bc0-426c-8aa1-e2660b6784cf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: de9e71560a66fb376d6aab2a6e334173be311aca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486915"
---
# <a name="localdbgetinstances-function"></a>Función LocalDBGetInstances
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Devuelve todas las instancias de SQL Server Express LocalDB con la versión indicada.  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
#define MAX_LOCALDB_INSTANCE_NAME_LENGTH 128typedef WCHAR TLocalDBInstanceName[MAX_LOCALDB_INSTANCE_NAME_LENGTH + 1];typedef TLocalDBInstanceName* PTLocalDBInstanceName;  
HRESULT LocalDBGetInstances(  
           PTLocalDBInstanceName pInstanceNames,  
           LPDWORD lpdwNumberOfInstances  
);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pInstanceNames*  
 Genere Cuando esta función devuelve un valor, contiene los nombres de las instancias de LocalDB con nombre y predeterminadas en la estación de trabajo del usuario.  
  
 *lpdwNumberOfInstances*  
 [Entrada/Salida] En la entrada, contiene el número de zonas para los nombres de instancia en el búfer de *pInstanceNames* . En la salida, contiene el número de instancias de LocalDB que se encuentran en la estación de trabajo del usuario.  
  
## <a name="returns"></a>Devoluciones  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 El búfer de entrada es demasiado corto y no se ha solicitado truncamiento.  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 La ruta de acceso donde la instancia debe almacenarse es mayor que MAX_PATH.  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 No se puede tener acceso a un registro de la instancia.  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 Una configuración de instancia está dañada.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Se ha producido un error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Observaciones  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
