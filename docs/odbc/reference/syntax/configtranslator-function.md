---
title: Función ConfigTranslator | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edcffe36c0185276fae89f800e1bbcfc5bc33b33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232022"
---
# <a name="configtranslator-function"></a>Función ConfigTranslator
**Conformidad**  
 Versión de introducción: ODBC 2.0  
  
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
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador es null.  
  
 *pvOption*  
 [Salida] Una opción de traducción de 32 bits.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **ConfigTranslator** devuelve FALSE, un asociado  *\*pfErrorCode* valor se registra en el búfer de error del instalador mediante una llamada a **SQLPostInstallerError**y se puede obtener mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válida|El *hwndParent* argumento era NULL o no válido.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Un error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *SzError* argumento en una llamada a la **SQLPostInstallerError** función debe contener el mensaje de error específico del controlador.|  
|ODBC_ERROR_INVALID_OPTION|Opción de conversión no válida|El *pvOption* argumento contiene un valor no válido.|  
  
## <a name="comments"></a>Comentarios  
 Si el traductor admite solo una opción de traducción, **ConfigTranslator** devuelve TRUE y establece *pvOption* a la opción de 32 bits. En caso contrario, determina la opción de traducción predeterminado para usar. **ConfigTranslator** puede mostrar un cuadro de diálogo con el que un usuario selecciona una opción de traducción predeterminado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de una opción de traducción|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Seleccionar un traductor|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Establecer una opción de traducción|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
