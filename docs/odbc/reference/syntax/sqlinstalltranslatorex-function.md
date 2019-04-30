---
title: Función SQLInstallTranslatorEx | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 276b8627588bcd3472c12564db1e8c6e6af1ef2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242314"
---
# <a name="sqlinstalltranslatorex-function"></a>Función SQLInstallTranslatorEx
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallTranslatorEx** agrega información sobre un traductor de la sección de Odbcinst.ini de la información del sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC traductores clave del registro).  
  
 La funcionalidad de **SQLInstallTranslatorEx** también se puede acceder con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Esto debe contener una lista doblemente terminada en null de pares de palabra clave y valor que describe el traductor. Para obtener más información sobre la sintaxis del par de palabra clave y valor, vea [subclaves de la especificación de traductor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 El **traductor** y **instalación** palabras clave que deben incluirse en el *lpszTranslator* cadena. La traducción de archivo DLL se muestra con la **traductor** palabra clave y el programa de instalación de traductor DLL aparece con el **instalación** palabra clave. Cada par se termina con un byte NULL, y toda la lista se termina con un byte NULL. (Es decir, dos bytes NULL marcan el final de la lista). El formato de *lpszTranslator* es como sigue:  
  
 \0Translator=*translator-DLL-filename*\0[Setup=*setup-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [Entrada] Ruta de acceso completa de un puntero nulo o donde es el traductor para instalarse. Si *lpszPath* es un puntero nulo, se instalarán los traductores en el directorio del sistema.  
  
 *lpszPathOut*  
 [Salida] La ruta de acceso del directorio de destino donde debe instalarse el traductor. Si nunca se ha instalado el traductor, *lpszPathOut* es el mismo que *lpszPathIn*. Si existe una instalación anterior del traductor, *lpszPathOut* es la ruta de acceso de la instalación anterior.  
  
 *cbPathOutMax*  
 [Entrada] Longitud de *lpszPathOut.*  
  
 *pcbPathOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszPathOut*. Si el número de bytes disponible para devolver es mayor o igual a *cbPathOutMax*, la ruta de acceso de salida en *lpszPathOut* se trunca a *pcbPathOutMax* menos el carácter de terminación NULL. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_INQUIRY: Realizar consultas sobre dónde se puede instalar un traductor.  
  
 ODBC_INSTALL_COMPLETE: Completar la solicitud de instalación.  
  
 *lpdwUsageCount*  
 [Salida] El contador de uso del traductor después de llamar a esta función.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLInstallTranslatorEx** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszPathOut* argumento no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta de acceso truncado.<br /><br /> El *cbPathOutMax* argumento era 0 y el *fRequest* argumento era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no era uno de los siguientes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares de palabra clave y valor no válido|El *lpszTranslator* argumento contenía un error de sintaxis.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válido|El *lpszPathIn* argumento contiene una ruta de acceso no válido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válidos|El *lpszTranslator* argumento no contiene una lista de pares de palabra clave y valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso del componente del registro|El instalador no pudo incrementar el contador de uso del traductor.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallTranslatorEx** proporciona un mecanismo para instalar solo el traductor. Esta función no copia los archivos. El programa de llamada es responsable de copiar los archivos de traductor.  
  
 **SQLInstallTranslatorEx** incrementa el contador de uso del componente para el traductor instalado en 1. Si ya existe una versión del traductor, pero el recuento de utilización del componente para el traductor no existe, el nuevo valor de recuento de uso del componente se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente el archivo de traductor y mantener el contador de uso de archivo. Si no se ha instalado previamente el archivo de traductor, el programa de instalación de la aplicación debe copiar los archivos y crear el archivo o archivos recuento de uso. Si el archivo se ha instalado anteriormente, el programa de instalación simplemente incrementa el recuento de uso de archivo.  
  
 Si previamente se instaló una versión anterior del traductor por la aplicación, el traductor se debe desinstalar y volver a instalar, para que el recuento de utilización del componente traductor es válido. **SQLRemoveTranslator** debe llamarse para reducir el recuento de uso de componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar el antiguo archivo o archivos con el nuevo archivo. El recuento de uso de archivos seguirán siendo las mismas y otras aplicaciones que usan el archivo de la versión anterior, ahora se usarán la versión más reciente.  
  
 La longitud de la ruta de acceso en *lpszPathOut* en **SQLInstallTranslatorEx** permite un proceso de instalación en dos fases, por lo que una aplicación puede determinar qué *cbPathOutMax* debe mediante una llamada a **SQLInstallTranslatorEx** con un *fRequest* del modo ODBC_INSTALL_INQUIRY. Esto devolverá el número total de bytes disponibles en el *pcbPathOut* búfer. **SQLInstallTranslatorEx** , a continuación, se puede llamar con un *fRequest* de ODBC_INSTALL_COMPLETE y *cbPathOutMax* argumento establecido en el valor de la *pcbPathOut* búfer más el carácter de terminación null.  
  
 Si decide no utilizar el modelo en dos fases para **SQLInstallTranslatorEx**, debe establecer *cbPathOutMax*, que define el tamaño del almacenamiento para la ruta de acceso del directorio de destino, en el valor _MAX_PATH, como se define en Stdlib.h, para evitar el truncamiento.  
  
 Cuando *referien* es ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** no permite *lpszPathOut* null (o *cbPathOutMax* sea 0). Si *referien* es ODBC_INSTALL_COMPLETE, se devuelve FALSE cuando el número de bytes disponible para devolver es mayor o igual a *cbPathOutMax*, con lo que el truncamiento se produce.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve una opción de traducción predeterminado|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selección de traductores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Eliminación de traductores|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
