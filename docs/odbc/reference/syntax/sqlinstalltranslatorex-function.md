---
title: "Función SQLInstallTranslatorEx | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 241cb92786626bfc4674426c67f099f4349a6cb4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallTranslatorEx** agrega información sobre un traductor a la sección de Odbcinst.ini de la información del sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC traductores clave del registro).  
  
 La funcionalidad de **SQLInstallTranslatorEx** también puede tener acceso mediante [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Entrada] Esto debe contener una lista de pares de palabra clave y valor que describe el traductor doblemente terminada en null. Para obtener más información sobre la sintaxis del par palabra clave-valor, vea [subclaves de la especificación de traductor](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 El **traductor** y **el programa de instalación** palabras clave debe incluirse en la *lpszTranslator* cadena. La traducción DLL aparece con el **traductor** palabra clave y el programa de instalación de traductor DLL aparece con el **el programa de instalación** palabra clave. Cada par se termina con un byte NULL, y toda la lista se termina con un byte NULL. (Es decir, dos bytes NULL marcan el final de la lista.) El formato de *lpszTranslator* es como sigue:  
  
 \0Translator=*traductor-DLL-nombre de archivo*\0[Setup=*nombre del programa de instalación de archivo DLL*\0]\0  
  
 *lpszPathIn*  
 [Entrada] Ruta de acceso completa de un puntero nulo o donde es el traductor para instalarse. Si *lpszPath* es un puntero nulo, se instalarán los traductores en el directorio del sistema.  
  
 *lpszPathOut*  
 [Salida] La ruta de acceso del directorio de destino donde debe instalarse el traductor. Si nunca se ha instalado el traductor, *lpszPathOut* es el mismo que *lpszPathIn*. Si existe una instalación anterior del traductor, *lpszPathOut* es la ruta de acceso de la instalación anterior.  
  
 *cbPathOutMax*  
 [Entrada] Longitud de *lpszPathOut.*  
  
 *pcbPathOut*  
 [Salida] Número total de bytes disponible para devolver en *lpszPathOut*. Si el número de bytes disponible para devolver es mayor o igual que *cbPathOutMax*, la ruta de acceso de salida en *lpszPathOut* se trunca a *pcbPathOutMax* menos el carácter de terminación NULL. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_INQUIRY: Realizar consultas sobre donde se puede instalar un traductor.  
  
 ODBC_INSTALL_COMPLETE: Completar la solicitud de instalación.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de utilización del traductor después de llamar a esta función.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLInstallTranslatorEx** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszPathOut* argumento no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta de acceso truncado.<br /><br /> El *cbPathOutMax* argumento era 0 y el *fRequest* argumento era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidas|El *lpszTranslator* argumento contiene un error de sintaxis.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válida|El *lpszPathIn* argumento contiene una ruta de acceso no válido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válidos|El *lpszTranslator* argumento no contiene una lista de pares de palabra clave y valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el contador de uso de componente del registro|El instalador no pudo incrementar el contador de uso del traductor.|  
  
## <a name="comments"></a>Comentarios  
 **SQLInstallTranslatorEx** proporciona un mecanismo para instalar solo el traductor. Esta función no copia los archivos. El programa de llamada es responsable de copiar los archivos de traductor.  
  
 **SQLInstallTranslatorEx** incrementa el contador de uso de componente para el traductor instalado en 1. Si ya existe una versión del traductor, pero el contador de uso de componente para el traductor no existe, el nuevo valor de recuento de uso del componente se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente el archivo del traductor y mantener el contador de uso de archivo. Si previamente no se ha instalado el archivo de traductor, el programa de instalación de la aplicación debe copiar el archivo o archivos y crear el archivo o archivos recuento de uso. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el contador de uso de archivo.  
  
 Si previamente se instaló una versión anterior del traductor de la aplicación, el traductor se debe desinstalar y, a continuación, reinstalar, para que el recuento de uso del componente de traductor es válido. **SQLRemoveTranslator** debe llamarse para disminuir el recuento de uso del componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el contador de uso del componente. El programa de instalación de la aplicación debe reemplazar el antiguo archivo o archivos con el nuevo archivo. El contador de uso de archivo seguirá siendo el mismo, y otras aplicaciones que usan la versión del archivo anterior ahora usará la versión más reciente.  
  
 La longitud de la ruta de acceso en *lpszPathOut* en **SQLInstallTranslatorEx** permite para un proceso de instalación en dos fases, por lo que una aplicación puede determinar qué *cbPathOutMax* debe ser mediante una llamada a **SQLInstallTranslatorEx** con una *fRequest* del modo ODBC_INSTALL_INQUIRY. Esto devolverá el número total de bytes disponible en la *pcbPathOut* búfer. **SQLInstallTranslatorEx** , a continuación, se puede llamar con un *fRequest* de ODBC_INSTALL_COMPLETE y *cbPathOutMax* establecido en el valor de la *pcbPathOut* búfer más el carácter de terminación null.  
  
 Si decide no utilizar el modelo en dos fases para **SQLInstallTranslatorEx**, debe establecer *cbPathOutMax*, que define el tamaño del almacenamiento para la ruta de acceso del directorio de destino, que el valor _MAX_PATH, como se definen en Stdlib.h, para evitar el truncamiento.  
  
 Cuando *referien* es ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** no permite *lpszPathOut* null (o *cbPathOutMax* para ser 0). Si *referien* es ODBC_INSTALL_COMPLETE, se devuelve FALSE cuando el número de bytes disponible para devolver es mayor o igual que *cbPathOutMax*, con lo que el truncamiento se produce.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devolver una opción de traducción predeterminado|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Seleccionar traductores|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Quitar traductores|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|

