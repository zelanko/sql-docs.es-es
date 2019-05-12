---
title: SQLWriteDSNToIni Function | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a36be7a98a39cab8b9df428b8d4bd9a1d399a1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536789"
---
# <a name="sqlwritedsntoini-function"></a>Función SQLWriteDSNToIni
**Conformidad**  
 Versión de introducción: ODBC 1.0  
  
 **Resumen**  
 **SQLWriteDSNToIni** agrega un origen de datos a la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDSN*  
 [Entrada] Nombre del origen de datos para agregar.  
  
 *lpszDriver*  
 [Entrada] Descripción del controlador (el nombre del DBMS asociado) presentada a los usuarios en lugar del nombre de controlador físico.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWriteDSNToIni** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El *lpszDSN* argumento contiene una cadena que no era válida para un DSN.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El *lpszDriver* argumento no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El programa de instalación no se pudo crear un DSN en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWriteDSNToIni** agrega el origen de datos a la sección [ODBC Data Sources] de la información del sistema. A continuación, crea una sección de la especificación del origen de datos y agrega una única palabra clave (**controlador**) con el nombre del controlador del archivo DLL como su valor. Si ya existe la sección de especificación del origen de datos, **SQLWriteDSNToIni** quita la sección anterior antes de crear uno nuevo.  
  
 El llamador de esta función debe agregar los valores y palabras clave específicas del controlador a la sección de especificación del origen de datos de la información del sistema.  
  
 Si el nombre del origen de datos es el predeterminado, **SQLWriteDSNToIni** también crea la sección de especificación del controlador predeterminado en la información del sistema.  
  
 Esta función se debe llamar solo desde un archivo DLL de configuración.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(en el archivo DLL de configuración)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Quitar un nombre de origen de datos de la información del sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
