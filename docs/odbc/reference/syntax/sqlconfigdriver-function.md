---
title: Función SQLConfigDriver (SQLConfigDriver) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0da15cef06e5d8392408108ce88b53f7885eb65e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301250"
---
# <a name="sqlconfigdriver-function"></a>Función SQLConfigDriver
**Conformidad**  
 Versión introducida: ODBC 2.5  
  
 **Resumen**  
 **SQLConfigDriver** carga el archivo DLL de instalación del controlador adecuado y llama a la función **ConfigDriver.**  
  
 También se puede tener acceso a la funcionalidad de **SQLConfigDriver** con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Identificador de ventana principal. La función no mostrará ningún cuadro de diálogo si el identificador es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_CONFIG_DRIVER: Cambia el tiempo de espera de agrupación de conexiones utilizado por el controlador.  
  
 ODBC_INSTALL_DRIVER: Instala un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quita un controlador existente.  
  
 Esta opción también puede ser específica del controlador, en cuyo caso la *fRequest* para la primera opción debe comenzar desde ODBC_CONFIG_DRIVER_MAX+1. La *fRequest* para cualquier opción adicional también debe comenzar a partir de un valor mayor que ODBC_CONFIG_DRIVER_MAX+1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador tal como está registrado en la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Cadena terminada en null que contiene argumentos para un *fRequest*específico del controlador.  
  
 *lpszMsg*  
 [Salida] Cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponibles para devolver en *lpszMsg*. Si el número de bytes disponibles para devolver es mayor o igual que *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos el carácter de terminación nula. El argumento *pcbMsgOut* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLConfigDriver** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszMsg* no era válido.|  
|ODBC_ERROR_INVALID_HWND|Mango de ventana no válido|El argumento *hwndParent* no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *fRequest* no era uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> El argumento *fRequest* era una opción específica del controlador que era menor o igual que ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszDriver* no era válido. No se pudo encontrar en el registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidos|El argumento *lpszArgs* contenía un error de sintaxis.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitud* fallida|El instalador no pudo realizar la operación solicitada por el argumento *fRequest.* Error en la llamada a **ConfigDriver.**|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de configuración del controlador o traductor|No se ha podido cargar la biblioteca de configuración del controlador.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLConfigDriver** permite que una aplicación llame a la rutina **ConfigDriver** de un controlador sin tener que conocer el nombre y cargar el archivo DLL de instalación específico del controlador. Un programa de instalación llama a esta función después de instalar el archivo DLL de instalación del controlador. El programa de llamada debe tener en cuenta que esta función podría no estar disponible para todos los controladores. En tal caso, el programa que realiza la llamada debe continuar sin errores.  
  
## <a name="driver-specific-options"></a>Opciones específicas del conductor  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador mediante el argumento *fRequest.* La *fRequest* para la primera opción será ODBC_CONFIG_DRIVER_MAX+1, y las opciones adicionales se incrementarán en 1 a partir de ese valor. Los argumentos requeridos por el controlador para esa función deben proporcionarse en una cadena terminada en null que se pasa en el *argumento lpszArgs.* Los controladores que proporcionan esta funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones deben estar completamente documentadas en la documentación del controlador. Los escritores de aplicaciones que usan opciones específicas del controlador deben tener en cuenta que este uso hará que la aplicación sea menos interoperable.  
  
## <a name="setting-connection-pooling-timeout"></a>Configuración del tiempo de espera de agrupación de conexiones  
 Las propiedades de tiempo de espera de agrupación de conexiones se pueden establecer al establecer la configuración del controlador. **SQLConfigDriver** se llama con un *fRequest* de ODBC_CONFIG_DRIVER y *lpszArgs* establecido en **CPTimeout**. **CPTimeout** determina el período de tiempo que una conexión puede permanecer en el grupo de conexiones sin utilizarse. Cuando expira el tiempo de espera, la conexión se cierra y se quita del grupo. El tiempo de espera predeterminado es 60 segundos.  
  
 Cuando **SQLConfigDriver** se llama con *fRequest* establecido en ODBC_INSTALL_DRIVER o ODBC_REMOVE_DRIVER, el Administrador de controladores carga el archivo DLL de instalación del controlador adecuado y llama a la función **ConfigDriver.** Cuando **SQLConfigDriver** se llama con un *fRequest* de ODBC_CONFIG_DRIVER, todo el procesamiento se realiza en el instalador ODBC, de modo que no se tiene que cargar el archivo DLL de instalación del controlador.  
  
## <a name="messages"></a>error de Hadoop  
 Una rutina de configuración del controlador puede enviar un mensaje de texto a una aplicación como cadenas terminadas en null en el búfer *lpszMsg.* El mensaje se truncará a *cbMsgMax* menos el carácter de terminación nula por la función **ConfigDriver** si es mayor o igual que los caracteres *cbMsgMax.*  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(en el archivo DLL de instalación)|  
|Eliminación del origen de datos predeterminado|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
