---
title: Función LocalDBGetVersionInfo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: localdb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- LocalDBGetVersionInfo
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
caps.latest.revision: 10
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8be469a7f4a9f1b316b881ea884f7fbabc955dfb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32935090"
---
# <a name="localdbgetversioninfo-function"></a>Función LocalDBGetVersionInfo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Devuelve información de la versión de SQL Server Express LocalDB especificada, por ejemplo si existe y el número de versión completo de LocalDB (incluida la compilación y los números de versión).  
  
 La información se devuelve en forma de un **struct** denominado **LocalDBVersionInfo**, que tiene la siguiente definición.  
  
```  
typedef struct _LocalDBVersionInfo  
{  
      // Contains the size of the LocalDBVersionInfo struct  
      DWORD  cbLocalDBVersionInfoSize;  
  
      // Holds the version name  
      TLocalDBVersionwszVersion;  
  
      // TRUE if the instance files exist on disk, FALSE otherwise  
      BOOL   bExists;  
  
      // Holds the LocalDB version for the instance in the format: major.minor.build.revision  
      DWORD  dwMajor;  
      DWORD  dwMinor;  
      DWORD  dwBuild;  
      DWORD  dwRevision;  
} LocalDBVersionInfo;  
  
```  
  
 **Archivo de encabezado:** sqlncli.h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT LocalDBGetVersionInfo(  
           PCWSTR wszVersionName,           PLocalDBVersionInfo pVersionInfo,           DWORD dwVersionInfoSize);  
```  
  
## <a name="parameters"></a>Parámetros  
 *wszVersionName*  
 [Entrada] El nombre de versión de LocalDB.  
  
 *pVersionInfo*  
 [Output] El búfer en el que se almacena información sobre la versión de LocalDB.  
  
 *dwVersionInfoSize*  
 [Entrada] Contiene el tamaño de la *VersionInfo* búfer.  
  
## <a name="returns"></a>Devuelve  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 La versión de LocalDB especificada no existe.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="details"></a>Detalles  
 El análisis razonado respecto a la introducción de la **struct** argumento de tamaño (*lpVersionInfoSize*) consiste en permitir a la API que devuelva distintas versiones de la **LocalDBVersionInfostruct**, eficazmente habilitar la compatibilidad con versiones anteriores y posteriores.  
  
 Si el **struct** argumento de tamaño (*lpVersionInfoSize*) coincide con el tamaño de una versión conocida de la **LocalDBVersionInfostruct**, esa versión de la  **struct** se devuelve. De lo contrario, se devuelve LOCALDB_ERROR_INVALID_PARAMETER.  
  
 Un ejemplo típico de **LocalDBGetVersionInfo** uso de la API tiene el siguiente aspecto:  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L”11.0”, &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
