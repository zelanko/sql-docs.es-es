---
title: Función LocalDBFormatMessage | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBFormatMessage
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d5aa59cdb3b1c59b78a0ef99fb7d375275d370e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68091224"
---
# <a name="localdbformatmessage-function"></a>Función LocalDBFormatMessage
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Devuelve la descripción textual localizada del error de SQL Server Express LocalDB especificado.  
  
 **Archivo de encabezado:** SQLNCLI. h  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT LocalDBFormatMessage(  
           HRESULT hrLocalDB,  
           DWORD dwFlags,   
           DWORD dwLanguageId,   
           LPWSTR wszMessage,   
           LPDWORD lpcchMessage   
);  
```  
  
## <a name="parameters"></a>Parámetros  
 *hrLocalDB*  
 [Entrada] Código de error de LocalDB.  
  
 *dwFlags*  
 [Entrada] Marcadores que especifican el comportamiento de esta función.  
  
 Marcadores disponibles:  
  
 LOCALDB_TRUNCATE_ERR_MESSAGE  
 Si el búfer de entrada es demasiado corto, el mensaje de error se truncará para ajustarse al búfer.  
  
 *dwLanguageId*  
 [Entrada] Idioma elegido (LANGID) o 0, en cuyo caso se utiliza el orden de idioma FORMATMESSAGE de Win32.  
  
 *wszMessage*  
 [Salida] Búfer para almacenar el mensaje de error de LocalDB.  
  
 *lpcchMessage*  
 [Entrada/Salida] Contiene en la entrada el tamaño de búfer de *wszMessage* en caracteres. En la salida, si el tamaño de búfer proporcionado es demasiado pequeño, contiene el tamaño de búfer necesario en caracteres, lo cual incluye los valores NULL finales. Si la función se realiza correctamente, contiene el número de caracteres del mensaje, excepto los valores NULL finales.  
  
## <a name="returns"></a>Devuelve  
 S_OK  
 La función se ha realizado correctamente.  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 El mensaje solicitado no existe.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 El mensaje no está disponible en el idioma solicitado.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 El búfer de entrada *wszMessage* es demasiado corto y no se ha solicitado truncamiento.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 Se ha producido un error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Observaciones  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../../relational-databases/sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Consulte también  
 [Información de encabezado y versión de SQL Server Express LocalDB](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
