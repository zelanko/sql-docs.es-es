---
title: Función SQLInstallDriverManager ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0788de0493439a360c0446733b31606a02e12422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302116"
---
# <a name="sqlinstalldrivermanager-function"></a>Función SQLInstallDriverManager
**Conformidad**  
 Versión introducida: ODBC 1.0: en desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y sistemas operativos posteriores  
  
 **Resumen**  
 **SQLInstallDriverManager** devuelve la ruta de acceso del directorio de destino para la instalación de los componentes principales ODBC. El programa que realiza la llamada debe copiar los archivos del Administrador de controladores en el directorio de destino.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLInstallDriverManager(  
     LPSTR    lpszPath,  
     WORD     cbPathMax,  
     WORD *   pcbPathOut);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszPath*  
 [Salida] Ruta de acceso del directorio de destino de la instalación.  
  
 *cbPathMax*  
 [Entrada] Longitud de *lpszPath*. Debe ser al menos _MAX_PATH bytes.  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (excluyendo el byte de terminación null) devueltos en *lpszPath*. Si el número de bytes disponibles para devolver es mayor o igual que *cbPathMax*, la ruta de acceso en *lpszPath* se trunca a *cbPathMax* menos el carácter de terminación nula. El argumento *pcbPathOut* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLInstallDriverManager** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszPath* no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta truncada.<br /><br /> El argumento *cbPathMax* era menor que _MAX_PATH.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componentes|El instalador no pudo incrementar el recuento de uso del componente principal ODBC.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallDriverManager** se llama para devolver la ruta de acceso para los componentes principales ODBC e incrementar el recuento de uso de componentes en la información del sistema. Si ya existe una versión del Administrador de controladores pero el recuento de uso de componentes para el controlador no existe, el nuevo valor de recuento de uso de componentes se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente los archivos del componente principal y mantener los recuentos de uso de archivos. Si un archivo de componente principal no se ha instalado previamente, el programa de instalación de la aplicación debe copiar el archivo y crear el recuento de uso del archivo. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el recuento de uso de archivos.  
  
 Si el programa de instalación de la aplicación instaló previamente una versión anterior del Administrador de controladores, los componentes principales deben desinstalarse y volver a instalarse, de modo que el recuento de uso del componente principal sea válido. **SQLRemoveDriverManager** primero debe llamarse para disminuir el recuento de uso de componentes. **SQLInstallDriverManager,** a continuación, debe llamarse para incrementar el recuento de uso de componentes. El programa de instalación de la aplicación debe reemplazar los archivos de componentes principales antiguos con los nuevos archivos. Los recuentos de uso de archivos seguirán siendo los mismos, y otras aplicaciones que usaron los archivos de componentes principales de la versión anterior ahora usarán los archivos de versión más reciente.  
  
 En una nueva instalación de los componentes principales de ODBC, controladores y traductores, el programa de instalación de la aplicación debe llamar a las siguientes funciones en secuencia: **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLConfigDriver** (con una *fRequest* de ODBC_INSTALL_DRIVER) y, a continuación, **SQLInstallTranslatorEx**. En una desinstalación de los componentes principales, controladores y traductores, el programa de instalación de la aplicación debe llamar a las siguientes funciones en secuencia: **SQLRemoveTranslator**, **SQLRemoveDriver**y, a continuación, **SQLRemoveDriverManager**. Estas funciones deben llamarse en esta secuencia. En una actualización de todos los componentes, todas las funciones de desinstalación deben llamarse en secuencia y, a continuación, todas las funciones de instalación deben llamarse en secuencia.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalación de un controlador|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|  
|Instalación de un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|  
|Extracción de un controlador|[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|  
|Extracción del Administrador de controladores|[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|  
|Eliminación de un traductor|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
