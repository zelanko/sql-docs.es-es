---
description: Función LocalDBGetVersions
title: Función LocalDBGetVersions | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBGetVersions
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 033a9c6b-0d7f-4f8a-ab60-33cd6fee0d33
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb1202b625b0cd990ce0c336821c0765de643787
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544055"
---
# <a name="localdbgetversions-function"></a>Función LocalDBGetVersions
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Devuelve todas las versiones de SQL Server Express LocalDB disponibles en el equipo.  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
#define MAX_LOCALDB_VERSION_LENGTH 43typedef WCHAR TLocalDBVersion[MAX_LOCALDB_VERSION_LENGTH + 1];typedef TLocalDBVersion* PTLocalDBVersion;HRESULT LocalDBGetVersions(           PTLocalDBVersion pVersion,           LPDWORD lpdwNumberOfVersions);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pVersionNames*  
 Genere Contiene los nombres de las versiones de LocalDB que están disponibles en la estación de trabajo del usuario.  
  
 *lpdwNumberOfVersions*  
 [Input/Output] En la entrada, contiene el número de zonas para las versiones en el búfer de *pVersionNames* .   
En salida, contiene el número de versiones de LocalDB existentes.  
  
## <a name="returns"></a>Devoluciones  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 El búfer de entrada es demasiado corto y no se ha solicitado truncamiento.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Se ha producido un error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Observaciones  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
