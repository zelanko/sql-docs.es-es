---
title: "Función SQLGetTranslator | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetTranslator
helpviewer_keywords: SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d8b0f18e683facc1316fd5a58ac1a2983acea63
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgettranslator-function"></a>SQLGetTranslator (función)
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **SQLGetTranslator** muestra un cuadro de diálogo desde el que un usuario puede seleccionar un traductor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLGetTranslator(  
     HWND      hwndParent,  
     LPSTR     lpszName,  
     WORD      cbNameMax,  
     WORD *    pcbNameOut,  
     LPSTR     lpszPath,  
     WORD      cbPathMax,  
     WORD *    pcbPathOut,  
     DWORD *   pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de la ventana primaria.  
  
 *lpszName*  
 [Entrada/salida] Nombre del traductor de la información del sistema.  
  
 *cbNameMax*  
 [Entrada] Longitud máxima de la *lpszName* búfer.  
  
 *pcbNameOut*  
 [Entrada/salida] Número total de bytes (excepto el byte de terminación null) se pasa o se devuelve en *lpszName*. Si el número de bytes disponible para devolver es mayor o igual que *cbNameMax*, el nombre del traductor en *lpszName* se trunca a *cbNameMax* menos el carácter de terminación NULL. El *pcbNameOut* argumento puede ser un puntero nulo.  
  
 *lpszPath*  
 [Salida] Ruta de acceso completa de la DLL de traducción.  
  
 *cbPathMax*  
 [Entrada] Longitud máxima de la *lpszPath* búfer.  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (excepto el byte de finalización en null) devuelven en *lpszPath*. Si el número de bytes disponible para devolver es mayor o igual que *cbPathMax*, la ruta de acceso del archivo DLL de traducción en *lpszPath* se trunca a *cbPathMax* menos el carácter de terminación NULL. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
 *pvOption*  
 Opción de traducción de 32 bits de [salida].  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcta y FALSE si se produce un error o si el usuario cancela el cuadro de diálogo.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetTranslator** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *cbNameMax* o *cbPathMax* argumento era menor o igual que 0.|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento era nulo o no válido.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszName* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de controlador o traductor|No se pudo cargar la biblioteca de traductor.|  
|ODBC_ERROR_INVALID_OPTION|Opción de transacción no válido|El *pvOption* argumento contiene un valor no válido.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Si *hwndParent* es null o si *lpszName*, *lpszPath*, o *pvOption* es un puntero nulo, **SQLGetTranslator** devuelve FALSE. En caso contrario, muestra la lista de traductores instalados en el siguiente cuadro de diálogo.  
  
 ![Cuadro de diálogo Seleccionar traductor](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Si *lpszName* contiene un nombre válido de traductor, está seleccionada. En caso contrario, \<traductor n > está seleccionada.  
  
 Si el usuario elige \<traductor n >, el contenido de *lpszName*, *lpszPath*, y *pvOption* no son modificadas. **SQLGetTranslator** establece *pcbNameOut* y *pcbPathOut* a 0 y devuelve TRUE.  
  
 Si el usuario elige un traductor, **SQLGetTranslator** llamadas **ConfigTranslator** en el programa de instalación del traductor DLL. Si **ConfigTranslator** devuelve un valor falso, **SQLGetTranslator** vuelve a su cuadro de diálogo. Si **ConfigTranslator** devuelve TRUE, **SQLGetTranslator** devuelve TRUE, junto con la opción de nombre, la ruta de acceso y la traducción de traductor seleccionado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Configurar un traductor|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtener un atributo de traducción|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de traducción|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
