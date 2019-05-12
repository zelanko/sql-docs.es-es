---
title: Función SQLConfigDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20316f2a7932768951633ae24e1b1e180c1dfb49
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537579"
---
# <a name="sqlconfigdriver-function"></a>Función SQLConfigDriver
**Conformidad**  
 Versión de introducción: ODBC 2.5  
  
 **Resumen**  
 **SQLConfigDriver** carga la DLL de instalación de controlador adecuado y llama a la **ConfigDriver** función.  
  
 La funcionalidad de **SQLConfigDriver** también se puede acceder con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_CONFIG_DRIVER: Cambia el tiempo de espera utilizado por el controlador de la agrupación de conexiones.  
  
 ODBC_INSTALL_DRIVER: Instala a un nuevo controlador.  
  
 ODBC_REMOVE_DRIVER: Quita un controlador existente.  
  
 Esta opción también puede ser específicos del controlador, en cuyo caso el *fRequest* para la primera opción se debe iniciar desde ODBC_CONFIG_DRIVER_MAX + 1. El *fRequest* para cualquier opción adicional también debe iniciar desde un valor mayor que ODBC_CONFIG_DRIVER_MAX + 1.  
  
 *lpszDriver*  
 [Entrada] El nombre del controlador como registrado en la información del sistema.  
  
 *lpszArgs*  
 [Entrada] Una cadena terminada en null que contiene los argumentos para un controlador específico *referien*.  
  
 *lpszMsg*  
 [Salida] Una cadena terminada en null que contiene un mensaje de salida de la configuración del controlador.  
  
 *cbMsgMax*  
 [Entrada] Longitud de *lpszMsg.*  
  
 *pcbMsgOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszMsg*. Si el número de bytes disponible para devolver es mayor o igual a *cbMsgMax*, el mensaje de salida en *lpszMsg* se trunca a *cbMsgMax* menos la terminación null carácter. El *pcbMsgOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLConfigDriver** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszMsg* argumento no era válido.|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válida|El *hwndParent* argumento no era válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no era uno de los siguientes:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> El *fRequest* argumento era una opción específica del controlador que era menor o igual que ODBC_CONFIG_DRIVER_MAX.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palabra clave y valor no válido|El *lpszArgs* argumento contenía un error de sintaxis.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|El programa de instalación no pudo realizar la operación solicitada por el *fRequest* argumento. La llamada a **ConfigDriver** error.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de traductor o controlador|No se pudo cargar la biblioteca del programa de instalación de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLConfigDriver** permite que una aplicación llamar a un controlador **ConfigDriver** rutinarias sin tener que conocer el nombre y cargar el archivo DLL de configuración específicos del controlador. Un programa de instalación llama a esta función después de la instalación del controlador que se ha instalado el archivo DLL. El programa que realiza la llamada debe tener en cuenta que esta función no esté disponible para todos los controladores. En tal caso, el programa que realiza la llamada debe continuar sin errores.  
  
## <a name="driver-specific-options"></a>Opciones específicas del controlador  
 Una aplicación puede solicitar características específicas del controlador expuestas por el controlador mediante el uso de la *fRequest* argumento. El *fRequest* para la primera opción serán ODBC_CONFIG_DRIVER_MAX + 1, y opciones adicionales se incrementa en 1 de ese valor. Los argumentos requeridos por el controlador para esa función debe proporcionarse en una cadena terminada en null pasados en el *lpszArgs* argumento. Los controladores que proporciona dicha funcionalidad deben mantener una tabla de opciones específicas del controlador. Las opciones deben estar completamente documentadas en la documentación del controlador. Los escritores de aplicaciones que usan las opciones específicas del controlador deben tener en cuenta que este uso realizará la aplicación menos interoperable.  
  
## <a name="setting-connection-pooling-timeout"></a>Establecer tiempo de espera de agrupación de conexiones  
 Al establecer la configuración del controlador, se pueden establecer las propiedades de tiempo de espera de agrupación de conexiones. **SQLConfigDriver** se denomina con un *referien* de ODBC_CONFIG_DRIVER y *lpszArgs* establecido en **CPTimeout**. **CPTimeout** determina el período de tiempo que una conexión puede permanecer en el grupo de conexiones sin ser usado. Cuando expira el tiempo de espera, la conexión se cierra y se quita del grupo. El tiempo de espera predeterminado es 60 segundos.  
  
 Cuando **SQLConfigDriver** se llama con *referien* establecido en ODBC_INSTALL_DRIVER o ODBC_REMOVE_DRIVER, el Administrador de controladores que se carga la DLL de instalación de controlador adecuado y llama a la  **ConfigDriver** función. Cuando **SQLConfigDriver** se denomina con un *referien* de ODBC_CONFIG_DRIVER, todo el procesamiento se realiza en el instalador ODBC, por lo que la DLL de instalación de controlador no tiene que cargarse.  
  
## <a name="messages"></a>Mensajes  
 Una rutina de configuración del controlador puede enviar un mensaje de texto a una aplicación como cadenas terminadas en null en la *lpszMsg* búfer. El mensaje se truncará a *cbMsgMax* menos el carácter de terminación null por el **ConfigDriver** función si es mayor o igual a *cbMsgMax* caracteres.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)(en el archivo DLL de configuración)|  
|Quitando el origen de datos predeterminado|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
