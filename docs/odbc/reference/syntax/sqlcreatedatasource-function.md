---
title: Función SQLCreateDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b432e8d40952574f1264e07a0b09e91a1e334b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537611"
---
# <a name="sqlcreatedatasource-function"></a>Función SQLCreateDataSource
**Conformidad**  
 Versión de introducción: ODBC 2.0  
  
 **Resumen**  
 **SQLCreateDataSource** muestra un cuadro de diálogo con el que el usuario puede agregar un origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwnd*  
 [Entrada] Identificador de la ventana primaria.  
  
 *lpszDS*  
 [Entrada] Nombre del origen de datos. *lpszDS* puede ser un puntero nulo o una cadena vacía.  
  
## <a name="returns"></a>Devuelve  
 **SQLCreateDataSource** devuelve TRUE si se crea el origen de datos. En caso contrario, devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLCreateDataSource** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válida|El *hwnd* argumento era NULL o no válido.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El *lpszDS* argumento contiene una cadena que no era válida para un DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|La llamada a **ConfigDSN** con la opción ODBC_ADD_DSN generado un error.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de traductor o controlador|No se pudo cargar la biblioteca del programa de instalación de controladores.|  
|ODBC_ERROR_USER_CANCELED|Operación cancelado por el usuario|El usuario canceló la creación de un nuevo origen de datos.|  
|ODBC_ERROR_CREATE_DSN_FAILED|No se pudo crear el DSN solicitado|No se pudo conectar a la base de datos; la llamada a **SQLDriverConnect** para un DSN de archivo no ha devuelto una conexión correcta.<br /><br /> No se pudo escribir en el archivo.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Si *hwnd* es null, **SQLCreateDataSource** devuelve FALSE. De lo contrario, muestra el **crear nuevo origen de datos** cuadro de diálogo con una página del Asistente para elegir el tipo de origen de datos para configurar, como se muestra en la siguiente ilustración.  
  
 ![Crear el cuadro de diálogo nuevo origen de datos: Seleccionar tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 La opción predeterminada es **origen de datos de archivo**. Cuando se ha elegido un origen de datos y **siguiente** hace clic en, se muestra la siguiente página del asistente que contiene una lista de controladores instalados.  
  
 ![Crear el cuadro de diálogo nuevo origen de datos: seleccionar controlador](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Si **cancelar** se hace clic en, el cuadro de diálogo cuadro desaparece y **SQLCreateDataSource** devuelve FALSE con el código de error de ODBC_ERROR_USER_CANCELED. Si el **origen de datos de usuario** o **origen de datos del sistema** se ha seleccionado la opción, el **avanzadas** botón no está disponible.  
  
 Cuando el **siguiente** se hace clic en botón, se producirá uno de los siguientes, dependiendo del tipo de datos de origen se ha seleccionado:  
  
-   Si **File Data Source** estaba seleccionado, se muestra una página del Asistente para que el usuario que escriba un nombre de archivo.  
  
-   Si **origen de datos de usuario** o **origen de datos del sistema** estaba seleccionado, se muestra una página del asistente muestra el tipo de origen de datos y el controlador para su revisión y cuándo **finalizar** es Haga clic en, el origen de datos está configurado.  
  
 Si **avanzadas** se hace clic en la página del Asistente Crear nuevo origen de datos, se muestra una página del Asistente para que el usuario escriba información específica del controlador. En el cuadro de texto de este cuadro de diálogo, escriba el controlador y palabras clave separadas por devoluciones, tal como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo de configuración de creación del DSN de archivo por adelantado](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Palabras clave adicionales específicas del controlador pueden encontrarse en la descripción de **SQLDriverConnect**. Todos excepto **DSN** se permiten.  
  
 El valor predeterminado para el **comprobar esta conexión** opción es TRUE. Este valor predeterminado se aplica si se activa esta página del asistente. Si **Aceptar** se hace clic en, la cadena especificada en el cuadro de texto y el **comprobar esta conexión** se almacenan en caché el valor de opción. (Si la **cerrar** botón o **cancelar** se hace clic en, cualquiera recién introducido información específica del controlador se pierde porque la cadena especificada en el cuadro de texto y el **comprobar esta conexión** no se almacenan en caché del valor de opción.)  
  
 Si **File Data Source** se seleccionó en la primera página del asistente, a continuación, una vez se ha seleccionado un controlador y los valores de palabra clave se ha escrito en la página del Asistente para configuración avanzada, el usuario pide que escriba un nombre de archivo. Haga clic en **examinar** para buscar un nombre de archivo, en cuyo caso el directorio predeterminado en el **examinar** cuadro se especifica mediante una combinación de la ruta de acceso especificada por CommonFileDir en HKEY_LOCAL_MACHINE\SOFTWARE\ Microsoft\Windows\CurrentVersion y "ODBC\DataSources". (Si CommonFileDir era "C:\Program Files\Common archivos", el directorio predeterminado sería "C:\Program programa\Common Files\ODBC\Data Sources").  
  
 Cuando se ha introducido un nombre de archivo y **siguiente** se hace clic en, el archivo de nombre especificado se comprueba la validez con las reglas de nomenclatura de archivos estándares del sistema operativo. Si el nombre de archivo no es válido, un cuadro de mensaje de error notifica al usuario que ha escrito un nombre de archivo no válido. Después de que el usuario confirma el cuadro de mensaje, se devuelve el foco a la página del asistente en el que se escribe el nombre de archivo. Si el nombre de archivo es válido, se muestra una página del asistente que muestra los pares de palabra clave y valor seleccionado para su revisión, tal como se muestra en la siguiente ilustración.  
  
 ![Crear el cuadro de diálogo nuevo origen de datos: revisar](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Si **finalizar** se hace clic en y **File Data Source** se ha seleccionado como el tipo de origen de datos y si el **comprobar esta conexión** opción es TRUE,  **SQLDriverConnect** se denomina con el **SAVEFILE** y **controlador** palabras clave. El *DriverCompletion* argumento está establecido en SQL_DRIVER_COMPLETE. El nombre de archivo para el **SAVEFILE** palabra clave es el nombre que se ha especificado o elegido y el nombre del controlador para el **controlador** palabra clave es el nombre que se ha elegido. Si se especificó una cadena de conexión específicos del controlador en la página del Asistente para configuración avanzada, esa cadena se anexa después la **controlador** palabra clave.  
  
 Si **SQLDriverConnect** devuelve SQL_SUCCESS, el Administrador de controladores ha creado el DSN de archivo. **SQLCreateDataSource** devuelve TRUE. Si **SQLDriverConnect** no devuelve SQL_SUCCESS, un mensaje de advertencia cuadro indica que no se pudo establecer una conexión al origen de datos. Todavía se puede crear un DSN con información de conexión mínima. Este cuadro de mensaje permite al usuario cancelar o continuar con la creación del DSN de archivo.  
  
 Si el usuario decide continuar creando el DSN, este proceso continúa como si el **comprobar esta conexión** opción se establece en FALSE. Si el usuario decide cancelar, se devuelve FALSE para **SQLCreateDataSource** con un código de error de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Si **File Data Source** se ha seleccionado como el tipo de origen de datos y el **comprobar esta conexión** opción es FALSE, se crea un DSN de archivo con el **controlador** palabra clave y especificado por el usuario cadena de conexión (si existe) desde la página del Asistente para configuración avanzada. Si la creación del archivo se realizó correctamente, se devuelve TRUE para **SQLCreateDataSource**. Si no se realizó correctamente la creación del archivo, un cuadro de mensaje de error notifica al usuario con error que se devolvió desde el sistema operativo. Se devuelve FALSE para **SQLCreateDataSource** con un código de error de ODBC_ERROR_CREATE_DSN_FAILED. Para obtener más información acerca de los orígenes de datos de archivo, consulte [conecta orígenes de datos de archivo utilizando](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), o vea [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Si **usuario** o **origen de datos del sistema** se ha seleccionado como el tipo de origen de datos, **ConfigDSN** en la configuración del controlador de biblioteca se denomina con el ODBC_ADD_DSN  *fRequest*. Para obtener más información, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Administrar orígenes de datos|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
