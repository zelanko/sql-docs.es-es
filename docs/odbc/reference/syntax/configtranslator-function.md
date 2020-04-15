---
title: Función ConfigTranslator (ConfigTranslator) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306036"
---
# <a name="configtranslator-function"></a>Función ConfigTranslator
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **ConfigTranslator** devuelve una opción de traducción predeterminada para un traductor. Puede estar en el archivo DLL del traductor o en un archivo DLL de instalación independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de ventana principal. La función no mostrará ningún cuadro de diálogo si el identificador es null.  
  
 *pvOption*  
 [Salida] Una opción de traducción de 32 bits.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **ConfigTranslator** devuelve FALSE, se registra un valor * \*pfErrorCode* asociado en el búfer de errores del instalador mediante una llamada a **SQLPostInstallerError** y se puede obtener llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Mango de ventana no válido|El *hwndParent* argumento no era válido o NULL.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *Argumento SzError de* una llamada a la función **SQLPostInstallerError** debe contener el mensaje de error específico del controlador.|  
|ODBC_ERROR_INVALID_OPTION|Opción de traducción no válida|El argumento *pvOption* contenía un valor no válido.|  
  
## <a name="comments"></a>Comentarios  
 Si el traductor solo admite una única opción de traducción, **ConfigTranslator** devuelve TRUE y establece *pvOption* en la opción de 32 bits. De lo contrario, determina la opción de traducción predeterminada que se va a utilizar. **ConfigTranslator** puede mostrar un cuadro de diálogo con el que un usuario selecciona una opción de traducción predeterminada.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtener una opción de traducción|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Selección de un traductor|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Configuración de una opción de traducción|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
