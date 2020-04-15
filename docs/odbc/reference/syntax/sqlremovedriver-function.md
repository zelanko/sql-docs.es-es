---
title: Función SQLRemoveDriver ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205c5b46e5f6cea195094f7a50e81d7509927d1a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303936"
---
# <a name="sqlremovedriver-function"></a>Función SQLRemoveDriver
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLRemoveDriver** cambia o quita información sobre el controlador de la odbcinst.ini entrada en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] El nombre del controlador registrado en la clave Odbcinst.ini de la información del sistema.  
  
 *fRemoveDSN*  
 [Entrada] Los valores válidos son:  
  
 TRUE: quite los DSN asociados al controlador especificado en *lpszDriver*. FALSE: no quite los DSN asociados con el controlador especificado en *lpszDriver*.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de uso del controlador después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRemoveDriver** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente no encontrado en el registro|El instalador no pudo quitar la información del controlador porque no existía en el registro o no se pudo encontrar en el registro.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszDriver* no era válido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componentes|El instalador no pudo disminuir el recuento de uso del controlador.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El *fRemoveDSN* argumento era TRUE; sin embargo, uno o más DSN no se pudieron eliminar. Error en la llamada a **SQLConfigDriver** con la solicitud ODBC_REMOVE_DRIVER.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDriver** complementa la función [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) y actualiza el recuento de uso de componentes en la información del sistema. Esta función debe llamarse sólo desde una aplicación de instalación.  
  
 **SQLRemoveDriver** reducirá el valor de recuento de uso del componente en 1. Si el recuento de uso de componentes va a 0, se producirá lo siguiente:  
  
1.  Se llamará a la función **SQLConfigDriver** con la opción ODBC_REMOVE_DRIVER. Si la opción *fRemoveDSN* está establecida en TRUE, la función **ConfigDSN** llama a **SQLRemoveDSNFromIni** para quitar todos los orígenes de datos asociados con el controlador especificado en *lpszDriver.* Si la opción *fRemoveDSN* está establecida en FALSE, los orígenes de datos no se eliminarán.  
  
2.  Se eliminará la entrada del controlador en la información del sistema. La entrada del controlador se encuentra en la siguiente ubicación de información del sistema, bajo el nombre del controlador:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** no quita realmente ningún archivo. El programa de llamada es responsable de eliminar archivos y mantener el recuento de uso de archivos. Sólo después de que el recuento de uso de componentes y el recuento de uso de archivos hayan alcanzado cero, se eliminará físicamente un archivo. Algunos archivos de un componente se pueden eliminar y otros no, dependiendo de si los archivos son utilizados por otras aplicaciones que han incrementado el recuento de uso de archivos.  
  
 **SQLRemoveDriver** también se llama como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y ha instalado previamente el controlador, el controlador debe quitarse y, a continuación, volver a instalarlo. **SQLRemoveDriver** primero debe llamarse para disminuir el recuento de uso de componentes y, a continuación, **SQLInstallDriverEx** debe llamarse para incrementar el recuento de uso de componentes. El programa de instalación de la aplicación debe reemplazar los archivos antiguos con los nuevos archivos. El recuento de uso de archivos seguirá siendo el mismo, y otras aplicaciones que usan los archivos de la versión anterior ahora usarán la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (en el archivo DLL de instalación)|  
|Agregar, modificar o quitar un controlador|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalación de un controlador|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
