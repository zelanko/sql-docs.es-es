---
title: Conexión mediante orígenes de datos de archivos ( File Data Sources) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c752fc3b09c06c68dcc216cacac63744dc3101b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287415"
---
# <a name="connecting-using-file-data-sources"></a>Conectar con orígenes de datos de archivo
La información de conexión de un origen de datos de archivo se almacena en un archivo .dsn. Como resultado, la cadena de conexión puede ser utilizada repetidamente por un solo usuario o compartida entre varios usuarios si tienen instalado el controlador adecuado. El archivo contiene un nombre de controlador (u otro nombre de origen de datos en el caso de un origen de datos de archivo no compartible) y, opcionalmente, una cadena de conexión que **SQLDriverConnect**puede utilizar. El Administrador de controladores compila la cadena de conexión para la llamada a **SQLDriverConnect** desde las palabras clave del archivo .dsn.  
  
 Un origen de datos de archivo permite a una aplicación especificar opciones de conexión sin tener que crear una cadena de conexión para su uso con **SQLDriverConnect**. El origen de datos de archivo normalmente se crea especificando la palabra clave **SAVEFILE,** lo que hace que el Administrador de controladores guarde la cadena de conexión de salida creada por una llamada a **SQLDriverConnect** en el archivo .dsn. Esa cadena de conexión se puede usar repetidamente llamando a **SQLDriverConnect** con la palabra clave **FILEDSN.** Esto optimiza el proceso de conexión y proporciona un origen persistente de la cadena de conexión.  
  
 Los orígenes de datos de archivo también se pueden crear llamando a **SQLCreateDataSource** en el archivo DLL del instalador. La información se puede escribir en el archivo .dsn llamando a **SQLWriteFileDSN**y leerse desde el archivo .dsn llamando a **SQLReadFileDSN**; ambas funciones también están en el archivo DLL del instalador. Para obtener información sobre el archivo DLL del instalador, consulte [Configuración de orígenes](../../../odbc/reference/install/configuring-data-sources.md)de datos .  
  
 Las palabras clave utilizadas para la información de conexión se encuentran en la sección [ODBC] de un archivo .dsn. La información mínima que tendría un archivo .dsn compartible en la sección [ODBC] es la palabra clave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 El archivo .dsn compartible normalmente contiene una cadena de conexión, como se indica a continuación:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Cuando el origen de datos del archivo no se puede compartir, el archivo .dsn solo contiene una palabra clave **DSN.** Cuando se envía la información en un origen de datos de archivo no compartible, se conecta según sea necesario al origen de datos indicado por la palabra clave **DSN.** Un archivo .dsn no compartible contendría la siguiente palabra clave:  
  
```  
DSN = MyDataSource  
```  
  
 La cadena de conexión utilizada para un origen de datos de archivo es la unión de las palabras clave especificadas en el archivo .dsn y las palabras clave especificadas en la cadena de conexión en la llamada a **SQLDriverConnect**. Si alguna de las palabras clave del archivo .dsn entra en conflicto con las palabras clave de la cadena de conexión, el Administrador de controladores decide qué valor de palabra clave se debe usar. Para obtener más información, vea [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte también  
 [https://support.microsoft.com/kb/165866](https://support.microsoft.com/kb/165866)
