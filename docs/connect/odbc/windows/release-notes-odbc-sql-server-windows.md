---
title: Notas de la versión de ODBC a SQL Server en Windows | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
ms.reviewer: v-chojas
author: v-makouz
ms.author: v-chojas
manager: kenvh
ms.openlocfilehash: 76ffaac48e8af454e887fd4fd30540eed4c4b453
ms.sourcegitcommit: 9bdecafd1aefd388137ff27dfef532a8cb0980be
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2020
ms.locfileid: "77173518"
---
# <a name="release-notes-for-odbc-to-sql-server-on-windows"></a>Notas de la versión de ODBC a SQL Server en Windows

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este artículo sobre notas de la versión se describen las novedades de Microsoft ODBC Driver para SQL Server en Windows.

<!--
PLEASE USE THE STANDARD 2-COLUMN TABLE FORMAT!

For all our Release Notes articles (What's New too?), we are standardizing on the 2-column format that you see here for version "## 17.3".

Going forward, all new additions to this article must use the 2-column format.

Also, use the shorter ## H2 title format, which eliminates all the redundant constants, and appends the date-added.
One beneift of shortness is the avoidance of the annoying wrapping of unnecessarily long H2 titles in the rightNav.
- OLD H2:  ## What's New in the [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] on Windows
- NEW H2:  ## 17.3, February 2019

By the way, in GitHub, the file name is changing today 2019/03/30:
- FROM:  docs/connect/odbc/windows/release-notes.md
- TO  :  docs/connect/odbc/windows/release-notes-odbc-sql-server-windows.md

Thank you.
GeneMi (and CraigG).  2019/03/30.
-->

## <a name="175-january-2020"></a>17.5, enero de 2020

| Característica agregada | Detalles |
| :------------ | :------ |
| Atributo de conexión SQL_COPT_SS_SPID para recuperar el SPID sin recorrido de ida y vuelta al servidor | Consulte [Atributos y palabras clave de cadena de conexión y DNS](../dsn-connection-string-attribute.md). |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="1742-october-2019"></a>17.4.2, octubre de 2019

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con puntos de conexión de Azure Key Vault adicionales | Consulte [Uso de Always Encrypted con ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Compatibilidad con la configuración de la versión de clasificación de datos | Vea [Clasificación de datos](../data-classification.md#bkmk-version). |
| Incluye la biblioteca de autenticación de Azure Active Directory (ADAL) y el instalador. | Ahora incluido en la instalación del controlador base, actualizará las instalaciones existentes de la Biblioteca de autenticación de Active Directory para SQL Server, quitándolas de la lista de aplicaciones instaladas en Windows. |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="174-july-2019"></a>17.5, julio de 2019

| Característica agregada | Detalles |
| :------------ | :------ |
| Always Encrypted con enclaves seguros. | Consulte [Uso de Always Encrypted con ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md). |
| Configuración de Mantener conexión TCP configurable. | Consulte [Conectarse a SQL Server](../linux-mac/connection-string-keywords-and-data-source-names-dsns.md). |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="173-february-2019"></a>17.3, febrero de 2019

| Característica agregada | Detalles |
| :------------ | :------ |
| Modo de autenticación de Azure Active Directory Managed Service Identity (del sistema y asignado por el usuario). | Consulte [Uso de Azure Active Directory con el controlador ODBC](../using-azure-active-directory.md). |
| Capacidad de transmitir en secuencias los parámetros de entrada con columnas Always Encrypted. | Vea [Limitations of the ODBC driver when using Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted) (Limitaciones del controlador ODBC al usar Always Encrypted). |
| Transacciones distribuidas XA. | [Uso de las transacciones XA](../use-xa-with-dtc.md). |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="172-july-2018"></a>17.2, julio de 2018

| Característica agregada | Detalles |
| :------------ | :------ |
| Clasificación de datos para Azure SQL Database y SQL Server. | Vea [Clasificación de datos](../data-classification.md). |
| Compatibilidad con la codificación de servidor UTF-8. | &nbsp; |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="171-march-2018"></a>17.1, marzo de 2018

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con atributos de conexión de `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS`. | &bull; &nbsp; `SQL_COPT_SS_CEKCACHETTL`<br/>Permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como vaciarla.<br/><br/>&bull; &nbsp; `SQL_COPT_SS_TRUSTEDCMKPATHS`<br/>Permite que la aplicación restrinja las operaciones de AE para que solo usen la lista especificada de claves maestras de columna.<br/><br/> Para obtener más información, vea [Using Always Encrypted with the ODBC Driver for SQL Server](../using-always-encrypted-with-the-odbc-driver.md) (Uso de Always Encrypted con el controlador ODBC para SQL Server). |
| Compatibilidad con la autenticación interactiva de Azure Active Directory | &nbsp; |
| Correcciones de errores. | Vea [Correcciones de errores](../bug-fixes.md). |
| &nbsp; | &nbsp; |

## <a name="17-february-2018"></a>17, febrero de 2018

| Característica agregada | Detalles |
| :------------ | :------ |
| Compatibilidad con Always Encrypted para la API de BCP. | &nbsp; |
| Nuevo atributo de cadena de conexión.`UseFMTOnly` | Hace que el controlador use los metadatos heredados en casos especiales que requieren tablas temporales. |
| Compatibilidad con Instancia administrada de Azure SQL. | Versión preliminar privada ampliada.<br/><br/>Vea la siguiente lista de [diferencias al usar Instancia administrada (versión 17 de ODBC)](#diffs-managed-instance-17). |
| &nbsp; | &nbsp; |

| Dependencia modificada | Detalles |
| :------------ | :------ |
| Se eliminó el ayudante para el inicio de sesión de Microsoft Online Services | Se ha eliminado la dependencia. |
| &nbsp; | &nbsp; |

### <a name="diffs-managed-instance-17"></a> Diferencias cuando se usa Instancia administrada (versión 17 de ODBC)

Esta versión es compatible con Instancia administrada de Azure SQL (versión preliminar privada ampliada). Vea la siguiente lista de diferencias cuando se usa Instancia administrada.

> [!NOTE]
> Hay varias diferencias cuando se usa Instancia administrada:
>
> - No se admite FILESTREAM.
> - No se admite el acceso al sistema de archivos local, pero es necesario para algunas cosas como los archivos de seguimiento.
> - No es posible crear el UDT desde la ruta de acceso local.
> - No se admite la Autenticación integrada de Windows.
> - No se admite DTC.
> - La cuenta `sa` no está presente (la cuenta predeterminada se denomina `cloudSA`).
> - El ERROR de token TDS (0xAA) devuelve un nombre de servidor incorrecto.
> - No se admiten caracteres especiales en el nombre de la base de datos.
> - No se admite ALTER DATABASE [dbname1] MODIFY NAME = [dbname2].
> - Los mensajes de error siempre se muestran en inglés, independientemente de la configuración de idioma (igual que Azure).

## <a name="131"></a>13.1

| Característica agregada | Detalles |
| :------------ | :------ |
| La versión 13.1 del controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agrega compatibilidad para [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) y [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md). | Estas compatibilidades agregadas están disponibles al conectarse a Microsoft SQL Server 2016 o a una versión posterior. |
| Hay atributos y palabras clave de agrupaciones de conexiones, que corresponden a las compatibilidades para Always Encrypted y Azure Active Directory. | Estas palabras clave y atributos se describen en [Agrupación de conexiones dependientes de controlador en el controlador ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md). |
| &nbsp; | &nbsp; |

## <a name="13"></a>13

| Característica agregada | Detalles |
| :------------ | :------ |
| Agrega compatibilidad para Microsoft SQL Server 2016. | Conserva la funcionalidad de la versión 11 del controlador ODBC. |
| &nbsp; | &nbsp; |

## <a name="11"></a>11

| Característica agregada | Detalles |
| :------------ | :------ |
| Contiene nuevas características. | Vea [Características de Microsoft ODBC Driver para SQL Server en Windows](features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md). |
| Contiene todas las características que se incluyen con ODBC en SQL Server 2012 Native Client. | &nbsp; |
| &nbsp; | &nbsp; |
