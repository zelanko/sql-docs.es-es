---
title: Configuración de opciones mediante programación para el controlador de archivo de texto ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e19c3b49479047bc92a7b6f72359d4951d8df16e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300755"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Establecer opciones mediante programación para el controlador de archivo de texto

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Nombre que identifica el origen de datos, como Cálculo de nómina o Personal.|Para establecer esta opción dinámicamente, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir formato|Muestra el cuadro de diálogo **Definir formato** de texto y permite especificar el esquema para tablas individuales en el directorio del origen de datos.|Esta opción no se puede establecer dinámicamente mediante una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos; por ejemplo, "Fecha de contratación, historial salarial y revisión actual de todos los empleados".|Para establecer esta opción dinámicamente, utilice la palabra clave **DESCRIPTION** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directorio|Selecciona el directorio de destino.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensiones|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos. Cuando se utiliza el controlador de texto, se crea un archivo sin extensión cuando se ejecuta la instrucción CREATE TABLE con un nombre que no tiene extensión. Otros controladores crean un archivo con una extensión predeterminada cuando no se proporciona ninguna extensión. Para crear un archivo con una extensión .txt, la extensión debe incluirse en el nombre. Para mostrar archivos sin extensiones en el cuadro de diálogo Definir formato de **texto,** "*." debe agregarse a la lista de extensiones.|Para establecer esta opción dinámicamente, utilice la palabra clave **EXTENSIONS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción dinámicamente, utilice la palabra clave **READONLY** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Filas para escanear|El número de filas que se van a examinar para determinar el tipo de datos de cada columna. El tipo de datos se determina dado el número máximo de tipos de datos encontrados. Si se encuentran datos que no coinciden con el tipo de datos adivinado para la columna, el tipo de datos se devolverá como un valor NULL.<br /><br /> Para el controlador de texto, puede introducir un número del 1 al 32767 para el número de filas que se van a escanear; sin embargo, el valor siempre se establecerá de forma predeterminada en 25. (Un número fuera del límite devolverá un error.)|Para establecer esta opción dinámicamente, utilice la palabra clave **MAXSCANROWS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Seleccione Directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea acceder.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos más utilizados. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se utilizan con frecuencia. Como alternativa, puede calificar los nombres de archivo en una instrucción SELECT con el nombre del directorio:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
