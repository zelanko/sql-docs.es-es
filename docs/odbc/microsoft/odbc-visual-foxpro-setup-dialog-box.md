---
title: Cuadro de diálogo Configuración de ODBC Visual FoxPro | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298085"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Cuadro de diálogo de configuración de Visual FoxPro ODBC
El cuadro de diálogo **configuración de ODBC para Visual FoxPro** le permite agregar o cambiar un origen de datos de Visual FoxPro.  
  
 Para descargar el controlador, consulte [el sitio de descarga del controlador ODBC de Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opciones del cuadro de diálogo  
 **Nombre del origen de datos**  
 Escriba el nombre que desea usar para el origen de datos.  
  
 **Descripción**  
 Escriba una descripción para el origen de datos.  
  
 **Tipo de base de datos**  
 Permite elegir el tipo de base de datos al que se desea conectar el origen de datos.  
  
 **Base de datos de Visual FoxPro (. DBC**  
 Especifica que el origen de datos se conecta a una [base](../../odbc/microsoft/visual-foxpro-terminology.md) de datos de Visual FoxPro (archivo. DBC) y a todas las tablas y vistas locales de la base de datos.  
  
 **Directorio de tabla libre**  
 Especifica que el origen de datos se conecta a un directorio de [tablas libres](../../odbc/microsoft/visual-foxpro-terminology.md). Las funciones de catálogo de ODBC, como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md), omiten todas las tablas de [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) del mismo directorio. Se puede tener acceso a las tablas de base de datos mediante instrucciones SELECT de SQL enviadas a través de [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) y [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Path**  
 Muestra la ruta de acceso y el nombre de la base de datos o el directorio de las tablas disponibles a las que se conecta el origen de datos.  
  
 **Examinar**  
 Permite buscar en el sistema y la red la base de datos o el directorio al que desea conectar el origen de datos.  
  
 **Opciones**  
 Expande el cuadro de diálogo para que pueda establecer las opciones del controlador ODBC de Visual FoxPro.  
  
## <a name="driver"></a>Controlador  
 **Secuencia de intercalación**  
 Secuencia en la que se ordenan los campos. Las secuencias predeterminadas reflejan las secuencias admitidas por la versión de idioma del sistema operativo. Para obtener una lista de las secuencias de intercalación admitidas, vea [set COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusivo**  
 Cuando se activa esta casilla, el controlador abre la base de datos de Visual FoxPro exclusivamente cuando se obtiene acceso a los datos mediante el origen de datos. Otros usuarios no pueden tener acceso a la base de datos ni a las tablas de la base de datos mientras la base de datos se abre exclusivamente. Las tablas de la base de datos abierta exclusivamente se abren como compartidas. Para abrir exclusivamente una tabla, use el comando [set Exclusive](../../odbc/microsoft/set-exclusive-command.md) . Esta casilla está deshabilitada cuando el **tipo de base de datos** está establecido en directorio de **tabla libre**.  
  
 **Null**  
 Determina si las columnas creadas con ALTER TABLE y CREATE TABLE permiten valores NULL. Si establece null en, INSERT-SQL inserta un valor null en una columna no incluida en una instrucción INSERT-SQL... Cláusula VALUE. Si null está desactivado, se inserta un espacio en blanco. También puede controlar esta opción a través de una cadena de conexión que se pasa como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminado**  
 Determina si se devuelven las filas marcadas como eliminadas. También puede controlar esta opción a través de una cadena de conexión que se pasa como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Obtención de datos en segundo plano**  
 Determina si los registros se capturarán en segundo plano (captura progresiva) o si la aplicación esperará hasta que se capturen todos los registros del conjunto de resultados.
