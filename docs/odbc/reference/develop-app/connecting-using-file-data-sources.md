---
title: Conectar con orígenes de datos de archivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6fec2cea71ba818e955e0b6c2ce31c58f2c07357
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677324"
---
# <a name="connecting-using-file-data-sources"></a>Conectar con orígenes de datos de archivo
La información de conexión para un origen de datos de archivo se almacena en un archivo DSN. Como resultado, la cadena de conexión se puede utilizar varias veces un único usuario o compartida entre varios usuarios si tienen instalado el controlador apropiado. El archivo contiene un nombre de controlador (u otro nombre de origen de datos en el caso de un origen de datos de archivo no se puede compartir) y si lo desea, una cadena de conexión que puede usarse por **SQLDriverConnect**. El Administrador de controladores se basa la cadena de conexión para la llamada a **SQLDriverConnect** en las palabras clave en el archivo DSN.  
  
 Un origen de datos de archivo permite que una aplicación especificar las opciones de conexión sin tener que crear una cadena de conexión para su uso con **SQLDriverConnect**. Normalmente, se crea el origen de datos de archivos especificando la **SAVEFILE** palabra clave, lo que hace que el Administrador de controladores para guardar la cadena de conexión de salida creada por una llamada a **SQLDriverConnect** al archivo DSN. Que la cadena de conexión se puede usar repetidamente mediante una llamada a **SQLDriverConnect** con el **FILEDSN** palabra clave. Esto simplifica el proceso de conexión y proporciona un origen de la cadena de conexión persistente.  
  
 Orígenes de datos de archivo también se pueden crear mediante una llamada a **SQLCreateDataSource** en el archivo DLL de instalador. Se puede escribir información en el archivo DSN mediante una llamada a **SQLWriteFileDSN**y leer el archivo DSN mediante una llamada a **SQLReadFileDSN**; ambas de estas funciones también están en el archivo DLL de instalador. Para obtener información acerca del archivo DLL de instalador, vea [configurar orígenes de datos](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Las palabras clave utilizadas para obtener información de conexión están en la sección [ODBC] de un archivo DSN. La información mínima que tendría un archivo DSN que se pueda compartir en la sección [ODBC] es la palabra clave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 El archivo que se pueda compartir .dsn normalmente contiene una cadena de conexión, como se indica a continuación:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Cuando el origen de datos de archivo es no se puede compartir, el archivo .dsn contiene sólo un **DSN** palabra clave. Cuando el Administrador de controladores se envía la información en un origen de datos no se puede compartir archivos, se conecta según sea necesario para el origen de datos indicado por el **DSN** palabra clave. Un archivo no se puede compartir .dsn contendría la siguiente palabra clave:  
  
```  
DSN = MyDataSource  
```  
  
 La cadena de conexión utilizada para un origen de datos de archivo es la unión de las palabras clave especificadas en el archivo DSN y las palabras clave especificadas en la cadena de conexión en la llamada a **SQLDriverConnect**. Si cualquiera de las palabras clave en el archivo .dsn entran en conflicto con las palabras clave en la cadena de conexión, el Administrador de controladores decide qué valor de palabra clave debe usarse. Para obtener más información, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vea también  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
