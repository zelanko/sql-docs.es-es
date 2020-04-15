---
title: Función SQLRemoveDriverManager ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 27b32c1c4e0f3f4d5359af287ba07d40b033af00
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301816"
---
# <a name="sqlremovedrivermanager-function"></a>Función SQLRemoveDriverManager
**Conformidad**  
 Versión introducida: ODBC 3.0: en desuso en Windows XP Service Pack 2, Windows Server 2003 Service Pack 1 y sistemas operativos posteriores.  
  
 **Resumen**  
 **SQLRemoveDriverManager** cambia o quita información sobre los componentes principales ODBC de la odbcinst.ini entrada en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveDriverManager(  
     LPDWORD     pdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *pdwUsageCount*  
 [Salida] El recuento de uso del Administrador de controladores después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRemoveDriverManager** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente no encontrado en el registro|El instalador no pudo quitar la información del Administrador de controladores porque no existía en el registro o no se pudo encontrar en el registro.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componentes|El instalador no pudo disminuir el recuento de uso del Administrador de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveDriverManager** complementa la función **SQLInstallDriverManager** y actualiza el recuento de uso de componentes en la información del sistema. Esta función debe llamarse sólo desde una aplicación de instalación.  
  
 **SQLRemoveDriverManager** reducirá el recuento de uso del componente principal en 1. Si el recuento de uso de componentes va a 0, se eliminará la información del sistema de entrada. La entrada del componente principal se encuentra en la siguiente ubicación en la información del sistema, bajo el título "ODBC Core":  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
> [!CAUTION]  
>  Una aplicación no debe eliminar físicamente los archivos del Administrador de controladores cuando el recuento de uso de componentes y el recuento de uso de archivos alcanzan cero.  
  
 **SQLRemoveDriverManager** no quita realmente ningún archivo. El programa que realiza la llamada es responsable de eliminar archivos y mantener los recuentos de uso de archivos. Sin embargo, los archivos del Administrador de controladores no deben eliminarse cuando el recuento de uso de componentes y el recuento de uso de archivos han alcanzado cero, ya que estos archivos pueden ser utilizados por otras aplicaciones que no han incrementado el recuento de uso de archivos.  
  
 **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación. Los componentes principales de ODBC (que incluyen el Administrador de controladores, la biblioteca de cursores, el instalador, la biblioteca de idiomas, el administrador, los archivos thunking, etc.) se desinstalan como un todo. Los siguientes archivos no se quitan cuando **SQLRemoveDriverManager** se llama como parte del proceso de desinstalación:  
  
|||  
|-|-|  
|ODBC32DLL|ODBCCP32. Dll|  
|ODBCCR32. Dll|ODBC16GT. Dll|  
|ODBCCU32. Dll|ODBC32GT. Dll|  
|Odbcint. Dll|DS16GT. Dll|  
|ODBCTRAC. Dll|DS32GT. Dll|  
|MSVCRT40. Dll|ODBCAD32. Exe|  
|ODBCCP32. Cpl||  
  
 **SQLRemoveDriverManager** también se llama como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y ha instalado previamente el controlador, el controlador debe quitarse y, a continuación, volver a instalarlo.  
  
 **SQLRemoveDriverManager** primero debe llamarse para disminuir el recuento de uso de componentes. **SQLInstallDriverEx,** a continuación, debe llamarse para aumentar el recuento de uso de componentes. El programa de instalación de la aplicación debe reemplazar los archivos de componentes principales antiguos con los nuevos archivos. Los recuentos de uso de archivos seguirán siendo los mismos, y otras aplicaciones que utilizan los archivos de componentes principales de la versión anterior ahora usarán los archivos de versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Instalación de un gestor de controladores|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
