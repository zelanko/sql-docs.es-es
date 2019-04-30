---
title: Función SQLRemoveDriver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ef98000391ec6c39012603795b7f11a34c68183
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185993"
---
# <a name="sqlremovedriver-function"></a>Función SQLRemoveDriver
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLRemoveDriver** cambia o quita la información sobre el controlador de la entrada de Odbcinst.ini en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] El nombre del controlador como registrado en la clave de Odbcinst.ini la información del sistema.  
  
 *fRemoveDSN*  
 [Entrada] Los valores válidos son:  
  
 TRUE: Quitar asociado con el controlador especificado en el DSN *lpszDriver*. FALSE: No quite los DSN asociados con el controlador especificado en *lpszDriver*.  
  
 *lpdwUsageCount*  
 [Salida] El contador de uso del controlador después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveDriver** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no pudo quitar la información del controlador porque no existía en el registro o no se encontró en el registro.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El *lpszDriver* argumento no era válido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de utilización de componente|El instalador no pudo reducir el recuento de uso del controlador.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|El *fRemoveDSN* argumento era TRUE; sin embargo, no se pudieron quitar uno o varios de los DSN. La llamada a **SQLConfigDriver** con la solicitud ODBC_REMOVE_DRIVER generado un error.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDriver** complementa el [SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) función y las actualizaciones de contar el uso de componentes en la información del sistema. Esta función debe llamarse únicamente desde una aplicación de instalación.  
  
 **SQLRemoveDriver** reducirá el valor de recuento de uso de componentes en 1. Si el recuento de uso de componente llega a 0, sucederá lo siguiente:  
  
1.  El **SQLConfigDriver** se llamará la función con la opción ODBC_REMOVE_DRIVER. Si el *fRemoveDSN* opción está establecida en TRUE, el **ConfigDSN** llamadas de función **SQLRemoveDSNFromIni** para quitar todos los orígenes de datos asociados con el controlador especificado en *lpszDriver.* Si el *fRemoveDSN* opción está establecida en FALSE, no se eliminarán los orígenes de datos.  
  
2.  Se quitará la entrada del controlador en la información del sistema. La entrada del controlador está en la siguiente ubicación de información del sistema, en el nombre del controlador:  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **SQLRemoveDriver** no elimina los archivos. El programa de llamada es responsable de eliminar archivos y mantener el contador de uso de archivo. Solo después de que han alcanzado el recuento de utilización del componente y el recuento de uso de archivo cero es un archivo físicamente eliminado. Se pueden eliminar algunos archivos en un componente y otros usuarios eliminan no, dependiendo de si se usan los archivos por otras aplicaciones que se incrementan el contador de uso de archivo.  
  
 **SQLRemoveDriver** también se denomina como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y que previamente haya instalado al controlador, se debe quitar y volver a instalar el controlador. **SQLRemoveDriver** en primer lugar debe llamarse para reducir el recuento de uso de componente y, a continuación, **SQLInstallDriverEx** debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar los antiguos archivos con los nuevos archivos. El recuento de uso de archivos seguirán siendo las mismas y otras aplicaciones que usan archivos de la versión anterior, ahora se usarán la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un controlador|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md) (en el archivo DLL de configuración)|  
|Agregar, modificar o quitar un controlador|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|Instalar un controlador|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
