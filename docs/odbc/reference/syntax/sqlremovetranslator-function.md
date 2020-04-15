---
title: Función SQLRemoveTranslator ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 348d2c5da0731ba88ccd4dd6406d3754890f7906
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301792"
---
# <a name="sqlremovetranslator-function"></a>Función SQLRemoveTranslator
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLRemoveTranslator** elimina la información sobre un traductor de la sección Odbcinst.ini de la información del sistema y disminuye el recuento de uso de componentes del traductor en 1.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLRemoveTranslator(  
     LPCSTR    lpszTranslator,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszTranslator*  
 [Entrada] El nombre del traductor registrado en la clave Odbcinst.ini de la información del sistema.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de uso del traductor después de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLRemoveTranslator** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|Componente no encontrado en el registro|El instalador no pudo eliminar la información del traductor porque no existía en el registro o no se encontraba en el registro.|  
|ODBC_ERROR_INVALID_NAME|Nombre de controlador o traductor no válido|El argumento *lpszTranslator* no era válido.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componentes|El instalador no pudo disminuir el recuento de uso del controlador.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLRemoveTranslator** complementa la función [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md) y actualiza el recuento de uso de componentes en la información del sistema. Esta función debe llamarse sólo desde una aplicación de instalación.  
  
 **SQLRemoveTranslator** reducirá el recuento de uso de componentes en 1. Si el recuento de uso de componentes va a 0, se eliminará la entrada del traductor en la información del sistema. La entrada del traductor se encuentra en la siguiente ubicación en la información del sistema, bajo el nombre del traductor:  
  
 `HKEY_LOCAL_MACHINE`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbcinst.ini`  
  
 **SQLRemoveTranslator** no elimina realmente ningún archivo. El programa de llamada es responsable de eliminar archivos y mantener el recuento de uso de archivos. Sólo después de que el recuento de uso de componentes y el recuento de uso de archivos hayan alcanzado cero, se eliminará físicamente un archivo. Algunos archivos de un componente se pueden eliminar y otros no, dependiendo de si los archivos son utilizados por otras aplicaciones que han incrementado el recuento de uso de archivos.  
  
 **SQLRemoveTranslator** también se llama como parte de un proceso de actualización. Si una aplicación detecta que tiene que realizar una actualización y ha instalado previamente el controlador, el controlador debe quitarse y, a continuación, volver a instalarlo. **SQLRemoveTranslator** primero debe llamarse para disminuir el recuento de uso del componente y, a continuación, **SQLInstallTranslatorEx** debe llamarse para incrementar el recuento de uso del componente. El programa de instalación de la aplicación debe reemplazar físicamente los archivos antiguos con los nuevos archivos. El recuento de uso de archivos seguirá siendo el mismo, y otras aplicaciones que usan los archivos de la versión anterior ahora usarán la versión más reciente.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Instalación de un traductor|[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|
