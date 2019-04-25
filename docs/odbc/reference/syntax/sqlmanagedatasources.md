---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f22fc952f0394f9e59ca8d67c76d0b00594b0759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62466021"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformidad**  
 Versión de introducción: ODBC 2.0  
  
 **Resumen**  
 **SQLManageDataSources** muestra un cuadro de diálogo con el que los usuarios pueden configurar, agregar y eliminar orígenes de datos en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwnd*  
 [Entrada] Identificador de la ventana primaria.  
  
## <a name="returns"></a>Devuelve  
 **SQLManageDataSources** devuelve FALSE si *hwnd* no es un identificador de ventana válido. En caso contrario, devuelve TRUE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLManageDataSources** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|La llamada a **ConfigDSN** error.|  
|ODBC_ERROR_INVALID__HWND|Identificador de ventana no válida|El *hwnd* argumento era NULL o no válido.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="managing-data-sources"></a>Administrar orígenes de datos  
 **SQLManageDataSources** muestra inicialmente la **Administrador de orígenes de datos ODBC** cuadro de diálogo, como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Administrador de orígenes de datos ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 El cuadro de diálogo muestra los orígenes de datos incluidos en la información del sistema en tres fichas: **DSN de usuario**, **DSN de sistema**, y **DSN de archivo**. Si el usuario hace doble clic en un origen de datos o selecciona un origen de datos y hace clic en **configurar**, **SQLManageDataSources** llamadas **ConfigDSN** en la configuración del archivo DLL con la ODBC_CONFIG_ Opción de DSN.  
  
 Si el usuario hace clic **agregar**, **SQLManageDataSources** muestra el **crear nuevo origen de datos** cuadro de diálogo, se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo nuevo origen de datos crear](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 El cuadro de diálogo muestra una lista de controladores instalados. Si el usuario hace doble clic en un controlador o selecciona un controlador y hace clic en **Aceptar**, **SQLManageDataSources** llamadas **ConfigDSN** en la configuración del archivo DLL y le pasa la opción ODBC_ADD_DSN.  
  
 Si el usuario selecciona un origen de datos y hace clic en **quitar**, **SQLManageDataSources** pide al usuario si desea eliminar el origen de datos. Si el usuario hace clic **Sí**, **SQLManageDataSources** llamadas **ConfigDSN** en el archivo DLL de configuración con la opción ODBC_REMOVE_DSN.  
  
 El **crear nuevo origen de datos** cuadro de diálogo se usa para agregar o eliminar un origen de datos de usuario, un origen de datos del sistema o un origen de datos de archivo.  
  
## <a name="user-dsns"></a>DSN de usuario  
 Los DSN que creó para usuarios individuales se llamará DSN de usuario, para distinguirlos de los DSN del sistema. DSN de usuario registrados como se indica a continuación en la información del sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSN del sistema  
 El **crear nuevo origen de datos** cuadro de diálogo le permite agregar un origen de datos del sistema para el equipo local o eliminar una, o para establecer la configuración de un origen de datos del sistema.  
  
 Un origen de datos configurado con un nombre de origen de datos del sistema (DSN) puede usarse por más de un usuario en el mismo equipo. También puede utilizarse por un servicio en todo el sistema, que, a continuación, se puede obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en la máquina.  
  
 Un DSN de sistema se registra en la entrada HKEY_LOCAL_MACHINE en la información del sistema en lugar de la entrada HKEY_CURRENT_USER. No está asociado a un usuario que inicia sesión con su nombre de usuario en particular y su contraseña, pero se puede usar cualquier usuario de la máquina o un servicio automático para todo el sistema. Sin embargo, es, vincular el DSN de sistema a una máquina. No se admite la capacidad de utilizar el DSN remotos entre equipos. Los DSN del sistema se registran como sigue en la información del sistema:  
  
 HKEY_LOCAL_MACHINE    SOFTWARE       ODBC          Odbc.ini  
  
## <a name="file-dsns"></a>DSN de archivo  
 Un origen de datos de archivo no tiene un nombre de origen de datos, como hace un origen de datos de la máquina y no está registrado en cualquier máquina o un usuario. La información de conexión para ese origen de datos se encuentra en un archivo de DSN que se puede copiar en cualquier equipo. Un origen de datos de archivo puede ser que se pueda compartir, en cuyo caso el archivo .dsn reside en una red y se puede utilizar simultáneamente varios usuarios en la red siempre y cuando el usuario tiene instalado el controlador apropiado. Un origen de datos de archivo también puede ser no se puede compartir, en cuyo caso puede utilizarse únicamente en una sola máquina.  
  
 Para obtener más información sobre los orígenes de datos de archivo, consulte [conecta orígenes de datos de archivo utilizando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), o vea [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Administración de los controladores  
 Si el usuario hace clic en el **controladores** pestaña en el **Administrador de orígenes de datos ODBC** cuadro de diálogo, **SQLManageDataSources** muestra una lista de controladores ODBC instalados en el sistema, así como información acerca de los controladores. La fecha que aparece es la fecha de creación del controlador, tal como se muestra en la siguiente ilustración.  
  
 ![Pestaña controladores de administrador de orígenes de datos ODBC](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opciones de traza  
 Si el usuario hace clic en el **seguimiento** pestaña en el **Administrador de orígenes de datos ODBC** cuadro de diálogo, **SQLManageDataSources** muestra las opciones de seguimiento, como se muestra en la siguiente ilustración.  
  
 ![Ficha trazas de administrador de orígenes de datos ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Si el usuario hace clic **Iniciar traza ahora** y, a continuación, hace clic en **Aceptar**, **SQLManageDataSources** habilita el seguimiento manual de todas las aplicaciones que se están ejecutando actualmente en la máquina.  
  
 Si el usuario especifica el nombre de un archivo de seguimiento en el **ruta de acceso del archivo de registro** cuadro de texto y, a continuación, hace clic en **Aceptar**, **SQLManageDataSources** establece la **TraceFile** palabra clave en la sección [ODBC] de la información del sistema para el nombre especificado.  
  
> [!IMPORTANT]  
>  Compatibilidad con Visual Studio Analyzer se quitó a partir de Windows 8 (Visual Studio Analyzer sólo se incluyó en versiones anteriores de Visual Studio.). Para conocer una alternativa mecanismo de solución de problemas, use el seguimiento BID.  
  
 Si el usuario hace clic **iniciar Visual Studio Analyzer** y, a continuación, hace clic en **Aceptar**, Visual Studio Analyzer está habilitada. Permanece habilitado hasta que **Detener Visual Studio Analyzer** se hace clic en.  
  
 Para obtener más información sobre el seguimiento, vea [seguimiento](../../../odbc/reference/develop-app/tracing.md). Para obtener más información sobre la **seguimiento** y **TraceFile** palabras clave, consulte [subclave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Crear orígenes de datos|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
