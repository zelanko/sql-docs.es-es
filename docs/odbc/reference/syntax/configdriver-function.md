---
title: Función ConfigDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d69db144a460bb2f662c8ba906bf0302cdf98388
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821663"
---
# <a name="configdriver-function"></a>Función ConfigDriver
**Conformidad**  
 Versión introdujo: ODBC 2.5  
  
 **Resumen**  
 **ConfigDriver** permite que un programa de instalación realizar la instalación y desinstalación de funciones sin necesidad de que el programa para llamar a **ConfigDSN**. Esta función llevará a cabo funciones específicas del controlador como crear información específica del controlador del sistema y realizar conversiones de DSN durante la instalación, así como para limpiar las modificaciones de información del sistema durante la desinstalación. Esta función se expone mediante la configuración del controlador de archivo DLL o un archivo DLL de configuración independiente.  
  
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
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El *fRequest* argumento debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_DRIVER: Instalar a un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quitar un controlador.  
  
 Esta opción también puede ser específicos del controlador, en cuyo caso el *fRequest* argumento para la primera opción se debe iniciar desde ODBC_CONFIG_DRIVER_MAX + 1. El *fRequest* argumento para cualquier opción adicional también debe iniciar desde un valor mayor que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador como registrado en la clave de Odbcinst.ini la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Una cadena terminada en null que contiene los argumentos para un determinado controlador *referien*.  
  
 *lpszMsg*  
 [Salida] Una cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg*.  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszMsg*.  
  
 Si el número de bytes disponible para devolver es mayor o igual a *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos la terminación null carácter. El *pcbMsgOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **ConfigDriver** devuelve FALSE, un asociado  *\*pfErrorCode* valor se registra en el búfer de error del instalador mediante una llamada a **SQLPostInstallerError** y puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válida|El *hwndParent* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no era uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> La opción específicos del controlador era menor o igual a ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|No se pudo realizar la operación solicitada por el *fRequest* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Un error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *SzError* argumento en una llamada a la **SQLPostInstallerError** función debe contener el mensaje de error específico del controlador.|  
  
## <a name="comments"></a>Comentarios  
  
### <a name="driver-specific-options"></a>Opciones específicas del controlador  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador mediante el uso de la *fRequest* argumento. El *fRequest* para la primera opción serán ODBC_CONFIG_DRIVER_MAX más 1, y opciones adicionales se incrementa en 1 de ese valor. Los argumentos requeridos por el controlador para esa función debe proporcionarse en una cadena terminada en null pasados en el *lpszArgs* argumento. Los controladores que proporciona dicha funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones deben estar completamente documentadas en la documentación del controlador. Los escritores de aplicaciones que usan las opciones específicas del controlador deben tener en cuenta que esto hará que la aplicación menos interoperable.  
  
### <a name="messages"></a>Mensajes  
 Una rutina de configuración del controlador puede enviar un mensaje de texto a una aplicación como una cadena terminada en null en la *lpszMsg* búfer. El mensaje se truncará a *cbMsgMax* menos el carácter de terminación null por el **ConfigDriver** función si es mayor o igual a *cbMsgMax* caracteres.
