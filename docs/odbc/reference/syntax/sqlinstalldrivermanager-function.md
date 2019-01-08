---
title: Función SQLInstallDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47069f1003b9b3f9bddb1e8601b3b4284372ae7e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205194"
---
# <a name="sqlinstalldrivermanager-function"></a>Función SQLInstallDriverManager
**Conformidad**  
 Versión de introducción: ODBC 1.0: En desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y los sistemas operativos posteriores  
  
 **Resumen**  
 **SQLInstallDriverManager** devuelve la ruta de acceso del directorio de destino para la instalación de los componentes principales ODBC. El programa de llamada realmente debe copiar los archivos del Administrador de controladores en el directorio de destino.  
  
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
 [Salida] Número total de bytes (sin incluir los bytes de terminación null) devuelven en *lpszPath*. Si el número de bytes disponible para devolver es mayor o igual a *cbPathMax*, la ruta de acceso en *lpszPath* se trunca a *cbPathMax* menos la terminación null carácter. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLInstallDriverManager** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszPath* argumento no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta de acceso truncado.<br /><br /> El *cbPathMax* argumento era menor que _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de utilización de componente|El instalador no pudo incrementar el contador de uso de componentes ODBC core.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallDriverManager** se llama para devolver la ruta de acceso para el número de componentes principales de ODBC y el uso de componentes de incremento en la información del sistema. Si ya existe una versión del Administrador de controladores, pero no existe el contador de uso del componente para el controlador, el nuevo valor de recuento de uso del componente se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente los archivos de componentes principales y recuentos de mantener el uso de archivos. Si no se ha instalado anteriormente un archivo de componente principal, el programa de instalación de la aplicación debe copiar el archivo y crear el contador de uso de archivo. Si el archivo se ha instalado anteriormente, el programa de instalación simplemente incrementa el recuento de uso de archivo.  
  
 Si anteriormente ha instalado una versión anterior del Administrador de controladores el programa de instalación de la aplicación, los componentes principales deben desinstalar y, a continuación, reinstalar, para que el recuento de uso de núcleos componente es válido. **SQLRemoveDriverManager** en primer lugar debe llamarse para reducir el recuento de uso del componente. **SQLInstallDriverManager** , a continuación, debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar los archivos del componente principal antiguo con los nuevos archivos. Los recuentos de uso de archivos seguirán siendo las mismas y otras aplicaciones que usan los archivos de componente de core versión anterior, ahora se usarán archivos de la versión más reciente.  
  
 En una instalación nueva de los componentes principales, controladores y traductores ODBC, el programa de instalación de la aplicación debe llamar a las siguientes funciones de secuencia: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (con un *referien* de ODBC_INSTALL_DRIVER) y, a continuación,  **SQLInstallTranslatorEx**. En una desinstalación de los componentes principales, controladores y traductores, el programa de instalación de la aplicación debe llamar a las siguientes funciones de secuencia: **SQLRemoveTranslator**, **SQLRemoveDriver**y, a continuación, **SQLRemoveDriverManager**. Estas funciones deben llamarse en esta secuencia. En una actualización de todos los componentes, todas las funciones de desinstalación deben llamarse en secuencia y, a continuación, todas las funciones de instalación deben llamarse en secuencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar un controlador|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalación de un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Eliminación de un controlador|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Quitar el Administrador de controladores|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Eliminación de un traductor|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
