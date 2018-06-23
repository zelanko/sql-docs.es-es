---
title: Función LocalDBFormatMessage | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- LocalDBFormatMessage
api_location:
- sqluserinstance.dll
topic_type:
- apiref
ms.assetid: 31b3152a-94cf-4f75-a31b-296d7dd16dbe
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1d2fbc72ef5f3b54e1a9889150ebc27b08520ba9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112284"
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
  
## <a name="remarks"></a>Notas  
 Para obtener un ejemplo de código que utilice LocalDB API, vea [SQL Server Express LocalDB Reference](../sql-server-express-localdb-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Información de encabezado y versión de SQL Server Express LocalDB](sql-server-express-localdb-header-and-version-information.md)  
  
  