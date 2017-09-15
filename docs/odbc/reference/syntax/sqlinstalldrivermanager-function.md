---
title: "Función SQLInstallDriverManager | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLInstallDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverManager
helpviewer_keywords:
- SQLInstallDriverManager function [ODBC]
ms.assetid: aebc439b-fffd-4d98-907a-0163f79aee8d
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6bc56b9045ae3f9a53b410ef0546d539e3c25ee8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalldrivermanager-function"></a>SQLInstallDriverManager (función)
**Conformidad**  
 Versión presentado: ODBC 1.0: en desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y sistemas operativos posteriores  
  
 **Resumen**  
 **SQLInstallDriverManager** devuelve la ruta de acceso del directorio de destino para la instalación de los componentes principales ODBC. El programa de llamada realmente debe copiar archivos del Administrador de controladores en el directorio de destino.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszPath*  
 [Salida] Ruta de acceso del directorio de destino de la instalación.  
  
 *cbPathMax*  
 [Entrada] Longitud de *lpszPath*. Debe ser al menos bytes _MAX_PATH.  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (excepto el byte de finalización en null) devuelven en *lpszPath*. Si el número de bytes disponible para devolver es mayor o igual que *cbPathMax*, la ruta de acceso en *lpszPath* se trunca a *cbPathMax* menos la terminación null carácter. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLInstallDriverManager** devuelve FALSE, un asociado * \*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los * \*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszPath* argumento no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta de acceso truncado.<br /><br /> El *cbPathMax* argumento era menor que _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componente|El instalador no pudo incrementar el contador de uso del componente de núcleo ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallDriverManager** se llama para devolver la ruta de acceso para el número de componentes principales de ODBC y el uso del componente de incremento en la información del sistema. Si ya existe una versión del Administrador de controladores, pero el contador de uso de componente para el controlador no existe, el nuevo valor de recuento de uso del componente se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente los archivos de componente de núcleo y recuentos de mantener el uso de archivos. Si no se ha instalado previamente un archivo de componente principal, el programa de instalación de la aplicación debe copiar el archivo y crear el contador de uso de archivo. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el contador de uso de archivo.  
  
 Si el programa de instalación de la aplicación se instaló anteriormente una versión anterior del Administrador de controladores, los componentes principales se deben desinstalar y volver a instalar, para que el recuento de uso de componente de núcleo es válido. **SQLRemoveDriverManager** en primer lugar debe llamarse para disminuir el recuento de uso del componente. **SQLInstallDriverManager** , a continuación, se debe llamar para incrementar el contador de uso del componente. El programa de instalación de la aplicación debe reemplazar los archivos del componente principal antiguo con los nuevos archivos. Los recuentos de uso de archivo seguirá siendo el mismo, y otras aplicaciones que usan los archivos de componente de núcleo de versión anteriores ahora utilizará los archivos de la versión más reciente.  
  
 En una instalación nueva de los componentes principales ODBC, controladores y traductores, el programa de instalación de la aplicación debe llamar a las funciones siguientes en secuencia: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (con un *referien* de ODBC_INSTALL_DRIVER) y, a continuación, **SQLInstallTranslatorEx**. En la desinstalación de los componentes principales, los controladores y los traductores, el programa de instalación de la aplicación debe llamar a las funciones siguientes en secuencia: **SQLRemoveTranslator**, **SQLRemoveDriver**y, a continuación, **SQLRemoveDriverManager**. Estas funciones deben llamarse en esta secuencia. En una actualización de todos los componentes, todas las funciones de desinstalación deben llamarse en secuencia y, a continuación, todas las funciones de instalación deben llamarse en secuencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar un controlador|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalar un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Quitar un controlador|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Quitar el Administrador de controladores|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Quitar un traductor|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
