---
title: Microsoft ODBC Driver for SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e867bb283434a6a7ae515823b370c73e4df4e131
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Controlador ODBC de Microsoft para SQL Server

![Descarga-CTRL+MAYÚS+TAB-dentro de un círculo](../../ssdt/media/download.png)[para descargar el controlador ODBC](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ODBC es la API de acceso de datos nativo principal para aplicaciones escritas en C y C++ para SQL Server. No hay un controlador ODBC para la mayoría de los orígenes de datos. Otros lenguajes que pueden usar ODBC incluyen COBOL, Perl, PHP y Python. ODBC se usa ampliamente en escenarios de integración de datos.

El controlador ODBC incluye herramientas como [ **sqlcmd** ](https://msdn.microsoft.com/library/ms162773.aspx) y [ **bcp**](https://msdn.microsoft.com/library/ms162802.aspx). El **sqlcmd** utilidad le permite ejecutar instrucciones Transact-SQL, procedimientos del sistema y secuencias de comandos SQL. El **bcp** forma masiva copia los datos entre una instancia de Microsoft SQL Server y un archivo de datos en un formato que elija. Puede usar **bcp** para importar muchas filas nuevas en tablas de SQL Server o para exportar datos de tablas a archivos de datos.  

## <a name="code-example-in-c"></a>Ejemplo de código de C++

Tenemos un archivo .zip pequeño que contiene el código fuente de un programa de C++ que utiliza ODBC:

- [Ejemplo de código de C++, con ODBC](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>Descargar

- ![Descarga-CTRL+MAYÚS+TAB-dentro de un círculo](../../ssdt/media/download.png)[para descargar el controlador ODBC](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

## <a name="documentation"></a>Documentación  

### <a name="linux-and-macos"></a>Linux y Mac OS

- [Instalar el controlador](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Conectar con **bcp**](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [Conectar con **sqlcmd**](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [Mediante la autenticación integrada (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)
- [Palabras clave de cadena de conexión y los nombres de origen de datos](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [Seguimiento de acceso a datos](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [Preguntas más frecuentes](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [Instalar al administrador de controladores](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [Problemas conocidos](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [Instrucciones de programación](../../connect/odbc/linux-mac/programming-guidelines.md)
- [Notas de la versión](../../connect/odbc/linux-mac/release-notes.md)
- [Compatibilidad con alta disponibilidad y recuperación ante desastres](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)

### <a name="windows"></a>Windows

- [Ejemplo de ejecución asincrónica (método de notificación)](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Resistencia de conexión en el controlador ODBC de Windows](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [Agrupación de conexiones dependientes del controlador](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [Características y cambios de comportamiento](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [Notas de la versión](../../connect/odbc/windows/release-notes.md)
- [Requisitos del sistema, instalación y archivos de controlador](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)

### <a name="features"></a>Características

- [Proveedores de almacén de claves personalizados](../../connect/odbc/custom-keystore-providers.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (las características disponibles también se aplican, sin OLEDB, ODBC Driver for SQL Server)
- [Siempre usar cifrado](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Con Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [Utilizando la resolución de IP de red transparente](../../connect/odbc/using-transparent-network-ip-resolution.md)

## <a name="community"></a>Comunidad  
- [Blog del equipo de Microsoft ODBC Driver for SQL Server](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [Foro para el acceso a los datos de SQL Server](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  

