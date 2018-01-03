---
title: "Función SQLRemoveTranslator | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRemoveTranslator
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveTranslator
helpviewer_keywords: SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9b076c209964110d2253681d97252ece25610ff
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlremovetranslator-function"></a>SQLRemoveTranslator (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLRemoveTranslator** quita información acerca de un traductor de la sección de Odbcinst.ini de la información del sistema y reduce contador de uso de componente del traductor en 1.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] El nombre del traductor como está registrado en la clave de Odbcinst.ini de la información del sistema.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de utilización del traductor después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveTranslator** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no pudo quitar la información de traductor porque no existía en el registro o no se encontró en el registro.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszTranslator* argumento no era válido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componente|El instalador no pudo reducir el recuento de uso del controlador.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveTranslator** complementa el [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) función y las actualizaciones de contar el uso del componente en la información del sistema. Esta función se debería llamar solo desde una aplicación de instalación.  
  
 **SQLRemoveTranslator** disminuye el contador de uso de componente en 1. Si el recuento de uso de componente llega a 0, se quitará la entrada de traductor de la información del sistema. La entrada de traductor está en la siguiente ubicación en la información del sistema, en el nombre del traductor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** realmente no elimina los archivos. El programa de llamada es responsable de eliminar los archivos y mantiene el recuento de uso de archivos. Solo una vez han alcanzado el recuento de utilización del componente y el recuento de uso de archivo cero es un archivo físicamente eliminado. Se pueden eliminar algunos archivos en un componente y otros usuarios eliminan no, dependiendo de si los archivos se usan para otras aplicaciones que se incrementan el contador de uso de archivo.  
  
 **SQLRemoveTranslator** también se llama como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y previamente instaló al controlador, se debe quitar y volver a instalar el controlador. **SQLRemoveTranslator** en primer lugar debe llamarse para disminuir el recuento de uso del componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el contador de uso del componente. El programa de instalación de la aplicación debe reemplazar físicamente los archivos antiguos con los nuevos archivos. El contador de uso de archivo seguirá siendo el mismo, y otras aplicaciones que usan los archivos de versiones anteriores ahora usará la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Instalar un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
