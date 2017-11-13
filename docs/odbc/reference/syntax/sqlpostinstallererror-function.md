---
title: "Función SQLPostInstallerError | Documentos de Microsoft"
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
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f7d3a6bec7c12e271c073d5665c0a4e9b227ceef
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLPostInstallerError** proporciona un mecanismo para una biblioteca del programa de instalación de controlador o traductor para informar de errores para el **ConfigDriver**, **ConfigDSN**, y **ConfigTranslator**  funciones a la cola de error del instalador. Las aplicaciones no usan esta API; usan **SQLInstallerError** para recuperar el error.  
  
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
 **SQLPostInstallerError** no publica valores de error para sí mismo. Si el error se ha registrado correctamente a la cola de errores de instalador (usando recuperables **SQLInstallerError**), se devuelve SQL_SUCCESS. Se devolverá SQL_ERROR si el valor de la *dwErrorCode* argumento no es uno de los códigos de error del instalador especificado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|Agregar, modificar o quitar orígenes de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|Establecer una opción de traducción|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|

