---
title: Función SQLRemoveTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveTranslator
helpviewer_keywords:
- SQLRemoveTranslator function [ODBC]
ms.assetid: c6feda49-0359-4224-8de9-77125cf2397b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf81d013ccf449288791b1875752d5b6067770a1
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207604"
---
# <a name="sqlremovetranslator-function"></a>Función SQLRemoveTranslator
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLRemoveTranslator** quita información acerca de un traductor de desde la sección de Odbcinst.ini de la información del sistema y disminuye el contador de uso de componente del traductor por 1.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] El nombre del traductor como registrado en la clave de Odbcinst.ini la información del sistema.  
  
 *lpdwUsageCount*  
 [Salida] El contador de uso del traductor después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveTranslator** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no pudo quitar la información de traductor porque no existía en el registro o no se encontró en el registro.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El *lpszTranslator* argumento no era válido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de utilización de componente|El instalador no pudo reducir el recuento de uso del controlador.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveTranslator** complementa el [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) función y las actualizaciones de contar el uso de componentes en la información del sistema. Esta función debe llamarse únicamente desde una aplicación de instalación.  
  
 **SQLRemoveTranslator** reducirá el recuento de utilización del componente en 1. Si el recuento de utilización del componente llega a 0, se quitará la entrada de traductor de la información del sistema. La entrada del traductor está en la siguiente ubicación en la información del sistema, en el nombre del traductor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** no elimina los archivos. El programa de llamada es responsable de eliminar archivos y mantener el contador de uso de archivo. Solo después de que han alcanzado el recuento de utilización del componente y el recuento de uso de archivo cero es un archivo físicamente eliminado. Se pueden eliminar algunos archivos en un componente y otros usuarios eliminan no, dependiendo de si se usan los archivos por otras aplicaciones que se incrementan el contador de uso de archivo.  
  
 **SQLRemoveTranslator** también se denomina como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y que previamente haya instalado al controlador, se debe quitar y volver a instalar el controlador. **SQLRemoveTranslator** en primer lugar debe llamarse para reducir el recuento de uso de componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar físicamente los archivos antiguos con los nuevos archivos. El recuento de uso de archivos seguirán siendo las mismas y otras aplicaciones que usan archivos de la versión anterior, ahora se usarán la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Instalación de un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
