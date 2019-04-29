---
title: Función LocalDBGetVersionInfo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBGetVersionInfo
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: d4aaea30-1d0d-4436-bcdc-5c101d27b1c1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4350badedcaf2a4e2b977b57cf9e6cfde6c1b275
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032233"
---
# <a name="localdbgetversioninfo-function"></a>Función LocalDBGetVersionInfo
  Devuelve información de la versión de SQL Server Express LocalDB especificada, por ejemplo si existe y el número de versión completo de LocalDB (incluida la compilación y los números de versión).  
  
 La información se devuelve en forma de un `struct` denominado **LocalDBVersionInfo**, que tiene la siguiente definición.  
  
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
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../express-localdb-error-messages/localdb-error-unknown-version.md)  
 La versión de LocalDB especificada no existe.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="details"></a>Detalles  
 La lógica subyacente en la introducción de la `struct` argumento de tamaño (*lpVersionInfoSize*) consiste en habilitar la API que devuelva distintas versiones de la **LocalDBVersionInfostruct**, eficaz habilitar la compatibilidad con versiones anteriores y posteriores.  
  
 Si el `struct` argumento de tamaño (*lpVersionInfoSize*) coincide con el tamaño de una versión conocida de la **LocalDBVersionInfostruct**, esa versión de la `struct` se devuelve. De lo contrario, se devuelve LOCALDB_ERROR_INVALID_PARAMETER.  
  
 Un ejemplo típico de **LocalDBGetVersionInfo** uso de la API tiene este aspecto:  
  
```  
LocalDBVersionInfo vi;  
LocalDBVersionInfo(L"11.0", &vi, sizeof(LocalDBVersionInfo));  
  
```  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
