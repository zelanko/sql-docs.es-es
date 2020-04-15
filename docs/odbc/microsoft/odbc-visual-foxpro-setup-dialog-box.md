---
title: Cuadro de diálogo Configuración de ODBC Visual FoxPro (ODBC Visual FoxPro Setup) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298085"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Cuadro de diálogo de configuración de Visual FoxPro ODBC
El cuadro de diálogo Configuración de **ODBC Visual FoxPro** permite agregar o cambiar un origen de datos de Visual FoxPro.  
  
 Para descargar el controlador, consulte el sitio de descarga del controlador ODBC de [Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opciones del cuadro de diálogo  
 **Nombre del origen de datos**  
 Escriba el nombre que desea usar para el origen de datos.  
  
 **Descripción**  
 Escriba una descripción para el origen de datos.  
  
 **Tipo de base de datos**  
 Le permite elegir el tipo de base de datos al que desea que se conecte el origen de datos.  
  
 **Base de datos de Visual FoxPro (. DBC)**  
 Especifica que el origen de datos se conecta a una [base](../../odbc/microsoft/visual-foxpro-terminology.md) de datos de Visual FoxPro (archivo .dbc) y a todas las tablas y vistas locales de la base de datos.  
  
 **Directorio de tablas libres**  
 Especifica que el origen de datos se conecta a un directorio de [tablas libres.](../../odbc/microsoft/visual-foxpro-terminology.md) Las funciones de catálogo ODBC, como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables,](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)omiten las tablas de [base](../../odbc/microsoft/visual-foxpro-terminology.md) de datos del mismo directorio. Se puede tener acceso a las tablas de base de datos mediante instrucciones SELECT de SQL enviadas a través de [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) y [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Path**  
 Muestra la ruta de acceso y el nombre de la base de datos o el directorio de tablas libres al que se conecta el origen de datos.  
  
 **Examinar**  
 Permite buscar en el sistema y la red la base de datos o el directorio al que desea conectar el origen de datos.  
  
 **Opciones**  
 Expande el cuadro de diálogo para que pueda establecer las opciones del controlador ODBC de Visual FoxPro.  
  
## <a name="driver"></a>Controlador  
 **Secuencia de intercalación**  
 La secuencia en la que se ordenan los campos. Las secuencias predeterminadas reflejan las secuencias admitidas por la versión de idioma del sistema operativo. Para obtener una lista de las secuencias de intercalación admitidas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusivo**  
 Cuando esta casilla de verificación está activada, el controlador abre la base de datos de Visual FoxPro exclusivamente cuando se accede a los datos mediante el origen de datos. Otros usuarios no pueden tener acceso a la base de datos o a las tablas de la base de datos mientras la base de datos se abre exclusivamente. Las tablas dentro de la base de datos abierta exclusivamente se abren como SHARED. Para abrir una tabla exclusivamente, utilice el comando [SET EXCLUSIVE.](../../odbc/microsoft/set-exclusive-command.md) Esta casilla de verificación está deshabilitada cuando **Tipo de base** de datos se establece en Directorio de tabla **libre**.  
  
 **Null**  
 Determina si las columnas creadas con ALTER TABLE y CREATE TABLE permiten valores nulos. Si establece Null ON, INSERT - SQL inserta un valor nulo en cualquier columna no incluida en un INSERT - SQL... Cláusula VALUE. Se inserta un espacio en blanco si Null está desactivado. También puede controlar esta opción a través de una cadena de conexión pasada como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminado**  
 Determina si se devuelven las filas marcadas como eliminadas. También puede controlar esta opción a través de una cadena de conexión pasada como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Obtener datos en segundo plano**  
 Determina si los registros se recuperarán en segundo plano (recuperación progresiva) o la aplicación esperará hasta que se obtengan todos los registros del conjunto de resultados.
