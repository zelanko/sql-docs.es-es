---
title: Pantalla del Asistente para orígenes de datos 2 (ODBC Driver for SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: David-Engel
ms.author: v-jizho2
ms.openlocfilehash: e2e6b323428b1ad8ae188ea65bf10382651d3d71
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928249"
---
# <a name="data-source-wizard-screen-2"></a>Pantalla del Asistente para orígenes de datos 2

Especifique el método de autenticación y configure las entradas de cliente avanzado de Microsoft SQL Server y el inicio de sesión y la contraseña que el controlador ODBC de SQL Server utilizará para conectarse a SQL Server mientras configura el origen de datos.

## <a name="options"></a>Opciones

### <a name="with-integrated-windows-authentication"></a>Con autenticación de Windows integrada

Especifica que el controlador solicite una conexión segura (o de confianza) a un servidor SQL Server. Una vez seleccionado, el servidor SQL Server utiliza la seguridad de inicio de sesión integrada para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor. Cualquier identificador o contraseña de inicio de sesión proporcionada no se tiene en cuenta. El administrador del sistema de SQL Server debe haber asociado su inicio de sesión de Windows a un identificador de inicio de sesión de SQL Server (por ejemplo, mediante SQL Server Management Studio).

También puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="with-active-directory-integrated-authentication"></a>Con la autenticación integrada de Active Directory

Especifica que el controlador se autentique en SQL Server mediante Azure Active Directory. Una vez seleccionado, SQL Server utiliza la seguridad de inicio de sesión integrada de Azure Active Directory para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor.

### <a name="with-sql-server-authentication"></a>Con autenticación de SQL Server

Especifica que el controlador se autentique en SQL Server mediante un id. y una contraseña de inicio de sesión.

### <a name="with-active-directory-password-authentication"></a>Con autenticación de contraseña de Active Directory

Especifica que el controlador se autentique en SQL Server mediante un id. y una contraseña de inicio de sesión de Azure Active Directory.

### <a name="with-active-directory-interactive-authentication"></a>Con autenticación interactiva de Active Directory

Especifica que el controlador se autentique en SQL Server mediante el modo Azure Active Directory interactivo proporcionando un id. de inicio de sesión. Esto desencadenará el cuadro de diálogo de pedidos Autenticación de Azure.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el id. de inicio de sesión que usa el controlador al conectarse a SQL Server si se selecciona **Con la autenticación de SQL Server, mediante un identificador de inicio de sesión y una contraseña escritos por el usuario**, **Con la autenticación de contraseña de Active Directory, mediante un id. de inicio de sesión y una contraseña especificados por el usuario** o **Con la autenticación interactiva de Active Directory, mediante un id. de inicio de sesión especificado por el usuario**. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el origen de datos una vez creado.

### <a name="password"></a>Contraseña

Especifica la contraseña que usa el controlador al conectarse a SQL Server si se selecciona **Con la autenticación de SQL Server, mediante un identificador de inicio de sesión y una contraseña escritos por el usuario** o **Con la autenticación de contraseña de Active Directory, mediante un id. de inicio de sesión y una contraseña especificados por el usuario**. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el nuevo origen de datos.

Tanto la casilla **Id. de inicio de sesión** como **Contraseña** están deshabilitadas si se selecciona **Con autenticación de Windows integrada** o **Con la autenticación integrada de Active Directory**.

### <a name="next"></a>Siguiente

Avanza a la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Vuelve a la pantalla del asistente anterior.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 1](../../../connect/odbc/windows/dsn-wizard-1.md)

[Pantalla del Asistente para orígenes de datos 3](../../../connect/odbc/windows/dsn-wizard-3.md)

