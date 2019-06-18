---
title: Problemas conocidos en esta versión del controlador para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 86b87d03a5b0a66ba1e77260a0ec0b43125fa98b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798755"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemas conocidos en esta versión del controlador

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artículo contiene una lista de problemas conocidos de Microsoft ODBC Driver 13, 13.1 y 17 para SQL Server en Linux y macOS.

Se publicarán más problemas en el [blog del equipo de Microsoft ODBC Driver](https://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux y macOS pueden convertir caracteres del área de uso privado (PUA) o caracteres definidos por el usuario final (EUDC) de forma diferente. Las conversiones que se realizan en el servidor de [!INCLUDE[tsql](../../../includes/tsql-md.md)] usan la biblioteca de conversión de Windows. Las conversiones del controlador usan las bibliotecas de conversión de Windows, Linux o macOS. Cada biblioteca puede generar resultados distintos al realizar estas conversiones. Para obtener más información, consulte [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caracteres del área de uso privado y definidos por el usuario final).

- Si la codificación del cliente es UTF-8, el administrador de controladores no siempre convierte correctamente de UTF-8 a UTF-16. Actualmente, se producen daños en los datos cuando uno o varios caracteres de la cadena no son caracteres UTF-8 válidos. Los caracteres ASCII se asignan correctamente. El administrador de controladores intenta realizar esta conversión al llamar a las versiones de SQLCHAR de la API de ODBC (por ejemplo, SQLDriverConnectA). El Administrador de controladores no intentará realizar esta conversión al llamar a las versiones de SQLWCHAR de la API de ODBC (por ejemplo, SQLDriverConnectW).  

- El parámetro *ColumnSize* de **SQLBindParameter** hace referencia al número de caracteres en el tipo SQL, mientras que *BufferLength* es el número de bytes en el búfer de la aplicación. Pero si el tipo de datos de SQL es `varchar(n)` o `char(n)`, la aplicación enlaza el parámetro como SQL_C_CHAR o SQL_C_VARCHAR y la codificación de caracteres del cliente es UTF-8, es posible que obtenga un error "Datos tipo String, se truncarán por la derecha" del controlador, aunque el valor de *ColumnSize* se corresponda con el tamaño del tipo de datos del servidor. Este error se produce porque las conversiones entre las codificaciones de caracteres pueden cambiar la longitud de los datos. Por ejemplo, un carácter de apóstrofo derecho (U+2019) codificado en CP-1252 como 0x92 de un solo byte, pero en UTF-8 como la secuencia de 3 bytes 0xe2 0x80 0x99.

Por ejemplo, si la codificación es UTF-8 y especifica 1 para *BufferLength* y *ColumnSize* en **SQLBindParameter** para un parámetro de salida, y luego intenta recuperar el carácter anterior almacenado en una columna `char(1)` en el servidor (mediante CP-1252), el controlador intenta convertirlo a la codificación UTF-8 de 3 bytes, pero no puede ajustar el resultado en un búfer de 1 byte. En la otra dirección, el controlador compara *ColumnSize* con *BufferLength* en **SQLBindParameter** antes de realizar la conversión entre las diferentes páginas de códigos del cliente y el servidor. Dado que un parámetro *ColumnSize* con un valor de 1 es inferior a uno *BufferLength* con, por ejemplo, un valor de 3, el controlador generará un error. Para evitar este error, asegúrese de que la longitud de los datos después de la conversión se ajuste a la columna o al búfer especificados. El parámetro*ColumnSize* no puede ser superior a 8000 para el tipo `varchar(n)`.

## <a name="see-also"></a>Consulte también  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

