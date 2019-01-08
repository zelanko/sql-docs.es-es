---
title: Función SQLRemoveDriverManager | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriverManager
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriverManager
helpviewer_keywords:
- SQLRemoveDriverManager function function [ODBC]
ms.assetid: 3a41511f-6603-4b81-a815-7883874023c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4949d84f75483bd4379366621e4a8921d9b4de39
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206664"
---
# <a name="sqlremovedrivermanager-function"></a>Función SQLRemoveDriverManager
**Conformidad**  
 Versión de introducción: ODBC 3.0: En desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y los sistemas operativos posteriores.  
  
 **Resumen**  
 **SQLRemoveDriverManager** cambia o quita la información acerca de los componentes principales ODBC de la entrada de Odbcinst.ini en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Salida] El contador de uso del Administrador de controladores después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveDriverManager** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no pudo quitar la información del Administrador de controladores porque no existía en el registro o no se encontró en el registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de utilización de componente|El instalador no pudo reducir el recuento de uso del Administrador de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDriverManager** complementa el **SQLInstallDriverManager** función y el uso de componentes se cuentan en la información del sistema de las actualizaciones. Esta función debe llamarse únicamente desde una aplicación de instalación.  
  
 **SQLRemoveDriverManager** reducirá el recuento de uso del componente de núcleos en 1. Si el recuento de utilización del componente llega a 0, se quitará la información del sistema de entrada. La entrada del componente principal está en la siguiente ubicación en la información del sistema, bajo el título "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Una aplicación no debería quitar físicamente los archivos del Administrador de controladores cuando el recuento de utilización del componente y el recuento de uso de archivo llegue a cero.  
  
 **SQLRemoveDriverManager** no elimina los archivos. El programa que realiza la llamada es responsable de eliminar los archivos y mantener el uso del archivo de cuenta. Los archivos del Administrador de controladores no se debe, sin embargo, se puede quitar cuando el recuento de utilización del componente y el recuento de uso de archivo han alcanzado el cero, porque estos archivos pueden utilizarse por otras aplicaciones que no se incrementan el contador de uso de archivo.  
  
 **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación. Se desinstalan los componentes principales de ODBC (que incluyen el Administrador de controladores, biblioteca de cursores, instalador, biblioteca de lenguaje, administrador, thunk archivos etc.) como un todo. Los siguientes archivos no están quitan cuando **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. ARCHIVO DLL|  
|ODBCCR32. ARCHIVO DLL|ODBC16GT. ARCHIVO DLL|  
|ODBCCU32. ARCHIVO DLL|ODBC32GT. ARCHIVO DLL|  
|ODBCINT. ARCHIVO DLL|DS16GT. ARCHIVO DLL|  
|ODBCTRAC. ARCHIVO DLL|DS32GT. ARCHIVO DLL|  
|MSVCRT40. ARCHIVO DLL|ODBCAD32. EXE|  
|ODBCCP32. CPL||  
  
 **SQLRemoveDriverManager** también se denomina como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y que previamente haya instalado al controlador, se debe quitar y volver a instalar el controlador.  
  
 **SQLRemoveDriverManager** en primer lugar debe llamarse para reducir el recuento de uso del componente. **SQLInstallDriverEx** , a continuación, debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar los archivos del componente principal antiguo con los nuevos archivos. Los recuentos de uso de archivos seguirán siendo las mismas y otras aplicaciones que usan los archivos de componente de core versión anterior, ahora se usarán archivos de la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Instalación de un administrador de controladores|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
