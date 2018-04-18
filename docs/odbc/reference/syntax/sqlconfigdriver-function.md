---
title: Función SQLConfigDriver | Documentos de Microsoft
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
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6459e3faeafddc2faef3b69a68a1bf975ac6c3e4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver (función)
**Conformidad**  
 Versión introdujo: ODBC 2.5  
  
 **Resumen**  
 **SQLConfigDriver** carga el archivo DLL de configuración de controlador adecuado y llama el **ConfigDriver** función.  
  
 La funcionalidad de **SQLConfigDriver** también puede tener acceso mediante [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador no es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_CONFIG_DRIVER: Cambia el tiempo de espera utilizado por el controlador de la agrupación de conexiones.  
  
 ODBC_INSTALL_DRIVER: Instala a un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quita un controlador existente.  
  
 Esta opción también puede ser específicos del controlador, en cuyo caso el *fRequest* para la primera opción debe iniciar desde ODBC_CONFIG_DRIVER_MAX + 1. El *fRequest* para cualquier opción adicional también debe iniciar desde un valor mayor que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador como está registrado en la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Una cadena terminada en null que contiene los argumentos para un determinado controlador *fRequest*.  
  
 *lpszMsg*  
 [Salida] Una cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszMsg*. Si el número de bytes disponible para devolver es mayor o igual que *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos la terminación null carácter. El *pcbMsgOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLConfigDriver** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszMsg* argumento no era válido.|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> El *fRequest* argumento era una opción específica del controlador que era menor o igual que ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidas|El *lpszArgs* argumento contiene un error de sintaxis.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|El programa de instalación no pudo realizar la operación solicitada por el *fRequest* argumento. La llamada a **ConfigDriver** error.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de controlador o traductor|No se pudo cargar la biblioteca de instalación de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLConfigDriver** permite que una aplicación llamar a un controlador **ConfigDriver** rutina sin tener que conocer el nombre y cargar el archivo DLL de configuración específicos del controlador. Un programa de instalación llama a esta función después de la instalación del controlador que se ha instalado el archivo DLL. El programa que realiza la llamada debe tener en cuenta que esta función podría no estar disponible para todos los controladores. En tal caso, el programa que realiza la llamada debe continuar sin errores.  
  
## <a name="driver-specific-options"></a>Opciones específicas del controlador  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador usando el *fRequest* argumento. El *fRequest* para la primera opción será ODBC_CONFIG_DRIVER_MAX + 1 y opciones adicionales se incrementan en 1 de ese valor. Pasan los argumentos requeridos por el controlador para esa función se debe proporcionar en una cadena terminada en null el *lpszArgs* argumento. Controladores de proporcionar esta funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones se deben documentar completamente en la documentación del controlador. Los escritores de aplicaciones que usan opciones específicas del controlador deben tener en cuenta que este uso realizará la aplicación menos interoperable.  
  
## <a name="setting-connection-pooling-timeout"></a>Establecer tiempo de espera de agrupación de conexiones  
 Propiedades de tiempo de espera de agrupación de conexiones se pueden establecer cuando se establece la configuración del controlador. **SQLConfigDriver** se llama con un *referien* de ODBC_CONFIG_DRIVER y *lpszArgs* establecido en **CPTimeout**. **CPTimeout** determina el período de tiempo que una conexión puede permanecer en la agrupación de conexiones sin que se va a usar. Cuando expira el tiempo de espera, la conexión se cierra y se quita del grupo. El tiempo de espera predeterminado es 60 segundos.  
  
 Cuando **SQLConfigDriver** se llama con *referien* establecido en ODBC_INSTALL_DRIVER o ODBC_REMOVE_DRIVER, el Administrador de controladores que se carga el archivo DLL de configuración de controlador adecuado y llama el  **ConfigDriver** función. Cuando **SQLConfigDriver** se llama con un *referien* de ODBC_CONFIG_DRIVER, todo el procesamiento se realiza en el instalador ODBC, por lo que el archivo DLL de configuración de controlador no tiene que se va a cargar.  
  
## <a name="messages"></a>Mensajes  
 Una rutina de instalación de controlador puede enviar un mensaje de texto a una aplicación como cadenas terminadas en null en la *lpszMsg* búfer. El mensaje se truncará a *cbMsgMax* menos el carácter de terminación null por la **ConfigDriver** funcionar si es mayor o igual que *cbMsgMax* caracteres.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(en la configuración del archivo DLL)|  
|Quitando el origen de datos predeterminada|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
