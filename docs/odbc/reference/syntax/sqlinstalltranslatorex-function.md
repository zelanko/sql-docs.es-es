---
title: Función SQLInstallTranslatorEx ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302096"
---
# <a name="sqlinstalltranslatorex-function"></a>Función SQLInstallTranslatorEx
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallTranslatorEx** agrega información acerca de un traductor a la sección Odbcinst.ini de la información del sistema (HKEY_LOCAL_MACHINE,SOFTWARE, ODBC, ODBCINST. InI-ODBC Translators clave del Registro).  
  
 También se puede tener acceso a la funcionalidad de **SQLInstallTranslatorEx** con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] Esto debe contener una lista doblemente terminada en null de pares palabra clave-valor que describen el traductor. Para obtener más información acerca de la sintaxis de pares palabra clave-valor, consulte Subclaves de [especificación](../../../odbc/reference/install/translator-specification-subkeys.md)de traductor .  
  
 Las palabras clave **Translator** y **Setup** deben incluirse en la cadena *lpszTranslator.* El archivo DLL de traducción se muestra con la palabra clave **Translator** y el archivo DLL de instalación del traductor se muestra con la palabra clave **Setup.** Cada par se termina con un byte NULL y toda la lista se termina con un byte NULL. (Es decir, dos bytes NULL marcan el final de la lista.) El formato de *lpszTranslator* es el siguiente:  
  
 Nombre de*archivo de la DLL del traductor de*0Traductor s0[Configuración-ARCHIVO-DLL-Nombre de*archivo*n.o 0]-0  
  
 *lpszPathIn*  
 [Entrada] Ruta de acceso completa de dónde se va a instalar el traductor o un puntero nulo. Si *lpszPath* es un puntero nulo, los traductores se instalarán en el directorio del sistema.  
  
 *lpszPathOut*  
 [Salida] La ruta del directorio de destino donde se debe instalar el traductor. Si el traductor nunca se ha instalado, *lpszPathOut* es el mismo que *lpszPathIn*. Si existe una instalación previa del traductor, *lpszPathOut* es la ruta de acceso de la instalación anterior.  
  
 *cbPathOutMax*  
 [Entrada] Longitud de *lpszPathOut.*  
  
 *pcbPathOut*  
 [Salida] Número total de bytes disponibles para devolver en *lpszPathOut*. Si el número de bytes disponibles para devolver es mayor o igual que *cbPathOutMax*, la ruta de salida de *lpszPathOut* se trunca en *pcbPathOutMax* menos el carácter de terminación null. El argumento *pcbPathOut* puede ser un puntero nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_INQUIRY: Pregunte dónde se puede instalar un traductor.  
  
 ODBC_INSTALL_COMPLETE: Complete la solicitud de instalación.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de uso del traductor después de llamar a esta función.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLInstallTranslatorEx** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszPathOut* no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta truncada.<br /><br /> El argumento *cbPathOutMax* era 0 y el argumento *fRequest* se ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *fRequest* no era uno de los siguientes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidos|El argumento *lpszTranslator* contenía un error de sintaxis.|  
|ODBC_ERROR_INVALID_PATH|Ruta de instalación no válida|El argumento *lpszPathIn* contenía una ruta de acceso no válida.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válida|El argumento *lpszTranslator* no contenía una lista de pares palabra clave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo aumentar o disminuir el recuento de uso de componentes del registro|El instalador no pudo incrementar el número de uso del traductor.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallTranslatorEx** proporciona un mecanismo para instalar solo el traductor. Esta función no copia realmente ningún archivo. El programa de llamada es responsable de copiar los archivos del traductor.  
  
 **SQLInstallTranslatorEx** incrementa el recuento de uso de componentes para el traductor instalado en 1. Si ya existe una versión del traductor pero el recuento de uso de componentes para el traductor no existe, el nuevo valor de recuento de uso de componentes se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente el archivo del traductor y mantener el recuento de uso del archivo. Si el archivo de traductor no se ha instalado previamente, el programa de instalación de la aplicación debe copiar el archivo o los archivos y crear el recuento de uso de archivos o archivos. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el recuento de uso del archivo.  
  
 Si la aplicación instaló previamente una versión anterior del traductor, se debe desinstalar y volver a instalar el traductor, de modo que el recuento de uso del componente del traductor sea válido. **SQLRemoveTranslator** debe llamarse para disminuir el recuento de uso del componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar el archivo o archivos antiguos con el nuevo archivo. El recuento de uso de archivos seguirá siendo el mismo, y otras aplicaciones que usaron el archivo de versión anterior ahora usarán la versión más reciente.  
  
 La longitud de la ruta de acceso en *lpszPathOut* en **SQLInstallTranslatorEx** permite un proceso de instalación en dos fases, por lo que una aplicación puede determinar qué debe ser *cbPathOutMax* llamando a **SQLInstallTranslatorEx** con un *fRequest* de modo ODBC_INSTALL_INQUIRY. Esto devolverá el número total de bytes disponibles en el búfer *pcbPathOut.* **SQLInstallTranslatorEx,** a continuación, se puede llamar con un *fRequest* de ODBC_INSTALL_COMPLETE y el *cbPathOutMax* argumento establecido en el valor en el *búfer pcbPathOut,* más el carácter de terminación null.  
  
 Si decide no utilizar el modelo de dos fases para **SQLInstallTranslatorEx**, debe establecer *cbPathOutMax*, que define el tamaño del almacenamiento para la ruta de acceso del directorio de destino, en el valor _MAX_PATH, tal como se define en Stdlib.h, para evitar el truncamiento.  
  
 Cuando *fRequest* es ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** no permite que *lpszPathOut* sea NULL (o *cbPathOutMax* sea 0). Si *fRequest* es ODBC_INSTALL_COMPLETE, FALSE se devuelve cuando el número de bytes disponibles para devolver es mayor o igual que *cbPathOutMax*, con el resultado de que se produce el truncamiento.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver una opción de traducción predeterminada|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selección de traductores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Eliminación de traductores|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
