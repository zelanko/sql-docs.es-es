---
title: SQLManageDataSources ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290223"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **SQLManageDataSources** muestra un cuadro de diálogo con el que los usuarios pueden configurar, agregar y eliminar orígenes de datos en la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwnd*  
 [Entrada] Identificador de ventana principal.  
  
## <a name="returns"></a>Devuelve  
 **SQLManageDataSources** devuelve FALSE si *hwnd* no es un identificador de ventana válido. De lo contrario, devuelve TRUE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLManageDataSources** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitud* fallida|Error en la llamada a **ConfigDSN.**|  
|ODBC_ERROR_INVALID__HWND|Mango de ventana no válido|El *hwnd* argumento no era válido o NULL.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="managing-data-sources"></a>Administrar orígenes de datos  
 **SQLManageDataSources** muestra inicialmente el cuadro de diálogo Administrador de orígenes de **datos ODBC,** como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Administrador de ODBC de origen de datos](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 El cuadro de diálogo muestra los orígenes de datos enumerados en la información del sistema en tres fichas: **DSN de**usuario , **DSN**de sistema y **DSN**de archivo . Si el usuario hace doble clic en un origen de datos o selecciona un origen de datos y hace clic en **Configurar**, **SQLManageDataSources** llama a **ConfigDSN** en el archivo DLL de instalación con la opción ODBC_CONFIG_DSN.  
  
 Si el usuario hace clic en **Agregar**, **SQLManageDataSources** muestra el cuadro de diálogo Crear nuevo origen de **datos,** que se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Crear un nuevo origen de datos](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 El cuadro de diálogo muestra una lista de controladores instalados. Si el usuario hace doble clic en un controlador o selecciona un controlador y hace clic en Aceptar , **SQLManageDataSources** llama **a** **ConfigDSN** en el archivo DLL de instalación y le pasa la opción ODBC_ADD_DSN.  
  
 Si el usuario selecciona un origen de datos y hace clic en **Quitar**, **SQLManageDataSources** le pregunta si el usuario desea eliminar el origen de datos. Si el usuario hace clic en **Sí**, **SQLManageDataSources** llama a **ConfigDSN** en el archivo DLL de instalación con la opción ODBC_REMOVE_DSN.  
  
 El cuadro de diálogo **Crear nuevo origen** de datos se utiliza para agregar o eliminar un origen de datos de usuario, un origen de datos del sistema o un origen de datos de archivo.  
  
## <a name="user-dsns"></a>DSN de usuario  
 Los DSN creados para usuarios individuales se denominarán DSN de usuario, para distinguirlos de los DSN del sistema. Los DSN de usuario se registran de la siguiente manera en la información del sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSN del sistema  
 El cuadro de diálogo **Crear nuevo origen** de datos permite agregar un origen de datos del sistema al equipo local o eliminar uno, o establecer la configuración de un origen de datos del sistema.  
  
 Más de un usuario puede utilizar un origen de datos configurado con un nombre de origen de datos del sistema (DSN) en el mismo equipo. También puede ser utilizado por un servicio de todo el sistema, que puede obtener acceso al origen de datos incluso si ningún usuario ha iniciado sesión en el equipo.  
  
 Un DSN del sistema se registra en la entrada HKEY_LOCAL_MACHINE en la información del sistema en lugar de en la entrada HKEY_CURRENT_USER. No está vinculado a un usuario que inicia sesión con su nombre de usuario y contraseña particular, pero puede ser utilizado por cualquier usuario de esa máquina o por un servicio automático en todo el sistema. Sin embargo, el DSN del sistema está atado a una máquina. No admite la capacidad de utilizar DSN remotos entre máquinas. Los DSN del sistema se registran de la siguiente manera en la información del sistema:  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>DSN de archivo  
 Un origen de datos de archivo no tiene un nombre de origen de datos, al igual que un origen de datos de máquina, y no está registrado en ningún usuario o equipo. La información de conexión de ese origen de datos se encuentra en un archivo .dsn que se puede copiar en cualquier equipo. Un origen de datos de archivo puede ser compartible, en cuyo caso el archivo .dsn reside en una red y puede ser utilizado simultáneamente por varios usuarios en la red, siempre y cuando el usuario tenga instalado el controlador adecuado. Un origen de datos de archivo también puede ser incompartible, en cuyo caso solo se puede utilizar en una sola máquina.  
  
 Para obtener más información sobre los orígenes de datos de archivo, vea Conexión mediante orígenes de [datos](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)de archivo o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Gestión de conductores  
 Si el usuario hace clic en la pestaña **Controladores** del cuadro de diálogo Administrador de orígenes de **datos ODBC,** **SQLManageDataSources** muestra una lista de controladores ODBC instalados en el sistema, así como información sobre los controladores. La fecha mostrada es la fecha de creación del controlador, como se muestra en la siguiente ilustración.  
  
 ![Pestaña Controladores de Administrador de orígenes de datos ODBC](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opciones de traza  
 Si el usuario hace clic en la pestaña **Seguimiento** del cuadro de diálogo Administrador de orígenes de **datos ODBC,** **SQLManageDataSources** muestra las opciones de seguimiento, como se muestra en la siguiente ilustración.  
  
 ![Pestaña Trazas de Administrador de orígenes de datos ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Si el usuario hace clic en **Iniciar seguimiento ahora** y, a continuación, hace clic en **Aceptar**, **SQLManageDataSources** habilita el seguimiento manualmente para todas las aplicaciones que se ejecutan actualmente en el equipo.  
  
 Si el usuario especifica el nombre de un archivo de seguimiento en el cuadro de texto Ruta del **archivo** de registro y, a continuación, hace clic en **Aceptar**, **SQLManageDataSources** establece la palabra clave **TraceFile** en la sección [ODBC] de la información del sistema en el nombre especificado.  
  
> [!IMPORTANT]  
>  La compatibilidad con Visual Studio Analyzer se quitó a partir de Windows 8 (Visual Studio Analyzer solo se incluía en versiones anteriores de Visual Studio.). Para un mecanismo de solución de problemas alternativo, utilice el seguimiento de BID.  
  
 Si el usuario hace clic en **Iniciar Visual Studio Analyzer** y, a continuación, hace clic en **Aceptar**, Visual Studio Analyzer está habilitado. Permanece habilitado hasta que se hace clic en **Detener Visual Studio Analyzer.**  
  
 Para obtener más información sobre el seguimiento, consulte [Seguimiento](../../../odbc/reference/develop-app/tracing.md). Para obtener más información acerca de las palabras clave **Trace** y **TraceFile,** vea [Subclave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Creación de orígenes de datos|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
