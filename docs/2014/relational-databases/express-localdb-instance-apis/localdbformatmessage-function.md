---
title: Función LocalDBFormatMessage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
api_name:
- LocalDBFormatMessage
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d287a7ceff1c38c829da91a8ae2e530f664fb4ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128748"
---
# <a name="localdbformatmessage-function"></a>Función LocalDBFormatMessage
  Devuelve la descripción textual localizada del error de SQL Server Express LocalDB especificado.  
  
 **Archivo de encabezado:** sqlncli.h  
  
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
  
 [LOCALDB_ERROR_NOT_INSTALLED](../express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB no está instalado en el equipo.  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 Uno o más parámetros de entrada especificados no son válidos.  
  
 [LOCALDB_ERROR_UNKNOWN_ERROR_CODE](../express-localdb-error-messages/localdb-error-unknown-error-code.md)  
 El mensaje solicitado no existe.  
  
 [LOCALDB_ERROR_UNKNOWN_LANGUAGE_ID](../express-localdb-error-messages/localdb-error-unknown-language-id.md)  
 El mensaje no está disponible en el idioma solicitado.  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 El búfer de entrada *wszMessage* es demasiado corto y no se ha solicitado truncamiento.  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../express-localdb-error-messages/localdb-error-internal-error.md)  
 Error inesperado. Vea el registro de eventos para obtener detalles.  
  
## <a name="remarks"></a>Comentarios  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  
