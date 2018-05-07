---
title: Conectar con orígenes de datos de archivo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], file data sources
- SQLDriverConnect function [ODBC], connecting using file data sources
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], file data sources
- file data sources [ODBC]
ms.assetid: 3003f8c2-8be6-41cc-8d9c-612e9bd0f3ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9e8fa3bbc90af4dc17d1dfc7e161fcab0177db7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-using-file-data-sources"></a>Conectar con orígenes de datos de archivo
La información de conexión para un origen de datos de archivo se almacena en un archivo de DSN. Como resultado, la cadena de conexión se puede utilizar repetidamente a un solo usuario o compartir entre varios usuarios si tienen instalado el controlador apropiado. El archivo contiene un nombre de controlador (u otro nombre de origen de datos en el caso de un origen de datos de archivo no se puede compartir) y si lo desea, una cadena de conexión que se puede usar por **SQLDriverConnect**. El Administrador de controladores genera la cadena de conexión de la llamada a **SQLDriverConnect** de las palabras clave en el archivo de DSN.  
  
 Un origen de datos de archivos permite que una aplicación especificar las opciones de conexión sin tener que crear una cadena de conexión para su uso con **SQLDriverConnect**. El origen de datos de archivo normalmente se crea especificando el **SAVEFILE** palabra clave, que hace que el Administrador de controladores para guardar la cadena de conexión de salida creada por una llamada a **SQLDriverConnect** al archivo DSN. Que la cadena de conexión se puede usar varias veces mediante una llamada a **SQLDriverConnect** con el **FILEDSN** palabra clave. Esto simplifica el proceso de conexión y proporciona una fuente persistente de la cadena de conexión.  
  
 Orígenes de datos de archivo también se pueden crear mediante una llamada a **SQLCreateDataSource** en el archivo DLL del instalador. Se puede escribir información en el archivo .dsn mediante una llamada a **SQLWriteFileDSN**y leer el archivo .dsn mediante una llamada a **SQLReadFileDSN**; ambas de estas funciones también están en el archivo DLL del instalador. Para obtener información acerca del instalador de DLL, consulte [configurar orígenes de datos](../../../odbc/reference/install/configuring-data-sources.md).  
  
 Las palabras clave utilizadas para obtener información de conexión se encuentran en la sección [ODBC] de un archivo de DSN. La información mínima que tendría un archivo .dsn pueden compartirse en la sección [ODBC] es la palabra clave DRIVER:  
  
```  
DRIVER = SQL Server  
```  
  
 El archivo .dsn compartible normalmente contiene una cadena de conexión, como se indica a continuación:  
  
```  
DRIVER = SQL Server  
UID = Larry  
DATABASE = MyDB  
```  
  
 Una vez no se puede compartir el origen de datos de archivo, el archivo .dsn contiene sólo un **DSN** palabra clave. Cuando el Administrador de controladores se envía la información en un origen de datos de archivo no se puede compartir, se conecta según sea necesario para el origen de datos indicado por la **DSN** palabra clave. Un archivo no se puede compartir .dsn contendría la siguiente palabra clave:  
  
```  
DSN = MyDataSource  
```  
  
 La cadena de conexión que se utiliza para un origen de datos de archivo es la unión de las palabras clave especificadas en el archivo .dsn y las palabras clave especificadas en la cadena de conexión en la llamada a **SQLDriverConnect**. Si cualquiera de las palabras clave en el archivo .dsn entra en conflicto con las palabras clave en la cadena de conexión, el Administrador de controladores decide qué valor de palabra clave se debe usar. Para obtener más información, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Vea también  
 [http://support.microsoft.com/kb/165866](http://support.microsoft.com/kb/165866)
