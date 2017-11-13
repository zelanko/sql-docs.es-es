---
title: "Función ConfigTranslator | Documentos de Microsoft"
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
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9de00042d81ac74bbda54be2060a331cf1ac3ad
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="configtranslator-function"></a>ConfigTranslator (función)
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **ConfigTranslator** devuelve una opción de traducción predeterminado para un traductor. Puede estar en el traductor de DLL o un archivo DLL de configuración independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador no es null.  
  
 *pvOption*  
 [Salida] Una opción de traducción de 32 bits.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **ConfigTranslator** devuelve FALSE, un asociado  *\*pfErrorCode* valor se registra en el búfer de error del instalador mediante una llamada a **SQLPostInstallerError**y puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento era nulo o no válido.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Un error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *SzError* argumento en una llamada a la **SQLPostInstallerError** función debe contener el mensaje de error específico del controlador.|  
|ODBC_ERROR_INVALID_OPTION|Opción de conversión no válida|El *pvOption* argumento contiene un valor no válido.|  
  
## <a name="comments"></a>Comentarios  
 Si el traductor admite solo una opción de traducción, **ConfigTranslator** devuelve TRUE y establece *pvOption* a la opción de 32 bits. En caso contrario, determina la opción de traducción predeterminado para usar. **ConfigTranslator** puede mostrar un cuadro de diálogo con el que un usuario selecciona una opción de traducción predeterminado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de una opción de traducción|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Al seleccionar un traductor|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Establecer una opción de traducción|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|

