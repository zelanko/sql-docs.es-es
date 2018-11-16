---
title: Cuadro de diálogo de instalación de Visual FoxPro ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e2d83f77f8bb9227daab996e425d1880d1bfabd
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674423"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Cuadro de diálogo de configuración de Visual FoxPro ODBC
El **programa de instalación de Visual FoxPro ODBC** cuadro de diálogo permite agregar o cambiar un origen de datos de Visual FoxPro.  
  
 Para descargar el controlador, consulte [el sitio de descarga de Visual FoxPro ODBC Driver](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opciones del cuadro de diálogo  
 **Nombre del origen de datos**  
 Escriba el nombre que desea usar para el origen de datos.  
  
 **Descripción**  
 Escriba una descripción para el origen de datos.  
  
 **Tipo de base de datos**  
 Le permite elegir el tipo de base de datos que desea que el origen de datos al que conectarse.  
  
 **Base de datos Visual FoxPro (. DBC)**  
 Especifica que el origen de datos se conecta a un Visual FoxPro [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) (archivo .dbc) y a todas las tablas y vistas locales en la base de datos.  
  
 **Directorio libre de tabla**  
 Especifica que el origen de datos se conecta a un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md). Cualquier [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) tablas en el mismo directorio se omiten las funciones de catálogo ODBC como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Pueden tener acceso a las tablas de base de datos mediante el uso de instrucciones SELECT de SQL que se envían a través de [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) y [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Ruta de acceso**  
 Muestra la ruta de acceso y nombre de la base de datos o el directorio de tablas libres al que se conecta el origen de datos.  
  
 **Examinar**  
 Permite buscar en el sistema y la red para la base de datos o el directorio al que desea conectarse al origen de datos.  
  
 **Opciones**  
 Expande el cuadro de diálogo para que pueda establecer las opciones del controlador ODBC de Visual FoxPro.  
  
## <a name="driver"></a>Controlador  
 **Secuencia de intercalación**  
 La secuencia en la que se ordenan los campos. Las secuencias de forma predeterminada reflejan las secuencias admitidas por la versión de idioma del sistema operativo. Para obtener una lista de secuencias de intercalación admitidas, consulte [establecer intercalar](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusivo**  
 Cuando se selecciona esta casilla, el controlador abre la base de datos de Visual FoxPro exclusivamente cuando tiene acceso a datos mediante el origen de datos. Otros usuarios no pueden acceder a la base de datos o las tablas de la base de datos mientras se abre de forma exclusiva la base de datos. Se abren tablas dentro de la base de datos abierta exclusivamente como compartido. Para abrir una tabla exclusivamente, utilice el [establecer exclusivo](../../odbc/microsoft/set-exclusive-command.md) comando. Esta casilla está deshabilitada cuando **tipo base de datos** está establecido en **directory tabla libre**.  
  
 **Null**  
 Determina si las columnas creadas con ALTER TABLE y CREATE TABLE admiten valores null. Si se establece en Null, Insertar – SQL inserta un valor null en cualquier columna que no se incluye en una instrucción INSERT: SQL... Cláusula VALUE. Si Null es OFF, se inserta un espacio en blanco. También puede controlar esta opción a través de una cadena de conexión pasada como se muestra en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminado**  
 Determina si se devuelven las filas marcadas como eliminadas. También puede controlar esta opción a través de una cadena de conexión pasada como se muestra en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Capturar los datos en segundo plano**  
 Determina si se recuperarán los registros en segundo plano (capturando progresiva) o la aplicación esperará hasta que se capturan todos los registros del conjunto de resultados.
