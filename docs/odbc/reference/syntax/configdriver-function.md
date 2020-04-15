---
title: Función ConfigDriver (ConfigDriver) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a2da5fd5ce01bd97f13d7c8d805c615c1ac436a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303966"
---
# <a name="configdriver-function"></a>Función ConfigDriver
**Conformidad**  
 Versión introducida: ODBC 2.5  
  
 **Resumen**  
 **ConfigDriver** permite que un programa de instalación realice funciones de instalación y desinstalación sin necesidad de que el programa llame a **ConfigDSN**. Esta función realizará funciones específicas del controlador, como la creación de información del sistema específica del controlador y la realización de conversiones de DSN durante la instalación, así como la limpieza de las modificaciones de información del sistema durante la desinstalación. Esta función se expone mediante el archivo DLL de instalación del controlador o un archivo DLL de instalación independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de ventana principal. La función no mostrará ningún cuadro de diálogo si el identificador es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El argumento *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_DRIVER: Instale un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quite un controlador.  
  
 Esta opción también puede ser específica del controlador, en cuyo caso el argumento *fRequest* de la primera opción debe comenzar desde ODBC_CONFIG_DRIVER_MAX+1. El argumento *fRequest* para cualquier opción adicional también debe comenzar a partir de un valor mayor que ODBC_CONFIG_DRIVER_MAX+1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador registrado en la clave Odbcinst.ini de la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Cadena terminada en null que contiene argumentos para un *fRequest*específico del controlador .  
  
 *lpszMsg*  
 [Salida] Cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg*.  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponibles para devolver en *lpszMsg*.  
  
 Si el número de bytes disponibles para devolver es mayor o igual que *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos el carácter de terminación nula. El argumento *pcbMsgOut* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **ConfigDriver** devuelve FALSE, se registra un valor * \*pfErrorCode* asociado en el búfer de errores del instalador mediante una llamada a **SQLPostInstallerError** y se puede obtener llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Mango de ventana no válido|El argumento *hwndParent* no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *fRequest* no era uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> La opción específica del controlador era menor o igual que ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszDriver* no era válido. No se pudo encontrar en el registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitud* fallida|No se pudo realizar la operación solicitada por el argumento *fRequest.*|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *Argumento SzError de* una llamada a la función **SQLPostInstallerError** debe contener el mensaje de error específico del controlador.|  
  
## <a name="comments"></a>Comentarios  
  
### <a name="driver-specific-options"></a>Opciones específicas del conductor  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador mediante el argumento *fRequest.* La *fRequest* para la primera opción se ODBC_CONFIG_DRIVER_MAX más 1, y las opciones adicionales se incrementarán en 1 a partir de ese valor. Los argumentos requeridos por el controlador para esa función deben proporcionarse en una cadena terminada en null que se pasa en el *argumento lpszArgs.* Los controladores que proporcionan esta funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones deben estar completamente documentadas en la documentación del controlador. Los escritores de aplicaciones que usan opciones específicas del controlador deben tener en cuenta que esto hará que la aplicación sea menos interoperable.  
  
### <a name="messages"></a>error de Hadoop  
 Una rutina de configuración del controlador puede enviar un mensaje de texto a una aplicación como una cadena terminada en null en el búfer *lpszMsg.* El mensaje se truncará a *cbMsgMax* menos el carácter de terminación nula por la función **ConfigDriver** si es mayor o igual que los caracteres *cbMsgMax.*
