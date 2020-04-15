---
title: Función SQLGetTranslator ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTranslator
helpviewer_keywords:
- SQLGetTranslator function [ODBC]
ms.assetid: 33879db3-5ef9-4585-9be5-69376157e017
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcd5aeebab8539b8b94db56ff30892f4a7dbbac1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303276"
---
# <a name="sqlgettranslator-function"></a>Función SQLGetTranslator
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **SQLGetTranslator** muestra un cuadro de diálogo desde el que un usuario puede seleccionar un traductor.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Identificador de ventana principal.  
  
 *lpszName*  
 [Entrada/Salida] Nombre del traductor de la información del sistema.  
  
 *cbNameMax*  
 [Entrada] Longitud máxima del búfer *lpszName.*  
  
 *pcbNameOut*  
 [Entrada/Salida] Número total de bytes (excluyendo el byte de terminación nula) pasados o devueltos en *lpszName*. Si el número de bytes disponibles para devolver es mayor o igual que *cbNameMax*, el nombre del traductor en *lpszName* se trunca en *cbNameMax* menos el carácter de terminación nula. El *argumento pcbNameOut* puede ser un puntero nulo.  
  
 *lpszPath*  
 [Salida] Ruta de acceso completa del archivo DLL de traducción.  
  
 *cbPathMax*  
 [Entrada] Longitud máxima del búfer *lpszPath.*  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (excluyendo el byte de terminación null) devueltos en *lpszPath*. Si el número de bytes disponibles para devolver es mayor o igual que *cbPathMax*, la ruta de acceso DLL de traducción en *lpszPath* se trunca a *cbPathMax* menos el carácter de terminación nula. El argumento *pcbPathOut* puede ser un puntero nulo.  
  
 *pvOption*  
 Opción de traducción de 32 bits [ Salida].  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error o si el usuario cancela el cuadro de diálogo.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetTranslator** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *cbNameMax* o *cbPathMax* era menor o igual que 0.|  
|ODBC_ERROR_INVALID_HWND|Mango de ventana no válido|El *hwndParent* argumento no era válido o NULL.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszName* no era válido. No se pudo encontrar en el registro.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de configuración del controlador o traductor|No se ha podido cargar la biblioteca de traductores.|  
|ODBC_ERROR_INVALID_OPTION|Opción de transacción no válida|El argumento *pvOption* contenía un valor no válido.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Si *hwndParent* es null o si *lpszName*, *lpszPath*o *pvOption* es un puntero nulo, **SQLGetTranslator** devuelve FALSE. De lo contrario, muestra la lista de traductores instalados en el siguiente cuadro de diálogo.  
  
 ![Cuadro de diálogo Seleccionar traductor](../../../odbc/reference/syntax/media/ch23j.gif "CH23J")  
  
 Si *lpszName* contiene un nombre de traductor válido, se selecciona. De \<lo contrario, no se selecciona> de traductor.  
  
 Si el usuario \<elige No Translator>, no se toca el contenido de *lpszName*, *lpszPath*y *pvOption.* **SQLGetTranslator** establece *pcbNameOut* y *pcbPathOut* en 0 y devuelve TRUE.  
  
 Si el usuario elige un traductor, **SQLGetTranslator** llama a **ConfigTranslator** en el archivo DLL de instalación del traductor. Si **ConfigTranslator** devuelve FALSE, **SQLGetTranslator** vuelve a su cuadro de diálogo. Si **ConfigTranslator** devuelve TRUE, **SQLGetTranslator** devuelve TRUE, junto con el nombre del traductor seleccionado, la ruta de acceso y la opción de traducción.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Configuración de un traductor|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Obtener un atributo de traducción|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de traducción|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
