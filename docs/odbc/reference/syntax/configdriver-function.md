---
title: Función ConfigDriver | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56825fd24bd452365d5c3279c6aa68db83bd2470
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configdriver-function"></a>ConfigDriver (función)
**Conformidad**  
 Versión introdujo: ODBC 2.5  
  
 **Resumen**  
 **ConfigDriver** permite que un programa de instalación para realizar la instalación y desinstalación de funciones sin necesidad de llamar al programa **ConfigDSN**. Esta función llevará a cabo funciones específicas del controlador como creación de información del sistema específicos del controlador y realizar conversiones de DSN durante la instalación, así como para limpiar las modificaciones de información del sistema durante la desinstalación. Esta función se expone mediante el programa de instalación de controlador DLL o un archivo DLL de configuración independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador no es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El *fRequest* argumento debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_DRIVER: Instalar a un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quitar un controlador.  
  
 Esta opción también puede ser específicos del controlador, en cuyo caso el *fRequest* argumento para la primera opción debe iniciar desde ODBC_CONFIG_DRIVER_MAX + 1. El *fRequest* argumento para cualquier opción adicional también debe iniciar desde un valor mayor que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador como está registrado en la clave de Odbcinst.ini de la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Una cadena terminada en null que contiene argumentos de un determinado controlador *fRequest*.  
  
 *lpszMsg*  
 [Salida] Una cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg*.  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszMsg*.  
  
 Si el número de bytes disponible para devolver es mayor o igual que *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos la terminación null carácter. El *pcbMsgOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **ConfigDriver** devuelve FALSE, un asociado  *\*pfErrorCode* valor se registra en el búfer de error del instalador mediante una llamada a **SQLPostInstallerError** y puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> La opción específicos del controlador era menor o igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|No se pudo realizar la operación solicitada por el *fRequest* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Un error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *SzError* argumento en una llamada a la **SQLPostInstallerError** función debe contener el mensaje de error específico del controlador.|  
  
## <a name="comments"></a>Comentarios  
  
### <a name="driver-specific-options"></a>Opciones específicas del controlador  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador usando el *fRequest* argumento. El *fRequest* para la primera opción será ODBC_CONFIG_DRIVER_MAX más 1, y opciones adicionales se incrementan en 1 de ese valor. Pasan los argumentos requeridos por el controlador para esa función se debe proporcionar en una cadena terminada en null el *lpszArgs* argumento. Controladores de proporcionar esta funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones se deben documentar completamente en la documentación del controlador. Los escritores de aplicaciones que usan opciones específicas del controlador deben tener en cuenta que esto hará que la aplicación menos interoperable.  
  
### <a name="messages"></a>Mensajes  
 Una rutina de instalación de controlador puede enviar un mensaje de texto a una aplicación como una cadena terminada en null en la *lpszMsg* búfer. El mensaje se truncará a *cbMsgMax* menos el carácter de terminación null por la **ConfigDriver** funcionar si es mayor o igual que *cbMsgMax* caracteres.
