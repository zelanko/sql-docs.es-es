---
title: Función SQLCreateDataSource ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94dc0d6d6f3b5bc96ae41aecda5b46f119cff85c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301205"
---
# <a name="sqlcreatedatasource-function"></a>Función SQLCreateDataSource
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **SQLCreateDataSource** muestra un cuadro de diálogo con el que el usuario puede agregar un origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hwnd*  
 [Entrada] Identificador de ventana principal.  
  
 *lpszDS*  
 [Entrada] Nombre del origen de datos. *lpszDS* puede ser un puntero nulo o una cadena vacía.  
  
## <a name="returns"></a>Devuelve  
 **SQLCreateDataSource** devuelve TRUE si se crea el origen de datos. De lo contrario, devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLCreateDataSource** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_HWND|Mango de ventana no válido|El *hwnd* argumento no era válido o NULL.|  
|ODBC_ERROR_INVALID_DSN|DSN no válido|El argumento *lpszDS* contenía una cadena que no era válida para un DSN.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitud* fallida|Error en la llamada a **ConfigDSN** con la opción ODBC_ADD_DSN.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de configuración del controlador o traductor|No se ha podido cargar la biblioteca de configuración del controlador.|  
|ODBC_ERROR_USER_CANCELED|Operación cancelada por el usuario|El usuario canceló la creación de un nuevo origen de datos.|  
|ODBC_ERROR_CREATE_DSN_FAILED|No se pudo crear el DSN solicitado|No se pudo conectar a la base de datos; la llamada a **SQLDriverConnect** para un DSN de archivo no devolvió una conexión correcta.<br /><br /> No se pudo escribir en el archivo.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 Si *hwnd* es null, **SQLCreateDataSource** devuelve FALSE. De lo contrario, muestra el cuadro de diálogo **Crear nuevo origen** de datos con una página del asistente para elegir el tipo de origen de datos que se va a configurar, como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Crear un nuevo origen de datos: seleccionar tipo](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 La opción predeterminada es Origen de **datos**de archivo . Cuando se ha elegido un origen de datos y se ha hecho clic en **Siguiente,** se muestra la siguiente página del asistente que contiene una lista de controladores instalados.  
  
 ![Cuadro de diálogo Crear un nuevo origen de datos: seleccionar controlador](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 Si se hace clic en **Cancelar,** el cuadro de diálogo desaparece y **SQLCreateDataSource** devuelve FALSE con el código de error de ODBC_ERROR_USER_CANCELED. Si se ha seleccionado la opción Origen de **datos** de usuario o Origen de datos del **sistema,** el botón **Avanzado** no está disponible.  
  
 Cuando se hace clic en el botón **Siguiente,** se producirá una de las siguientes situaciones, dependiendo del tipo de origen de datos seleccionado:  
  
-   Si se ha seleccionado Origen de **datos** de archivo, se muestra una página del asistente para que el usuario escriba un nombre de archivo.  
  
-   Si se ha seleccionado Origen de **datos** de usuario o **Origen** de datos del sistema, se muestra para su revisión una página del asistente que muestra el tipo de origen de datos y el controlador y, cuando se hace clic en **Finalizar,** se configura el origen de datos.  
  
 Si se hace clic en **Avanzadas** desde la página del asistente Crear nuevo origen de datos, se muestra una página del asistente para que el usuario escriba información específica del controlador. En el cuadro de texto de este cuadro de diálogo, escriba el controlador y las palabras clave separadas por retornos, como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Configuración de creación avanzada de DSN de archivo](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 Puede encontrar palabras clave adicionales específicas del controlador en la descripción de **SQLDriverConnect**. Todos excepto **DSN** están permitidos.  
  
 El valor predeterminado para la opción **Comprobar esta conexión** es TRUE. Este valor predeterminado se aplica independientemente de si esta página del asistente está activada o no. Si se hace clic en **Aceptar,** se almacenan en caché la cadena especificada en el cuadro de texto y el valor de la opción **Comprobar esta conexión.** (Si se hace clic en el botón **Cerrar** o **Cancelar,** se pierde cualquier información específica del controlador recién introducida porque la cadena especificada en el cuadro de texto y el valor de la opción **Verificar esta conexión** no se almacenan en caché.)  
  
 Si se ha seleccionado Origen de **datos** de archivo en la primera página del asistente, después de seleccionar un controlador y especificar los valores de palabra clave en la página Asistente avanzado, se solicita al usuario que escriba un nombre de archivo. Haga clic en **Examinar** para buscar un nombre de archivo, en cuyo caso el directorio predeterminado en el cuadro **Examinar** se especifica mediante una combinación de la ruta de acceso especificada por CommonFileDir en HKEY_LOCAL_MACHINE. (Si CommonFileDir era "C:-Archivos de programa-Archivos comunes", el directorio predeterminado sería "C:-Archivos de programa-Archivos comunes-ODBC-Orígenes de datos".)  
  
 Cuando se ha introducido un nombre de archivo y se hace clic en **Siguiente,** se comprueba la validez del nombre de archivo con respecto a las reglas de nomenclatura de archivos estándar del sistema operativo. Si el nombre de archivo no es válido, un cuadro de mensaje de error notifica al usuario que se ha introducido un nombre de archivo no válido. Después de que el usuario reconoce el cuadro de mensaje, el foco se devuelve a la página del asistente en la que se especifica el nombre de archivo. Si el nombre de archivo es válido, se muestra una página del asistente que muestra los pares palabra clave-valor seleccionados para su revisión, como se muestra en la siguiente ilustración.  
  
 ![Cuadro de diálogo Crear un nuevo origen de datos: revisar](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 Si se hace clic en **Finalizar** y se ha seleccionado Origen de **datos** de archivo como tipo de origen de datos y si la opción Comprobar **esta conexión** es TRUE, **SQLDriverConnect** se llama con las palabras clave **SAVEFILE** y **DRIVER.** El *DriverCompletion* argumento se establece en SQL_DRIVER_COMPLETE. El nombre de archivo de la palabra clave **SAVEFILE** es el nombre que se ha introducido o elegido, y el nombre del controlador de la palabra clave **DRIVER** es el nombre que se eligió. Si se especificó una cadena de conexión específica del controlador en la página del asistente Avanzado, esa cadena se anexa después de la palabra clave **DRIVER.**  
  
 Si **SQLDriverConnect** devuelve SQL_SUCCESS, el Administrador de controladores ha creado el DSN de archivo. **SQLCreateDataSource** devuelve TRUE. Si **SQLDriverConnect** no devuelve SQL_SUCCESS, un cuadro de mensaje de advertencia indica que no se pudo realizar una conexión al origen de datos. Todavía se puede crear un DSN con una información de conexión mínima. Este cuadro de mensaje permite al usuario cancelar o continuar con la creación de DSN de archivo.  
  
 Si el usuario decide continuar creando el DSN, este proceso continúa como si la opción **Verificar esta conexión** estuviera establecida en FALSE. Si el usuario decide cancelar, FALSE se devuelve para **SQLCreateDataSource** con un código de error de ODBC_ERROR_CREATE_DSN_FAILED.  
  
 Si se ha seleccionado Origen de **datos** de archivo como tipo de origen de datos y la opción Comprobar **esta conexión** es FALSE, se crea un DSN de archivo con la palabra clave **DRIVER** y la cadena de conexión especificada por el usuario (si existe) de la página Asistente avanzado. Si la creación del archivo se realizó correctamente, se devuelve TRUE para **SQLCreateDataSource**. Si la creación del archivo no se realizó correctamente, un cuadro de mensaje de error notifica al usuario con cualquier error devuelto desde el sistema operativo. FALSE se devuelve para **SQLCreateDataSource** con un código de error de ODBC_ERROR_CREATE_DSN_FAILED. Para obtener más información acerca de los orígenes de datos de archivo, vea Conexión mediante orígenes de [datos](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)de archivo o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
 Si se ha seleccionado **Usuario** o **Origen** de datos del sistema como tipo de origen de datos, se llama a **ConfigDSN** en la biblioteca de configuración del controlador con la ODBC_ADD_DSN *fRequest*. Para obtener más información, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Administración de orígenes de datos|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
