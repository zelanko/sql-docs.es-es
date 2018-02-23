---
title: "Problemas conocidos de esta versión del controlador de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 02/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- known issues
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ebc56810753f7cc269afa0f98ee6e2e56e959878
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2018
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemas conocidos en esta versión del controlador

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artículo contiene una lista de problemas conocidos de Microsoft ODBC Driver 13, 13.1 y 17 para SQL Server en Linux y macOS.

Se publicarán más problemas en el [blog del equipo de Microsoft ODBC Driver](http://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux y macOS convertir caracteres de forma diferente desde el área de uso privado (PUA) o caracteres de End User-Defined (EUDC). Las conversiones se realizan en el servidor de [!INCLUDE[tsql](../../../includes/tsql_md.md)] utilizar la biblioteca de conversión de Windows. Las conversiones del controlador usar las bibliotecas de conversión de Windows, Linux o Mac OS. Cada biblioteca puede producir resultados diferentes cuando se realizan estas conversiones. Para obtener más información, consulte [End-User-Defined and Private Use Area Characters](http://msdn.microsoft.com/library/dd317802.aspx)(Caracteres del área de uso privado y definidos por el usuario final).

- Si el cliente de codificación es UTF-8, el Administrador de controladores no siempre convierte correctamente de UTF-8 a UTF-16. Actualmente, daños en los datos se producen cuando uno o más caracteres de la cadena no son caracteres UTF-8 válidos. Caracteres ASCII están asignados correctamente. El Administrador de controladores intenta esta conversión al llamar a las versiones SQLCHAR de la API de ODBC (por ejemplo, SQLDriverConnectA). El Administrador de controladores no intentará realizar esta conversión al llamar a las versiones de SQLWCHAR de la API de ODBC (por ejemplo, SQLDriverConnectW).  

- El *ColumnSize* parámetro de **SQLBindParameter** hace referencia al número de caracteres en el tipo SQL, mientras que *BufferLength* es el número de bytes en la aplicación búfer. Sin embargo, si el tipo de datos SQL es `varchar(n)` o `char(n)`, la aplicación enlaza el parámetro como SQL_C_CHAR o SQL_C_VARCHAR y la codificación de caracteres del cliente es UTF-8, puede obtener un error de "datos de cadena, truncados por la derecha" desde el incluso si controlador la valor de *ColumnSize* se alinea con el tamaño del tipo de datos en el servidor. Este error se produce porque las conversiones entre codificaciones de caracteres pueden cambiar la longitud de los datos. Por ejemplo, un apóstrofo derecho caracteres (2019) está codificado en CP-1252 como el único byte 0 x 92, pero en UTF-8, como la secuencia de bytes de 3 0xe2 0x80 0x99.

Por ejemplo, si la codificación es UTF-8 y especifique 1 para ambos *BufferLength* y *ColumnSize* en **SQLBindParameter** para un parámetro out y, a continuación, intenta recuperar el carácter anterior almacenado en un `char(1)` columna en el servidor (mediante CP-1252), el controlador intenta convertirlo a la codificación de UTF-8 de 3 bytes, pero no puede ajustar el resultado en un búfer de 1 byte. En el otro sentido, compara *ColumnSize* con el *BufferLength* en **SQLBindParameter** antes de realizar la conversión entre páginas de códigos diferentes en el cliente y servidor. Dado que un parámetro *ColumnSize* con un valor de 1 es inferior a uno *BufferLength* con, por ejemplo, un valor de 3, el controlador generará un error. Para evitar este error, asegúrese de que la longitud de los datos después de conversión encaja en el búfer especificado o la columna. Tenga en cuenta que *ColumnSize* no puede ser mayor que 8000 para el `varchar(n)` tipo.

## <a name="see-also"></a>Vea también  
[Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)  

