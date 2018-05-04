---
title: Función SQLRemoveDriverManager | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ba1ba5d7f84da500f3887bf1684523f5501e9b1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedrivermanager-function"></a>SQLRemoveDriverManager (función)
**Conformidad**  
 Versión presentado: ODBC 3.0: en desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y sistemas operativos posteriores.  
  
 **Resumen**  
 **SQLRemoveDriverManager** cambia o quita la información acerca de los componentes principales ODBC de la entrada de Odbcinst.ini en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Salida] El contador de uso del Administrador de controladores después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLRemoveDriverManager** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|No se encuentra en el registro de componente|El programa de instalación no pudo quitar la información del Administrador de controladores porque no existía en el registro o no se encontró en el registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componente|El instalador no pudo reducir el recuento de uso del Administrador de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDriverManager** complementa el **SQLInstallDriverManager** función y las actualizaciones que el componente contador de uso de la información del sistema. Esta función se debería llamar solo desde una aplicación de instalación.  
  
 **SQLRemoveDriverManager** disminuye el recuento de uso del componente de núcleos en 1. Si el recuento de uso de componente llega a 0, se quitará la información del sistema de entrada. La entrada del componente principal está en la ubicación siguiente en la información del sistema, bajo el título "Núcleo de ODBC":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Una aplicación no debería quitar físicamente los archivos de administrador de controladores cuando el recuento de utilización del componente y el recuento de uso de archivo llegue a cero.  
  
 **SQLRemoveDriverManager** realmente no elimina los archivos. El programa de llamada es responsable de eliminar los archivos y recuentos de mantener el uso de archivos. Archivos de administrador de controladores no se debe, sin embargo, puede quitar cuando el recuento de utilización del componente y el recuento de uso de archivo llega a cero, porque estos archivos pueden usarse por otras aplicaciones que no se incrementan el contador de uso de archivo.  
  
 **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación. Se desinstalarán los componentes principales de ODBC (que incluyen el Administrador de controladores, biblioteca de cursores, instalador, biblioteca de lenguaje, administrador, archivos thunk y así sucesivamente) como un todo. Los siguientes archivos no están quitan cuando **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. ARCHIVO DLL|  
|ODBCCR32. ARCHIVO DLL|ODBC16GT. ARCHIVO DLL|  
|ODBCCU32. ARCHIVO DLL|ODBC32GT. ARCHIVO DLL|  
|ODBCINT. ARCHIVO DLL|DS16GT. ARCHIVO DLL|  
|ODBCTRAC. ARCHIVO DLL|DS32GT. ARCHIVO DLL|  
|MSVCRT40. ARCHIVO DLL|ODBCAD32. EXE|  
|ODBCCP32. CPL||  
  
 **SQLRemoveDriverManager** también se llama como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y previamente instaló al controlador, se debe quitar y volver a instalar el controlador.  
  
 **SQLRemoveDriverManager** en primer lugar debe llamarse para disminuir el recuento de uso del componente. **SQLInstallDriverEx** , a continuación, se debe llamar para incrementar el contador de uso del componente. El programa de instalación de la aplicación debe reemplazar los archivos del componente principal antiguo con los nuevos archivos. Los recuentos de uso de archivo seguirá siendo el mismo, y otras aplicaciones que usan los archivos de componente de núcleo de versión anteriores ahora utilizará los archivos de la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Instalación de un administrador de controladores|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
