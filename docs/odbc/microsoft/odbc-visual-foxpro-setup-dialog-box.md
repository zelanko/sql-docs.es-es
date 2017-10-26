---
title: "Cuadro de diálogo de configuración de Visual FoxPro ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 22208bd706e7b8966f54a501e9580b35d99a0555
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Cuadro de diálogo de configuración de Visual FoxPro ODBC
El **programa de instalación de Visual FoxPro ODBC** cuadro de diálogo le permite agregar o cambiar un origen de datos de Visual FoxPro.  
  
 Para descargar el controlador, consulte [el sitio de descarga de Visual FoxPro ODBC Driver](http://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opciones del cuadro de diálogo  
 **Nombre del origen de datos**  
 Escriba el nombre que desea usar para el origen de datos.  
  
 **Description**  
 Escriba una descripción para el origen de datos.  
  
 **Tipo de base de datos**  
 Le permite elegir el tipo de base de datos que desea que el origen de datos al que conectarse.  
  
 **Base de datos Visual FoxPro (. DBC)**  
 Especifica que el origen de datos se conecta a un Visual FoxPro [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) (archivo .dbc) y para todas las tablas y vistas locales en la base de datos.  
  
 **Directorio de tabla libre**  
 Especifica que el origen de datos se conecta a un directorio de [libre tablas](../../odbc/microsoft/visual-foxpro-terminology.md). Cualquier [base de datos](../../odbc/microsoft/visual-foxpro-terminology.md) tablas en el mismo directorio hace caso omiso de las funciones de catálogo ODBC como [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Pueden tener acceso a tablas de base de datos mediante instrucciones SELECT de SQL que se envían a través de [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) y [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Ruta de acceso**  
 Muestra la ruta de acceso y el nombre de la base de datos o el directorio de tablas disponibles al que se conecta el origen de datos.  
  
 **Examinar**  
 Permite buscar el sistema y la red de la base de datos o el directorio al que desea conectarse al origen de datos.  
  
 **Opciones**  
 Expande el cuadro de diálogo para que pueda establecer opciones del controlador ODBC de Visual FoxPro.  
  
## <a name="driver"></a>Controlador  
 **Secuencia de intercalación**  
 La secuencia de ordenación de los campos. Las secuencias de forma predeterminada reflejan las secuencias compatibles con su versión de idioma del sistema operativo. Para obtener una lista de secuencias de intercalación admitidas, consulte [establecer COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusivo**  
 Cuando esta casilla está activada, el controlador abre la base de datos de Visual FoxPro exclusivamente cuando tiene acceso a datos mediante el origen de datos. Otros usuarios no pueden tener acceso a la base de datos o las tablas de la base de datos mientras la base de datos se abre de forma exclusiva. Se abren tablas dentro de la base de datos abierto exclusivamente como compartido. Para abrir una tabla en modo exclusivo, use el [establecer exclusivo](../../odbc/microsoft/set-exclusive-command.md) comando. Esta casilla está deshabilitada cuando **tipo base de datos** está establecido en **directory Free Table**.  
  
 **Es null**  
 Determina si las columnas creadas con ALTER TABLE y CREATE TABLE admiten valores null. Si se establece en Null, INSERT: SQL inserta un valor null en cualquier columna que no se incluye en una instrucción INSERT: SQL... Cláusula de valor. Si Null es OFF, se inserta un espacio en blanco. También puede controlar esta opción a través de una cadena de conexión pasada como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminar**  
 Determina si se devuelven las filas marcadas como eliminadas. También puede controlar esta opción a través de una cadena de conexión pasada como en el código siguiente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Capturar los datos en segundo plano**  
 Determina si los registros se capturarán en segundo plano (capturar progresiva) o la aplicación esperará hasta que se buscan todos los registros del conjunto de resultados.

