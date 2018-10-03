---
title: Función SQLPostInstallerError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dc70580de4f759a5adb6a501ac5dc200b62cba5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716663"
---
# <a name="sqlpostinstallererror-function"></a>Función SQLPostInstallerError
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLPostInstallerError** proporciona un mecanismo para una biblioteca de configuración de traductor o controlador para informar de errores para el **ConfigDriver**, **ConfigDSN**, y **ConfigTranslator**  funciones a la cola de errores del instalador. Aplicaciones no utilizan esta API; usan **SQLInstallerError** para recuperar el error.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *fErrorCode*  
 [Entrada] Código de error del instalador.  
  
 *szErrorMsg*  
 [Entrada] Texto del mensaje de error.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLPostInstallerError** no registra los valores de error para sí mismo. Si el error se ha registrado correctamente a la cola de errores de instalador (recuperables mediante **SQLInstallerError**), se devuelve SQL_SUCCESS. Se devolverá SQL_ERROR si el valor de la *dwErrorCode* argumento no es uno de los códigos de error del instalador especificado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Agregar, modificar o quitar orígenes de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Establecer una opción de traducción|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
