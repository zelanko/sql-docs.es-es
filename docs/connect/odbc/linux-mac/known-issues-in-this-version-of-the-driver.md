---
title: Problemas conocidos del controlador ODBC en Linux y macOS
description: Obtenga información sobre problemas conocidos de Microsoft ODBC Driver for SQL Server en Linux y macOS y conozca los pasos para solucionar problemas de conectividad.
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6729d46fe498c6efe8e49f941c0ef1b007870b2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727406"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Problemas conocidos del controlador ODBC en Linux y macOS

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artículo contiene una lista de problemas conocidos de Microsoft ODBC Driver 13, 13.1 y 17 para SQL Server en Linux y macOS. También contiene pasos para solucionar problemas de conectividad.

## <a name="known-issues"></a>Problemas conocidos

Se irán publicando más problemas en el [blog de controladores de SQL Server](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers).  

- Debido a las limitaciones de la biblioteca del sistema, Alpine Linux admite menos codificaciones de caracteres y configuraciones regionales. Por ejemplo, en_US.UTF-8 no está disponible. Para más información, vea [musl libc: diferencias funcionales con respecto a glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html).

- Windows, Linux y macOS pueden convertir caracteres del área de uso privado (PUA) o caracteres definidos por el usuario final (EUDC) de forma diferente. Las conversiones que se realizan en el servidor de [!INCLUDE[tsql](../../../includes/tsql-md.md)] usan la biblioteca de conversión de Windows. Las conversiones del controlador usan las bibliotecas de conversión de Windows, Linux o macOS. Cada biblioteca puede generar resultados distintos al realizar estas conversiones. Para obtener más información, consulte [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caracteres del área de uso privado y definidos por el usuario final).

- Si la codificación del cliente es UTF-8, el administrador de controladores no siempre convierte correctamente de UTF-8 a UTF-16. Actualmente, se producen daños en los datos cuando uno o varios caracteres de la cadena no son caracteres UTF-8 válidos. Los caracteres ASCII se asignan correctamente. El administrador de controladores intenta realizar esta conversión al llamar a las versiones de SQLCHAR de la API de ODBC (por ejemplo, SQLDriverConnectA). El Administrador de controladores no intentará realizar esta conversión al llamar a las versiones de SQLWCHAR de la API de ODBC (por ejemplo, SQLDriverConnectW).  

- El parámetro *ColumnSize* de **SQLBindParameter** hace referencia al número de caracteres en el tipo SQL, mientras que *BufferLength* es el número de bytes en el búfer de la aplicación. Pero si el tipo de datos de SQL es `varchar(n)` o `char(n)`, la aplicación enlaza el parámetro como SQL_C_CHAR o SQL_C_VARCHAR y la codificación de caracteres del cliente es UTF-8, es posible que obtenga un error "Datos tipo String, se truncarán por la derecha" del controlador, aunque el valor de *ColumnSize* se corresponda con el tamaño del tipo de datos del servidor. Este error se produce porque las conversiones entre las codificaciones de caracteres pueden cambiar la longitud de los datos. Por ejemplo, un carácter de apóstrofo derecho (U+2019) codificado en CP-1252 como 0x92 de un solo byte, pero en UTF-8 como la secuencia de 3 bytes 0xe2 0x80 0x99.

Por ejemplo, si la codificación es UTF-8 y especifica 1 para *BufferLength* y *ColumnSize* en **SQLBindParameter** para un parámetro de salida, y luego intenta recuperar el carácter anterior almacenado en una columna `char(1)` en el servidor (mediante CP-1252), el controlador intenta convertirlo a la codificación UTF-8 de 3 bytes, pero no puede ajustar el resultado en un búfer de 1 byte. En la otra dirección, el controlador compara *ColumnSize* con *BufferLength* en **SQLBindParameter** antes de realizar la conversión entre las diferentes páginas de códigos del cliente y el servidor. Dado que un parámetro *ColumnSize* con un valor de 1 es inferior a uno *BufferLength* con, por ejemplo, un valor de 3, el controlador generará un error. Para evitar este error, asegúrese de que la longitud de los datos después de la conversión se ajuste a la columna o al búfer especificados. El parámetro*ColumnSize* no puede ser superior a 8000 para el tipo `varchar(n)`.

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a> Solución de problemas de conexión  

Si no se puede establecer una conexión con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el controlador ODBC, utilice la siguiente información para identificar el problema.  
  
El problema de conexión más común es que existan dos copias instaladas del Administrador de controladores unixODBC. Busque libodbc\*.so\*en /usr. Si ve más de una versión del archivo, posiblemente signifique que tiene instalado más de un administrador de controladores. La aplicación podría utilizar una versión incorrecta.
  
Habilite el registro de conexión editando el archivo `/etc/odbcinst.ini` para que contenga la siguiente sección con estos elementos:

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
Si obtiene otro error de conexión y no ve un archivo de registro, posiblemente signifique que tiene dos copias del Administrador de controladores en el equipo. De lo contrario, los resultados del registro deberían ser similares a los siguientes:  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 17 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
Si la codificación de caracteres ASCII no es UTF-8, por ejemplo: 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
hay más de un administrador de controladores instalados y la aplicación utiliza el incorrecto, o bien el administrador de controladores no se creó correctamente.  
  
Para obtener más información sobre cómo resolver errores de conexión, consulte:  

- [Pasos para solucionar problemas de conectividad de SQL](/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [Solución de problemas de conectividad de SQL Server 2005 (parte I)](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [Solución de problemas de conectividad en SQL Server 2008 con el búfer en anillo de conectividad](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [Solucionador de problemas de autenticación de SQL Server](/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>Pasos siguientes

Para obtener instrucciones sobre la instalación del controlador ODBC, vea los artículos siguientes:

- [Instalación de Microsoft ODBC Driver for SQL Server en Linux](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Instalación de Microsoft ODBC Driver for SQL Server en macOS](install-microsoft-odbc-driver-sql-server-macos.md)

Para obtener más información, vea las [Instrucciones de programación](programming-guidelines.md) y las [Notas de la versión](release-notes-odbc-sql-server-linux-mac.md).