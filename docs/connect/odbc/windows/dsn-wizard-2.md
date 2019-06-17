---
title: Origen de datos de pantalla del asistente 2 (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: v-jizho2
manager: jroth
ms.openlocfilehash: 2c41b9215979488cbec9ebda89d98bb0f464d11a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797806"
---
# <a name="data-source-wizard-screen-2"></a>Pantalla del Asistente para orígenes de datos 2

Especifique el método de autenticación y configure las entradas de cliente avanzado de Microsoft SQL Server y el inicio de sesión y la contraseña que el controlador ODBC de SQL Server utilizará para conectarse a SQL Server mientras configura el origen de datos.

## <a name="options"></a>Opciones

### <a name="with-integrated-windows-authentication"></a>Con autenticación de Windows integrada

Especifica que el controlador solicita una conexión segura (o de confianza) a un servidor SQL Server. Una vez seleccionado, el servidor SQL Server utiliza la seguridad de inicio de sesión integrada para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor. Cualquier identificador o contraseña de inicio de sesión proporcionada no se tiene en cuenta. El administrador del sistema de SQL Server debe haber asociado su inicio de sesión de Windows con un identificador de inicio de sesión de SQL Server (por ejemplo, mediante el uso de SQL Server Management Studio).

También puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="with-active-directory-integrated-authentication"></a>Con la autenticación integrada de Active Directory

Especifica que el controlador de autenticarse en SQL Server mediante Azure Active Directory. Una vez seleccionado, SQL Server utiliza la seguridad de inicio de sesión integrada de Azure Active Directory para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor.

### <a name="with-sql-server-authentication"></a>Con autenticación de SQL Server

Especifica que el controlador de autenticarse en SQL Server mediante un identificador de inicio de sesión y contraseña.

### <a name="with-active-directory-password-authentication"></a>Con autenticación de contraseña de Active Directory

Especifica que el controlador de autenticarse en SQL Server mediante un identificador de inicio de sesión de Azure Active Directory y una contraseña.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticación interactiva de Active Directory

Especifica que el controlador de autenticarse en SQL Server mediante Azure Active Directory Interactive modo proporcionando el identificador de inicio de sesión. Esto desencadenará el cuadro de diálogo de autenticación de Windows Azure.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el identificador de inicio de sesión, el controlador utiliza al conectarse a SQL Server si **con autenticación de SQL Server mediante un identificador de inicio de sesión y la contraseña escrita por el usuario** o **autenticación con contraseña de Active Directory con un identificador de inicio de sesión y una contraseña escritos por el usuario** o **con un identificador de inicio de sesión de autenticación con Active Directory Interactive escrita por el usuario** está seleccionada. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el origen de datos una vez creado.

### <a name="password"></a>Contraseña

Especifica la contraseña que el controlador utiliza al conectarse a SQL Server si **con autenticación de SQL Server mediante un identificador de inicio de sesión y la contraseña escrita por el usuario** o **autenticación con contraseña de Active Directory con un identificador de inicio de sesión y una contraseña escritos por el usuario** está seleccionada. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el nuevo origen de datos.

Tanto el **Id. de inicio de sesión** y **contraseña** cuadros están deshabilitados si **autenticación con Windows integrada** o **con Active Directory integrado autenticación** está seleccionada.

### <a name="next"></a>Siguiente

Continúa en la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Devuelve a la pantalla anterior del asistente.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Pantalla del Asistente para orígenes de datos 3](../../../connect/odbc/windows/dsn-wizard-3.md)

