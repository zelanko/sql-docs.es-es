---
title: Función SQLWriteDSNToIni | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a1ee3bdbdc14c01bf267c9dbb64ef10c93dfe1a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918170"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni (función)
**Conformidad**  
 Versión introdujo: ODBC 1.0  
  
 **Resumen**  
 **SQLWriteDSNToIni** agrega un origen de datos a la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWriteDSNToIni** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El *lpszDSN* argumento contenía una cadena que no era válida para un DSN.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszDriver* argumento no era válido.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El programa de instalación no pudo crear un DSN en el registro.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWriteDSNToIni** agrega el origen de datos a la sección [ODBC Data Sources] de la información del sistema. A continuación, se crea una sección de la especificación del origen de datos y se agrega una única palabra clave (**controlador**) con el nombre del controlador del archivo DLL como su valor. Si ya existe la sección de especificación del origen de datos, **SQLWriteDSNToIni** quita la sección anterior antes de crear uno nuevo.  
  
 El autor de llamada de esta función debe agregar los valores y palabras clave específicas del controlador a la sección de especificación del origen de datos de la información del sistema.  
  
 Si el nombre del origen de datos es el predeterminado, **SQLWriteDSNToIni** también crea la sección predeterminada de la especificación de controlador en la información del sistema.  
  
 Esta función se debería llamar solo desde un archivo DLL de configuración.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)(en la configuración del archivo DLL)|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Quitar un nombre de origen de datos de la información del sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
