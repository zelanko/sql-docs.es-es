---
title: Problemas conocidos de esta versión del controlador de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- known issues
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9cd3bb6f733b9d9cac1dc3973e65199c9357bbbb
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054723"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemas conocidos en esta versión del controlador

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo contiene una lista de problemas conocidos de Microsoft ODBC Driver 13, 13.1 y 17 para SQL Server en Linux y macOS.

Se publicarán más problemas en el [blog del equipo de Microsoft ODBC Driver](http://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux y macOS pueden convertir caracteres del área de uso privado (PUA) o caracteres definidos por el usuario final (EUDC) de forma diferente. Las conversiones que se realizan en el servidor de [!INCLUDE[tsql](../../../includes/tsql_md.md)] usan la biblioteca de conversión de Windows. Las conversiones del controlador usar las bibliotecas de conversión de Windows, Linux o macOS. Cada biblioteca puede generar resultados distintos al realizar estas conversiones. Para obtener más información, consulte [End-User-Defined and Private Use Area Characters](http://msdn.microsoft.com/library/dd317802.aspx)(Caracteres del área de uso privado y definidos por el usuario final).

- Si el cliente de codificación es UTF-8, el Administrador de controladores no siempre convierte correctamente de UTF-8 a UTF-16. Actualmente, daños en los datos se producen cuando uno o más caracteres de la cadena no son caracteres de UTF-8 válidos. Caracteres ASCII se asignan correctamente. El administrador de controladores intenta realizar esta conversión al llamar a las versiones de SQLCHAR de la API de ODBC (por ejemplo, SQLDriverConnectA). El Administrador de controladores no intentará realizar esta conversión al llamar a las versiones de SQLWCHAR de la API de ODBC (por ejemplo, SQLDriverConnectW).  

- El *ColumnSize* parámetro de **SQLBindParameter** hace referencia al número de caracteres en el tipo SQL, mientras que *BufferLength* es el número de bytes en la aplicación búfer. Pero si el tipo de datos de SQL es `varchar(n)` o `char(n)`, la aplicación enlaza el parámetro como SQL_C_CHAR o SQL_C_VARCHAR y la codificación de caracteres del cliente es UTF-8, es posible que obtenga un error "Datos tipo String, se truncarán por la derecha" del controlador, aunque el valor de *ColumnSize* se corresponda con el tamaño del tipo de datos del servidor. Este error se produce porque las conversiones entre las codificaciones de caracteres pueden cambiar la longitud de los datos. Por ejemplo, un apóstrofo derecho de caracteres (2019) está codificado en CP-1252 como el único byte 0 x 92, pero en UTF-8 como secuencia 0xe2 de 3 bytes 0x80 0x99.

Por ejemplo, si la codificación es UTF-8 y especifique 1 para ambos *BufferLength* y *ColumnSize* en **SQLBindParameter** para un parámetro out y, a continuación, intenta recuperar el carácter anterior almacenado en un `char(1)` columna en el servidor (mediante CP-1252), el controlador intenta convertirlo a la codificación de UTF-8 de 3 bytes, pero no puede ajustar el resultado en un búfer de 1 byte. En la otra dirección, lo compara *ColumnSize* con el *BufferLength* en **SQLBindParameter** antes de realizar la conversión entre páginas de códigos diferentes en el cliente y servidor. Dado que un parámetro *ColumnSize* con un valor de 1 es inferior a uno *BufferLength* con, por ejemplo, un valor de 3, el controlador generará un error. Para evitar este error, asegúrese de que la longitud de los datos después de conversión se adapta a la columna o el búfer especificado. Tenga en cuenta que *ColumnSize* no puede ser superior a 8000 la `varchar(n)` tipo.

## <a name="see-also"></a>Ver también  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)  

