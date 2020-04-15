---
title: Función SQLWriteDSNToIni ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bb141c8f54c49ca3a5c6fc4bc15d434f91795c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286965"
---
# <a name="sqlwritedsntoini-function"></a>Función SQLWriteDSNToIni
**Conformidad**  
 Versión introducida: ODBC 1.0  
  
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
 [Entrada] Nombre del origen de datos que se va a agregar.  
  
 *lpszDriver*  
 [Entrada] Descripción del controlador (normalmente el nombre del DBMS asociado) presentada a los usuarios en lugar del nombre del controlador físico.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLWriteDSNToIni** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El argumento *lpszDSN* contenía una cadena que no era válida para un DSN.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszDriver* no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El instalador no pudo crear un DSN en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWriteDSNToIni** agrega el origen de datos a la sección [Orígenes de datos ODBC] de la información del sistema. A continuación, crea una sección de especificación para el origen de datos y agrega una sola palabra clave (**Driver**) con el nombre del archivo DLL del controlador como su valor. Si la sección de especificación del origen de datos ya existe, **SQLWriteDSNToIni** quita la sección anterior antes de crear la nueva.  
  
 El llamador de esta función debe agregar cualquier palabra clave y valores específicos del controlador a la sección de especificación del origen de datos de la información del sistema.  
  
 Si el nombre del origen de datos es Predeterminado, **SQLWriteDSNToIni** también crea la sección de especificación de controlador predeterminada en la información del sistema.  
  
 Esta función debe llamarse sólo desde un archivo DLL de instalación.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(en el archivo DLL de instalación)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Eliminación de un nombre de origen de datos de la información del sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
