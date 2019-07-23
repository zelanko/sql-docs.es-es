---
title: Pantalla 2 del Asistente para orígenes de datos (controlador ODBC para SQL Server) | Microsoft Docs
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
ms.openlocfilehash: c997dd30b6d1e9844843ff4fa626c46b42fed463
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936571"
---
# <a name="data-source-wizard-screen-2"></a>Pantalla del Asistente para orígenes de datos 2

Especifique el método de autenticación y configure las entradas de cliente avanzado de Microsoft SQL Server y el inicio de sesión y la contraseña que el controlador ODBC de SQL Server utilizará para conectarse a SQL Server mientras configura el origen de datos.

## <a name="options"></a>Opciones

### <a name="with-integrated-windows-authentication"></a>Con autenticación de Windows integrada

Especifica que el controlador solicite una conexión segura (o de confianza) a un SQL Server. Una vez seleccionado, el servidor SQL Server utiliza la seguridad de inicio de sesión integrada para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor. Cualquier identificador o contraseña de inicio de sesión proporcionada no se tiene en cuenta. El administrador del sistema de SQL Server debe haber asociado su inicio de sesión de Windows con un ID. de inicio de sesión de SQL Server (por ejemplo, mediante el uso de SQL Server Management Studio).

También puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="with-active-directory-integrated-authentication"></a>Con la autenticación integrada de Active Directory

Especifica que el controlador se autentique en SQL Server mediante Azure Active Directory. Una vez seleccionado, SQL Server utiliza la seguridad de inicio de sesión integrada de Azure Active Directory para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor.

### <a name="with-sql-server-authentication"></a>Con autenticación de SQL Server

Especifica que el controlador se autentique en SQL Server mediante un identificador de inicio de sesión y una contraseña.

### <a name="with-active-directory-password-authentication"></a>Con autenticación de contraseña de Active Directory

Especifica que el controlador se autentique en SQL Server mediante un identificador de inicio de sesión de Azure Active Directory y una contraseña.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticación interactiva de Active Directory

Especifica que el controlador se autentique en SQL Server mediante Azure Active Directory modo interactivo proporcionando el identificador de inicio de sesión. Esto desencadenará el cuadro de diálogo de solicitud de autenticación de Windows Azure.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el identificador de inicio de sesión que utiliza el controlador al conectarse a SQL Server si **con la autenticación de SQL Server mediante un identificador de inicio de sesión y una contraseña escritos por el usuario** o **con Active Directory autenticación de contraseña mediante un identificador de inicio de sesión y una contraseña escritos por el usuario.** o bien **, con Active Directory autenticación interactiva mediante un identificador de inicio de sesión especificado por el usuario** está seleccionado. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el origen de datos una vez creado.

### <a name="password"></a>Contraseña

Especifica la contraseña que el controlador utiliza al conectarse a SQL Server si **con la autenticación de SQL Server mediante un identificador de inicio de sesión y una contraseña escritos por el usuario** o **con Active Directory autenticación de contraseña mediante un identificador de inicio de sesión y una contraseña escritos por el usuario.** está seleccionado. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el nuevo origen de datos.

Los cuadros **ID** . de inicio de sesión y **contraseña** están deshabilitados si está seleccionada la opción **con la autenticación integrada de Windows** o **con Active Directory autenticación integrada** .

### <a name="next"></a>Siguiente

Avanza a la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Vuelve a la pantalla anterior del asistente.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Pantalla del Asistente para orígenes de datos 3](../../../connect/odbc/windows/dsn-wizard-3.md)

