---
title: Configuración de opciones mediante programación para el controlador de Excel ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1fcd5542e4beee1f7c7a30d5e0ee9f2815a3f0b6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300775"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Opciones de configuración mediante programación para el controlador de Excel

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Nombre que identifica el origen de datos, como Cálculo de nómina o Personal.|Para establecer esta opción dinámicamente, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar ni crear una base de datos. Si no se proporciona ninguna base de datos al configurarla, se pedirá al usuario que elija un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción dinámicamente, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos; por ejemplo, "Fecha de contratación, historial salarial y revisión actual de todos los empleados".|Para establecer esta opción dinámicamente, utilice la palabra clave **DESCRIPTION** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directorio|Muestra el directorio seleccionado actualmente.<br /><br /> Para los archivos de Microsoft Excel 3.0/4.0, la visualización de la ruta de acceso se etiqueta como "Directorio", mientras que para los archivos de Microsoft Excel 5.0, 7.0 o 97, la visualización de la ruta de acceso se etiqueta como "Libro de trabajo".|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción dinámicamente, utilice la palabra clave **READONLY** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Filas para escanear|El número de filas que se van a examinar para determinar el tipo de datos de cada columna. El tipo de datos se determina dado el número máximo de tipos de datos encontrados. Si se encuentran datos que no coinciden con el tipo de datos adivinado para la columna, el tipo de datos se devolverá como un valor NULL.<br /><br /> Para el controlador de Microsoft Excel, puede escribir un número del 1 al 16 para que las filas se van a examinar. El valor predeterminado es 8; si se establece en 0, se analizan todas las filas. (Un número fuera del límite devolverá un error.)|Para establecer esta opción dinámicamente, utilice la palabra clave **MAXSCANROWS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Seleccione Directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea acceder.<br /><br /> Al definir un directorio de origen de datos (para todos los controladores excepto Microsoft Access), especifique el directorio donde se encuentran los archivos más utilizados. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se utilizan con frecuencia. Como alternativa, puede calificar los nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:-MYDIR-EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.<br /><br /> Para los archivos de Microsoft Excel 3.0 o 4.0, la visualización de la ruta de acceso se etiqueta como "Directorio" y el botón de selección de ruta de acceso se etiqueta como "Seleccionar directorio". Para los archivos de Microsoft Excel 5.0, 7.0 o 97, la visualización de la ruta de acceso se etiqueta como "Libro de trabajo" y el botón de selección de ruta se etiqueta como "Seleccionar libro de trabajo". Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos de Microsoft Excel más utilizados para Microsoft Excel 3.0/4.0, o el directorio donde se encuentra el archivo de libro para Microsoft Excel 5.0, 7.0 o 97. **Usar directorio actual** está deshabilitado para Microsoft Excel 5.0, 7.0 y 97.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
