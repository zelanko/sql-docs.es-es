---
title: Pantalla del Asistente para 2 (controlador ODBC para SQL Server) del origen de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: 22
author: MightyPen
ms.author: v-jizho2
manager: craigg
ms.openlocfilehash: 96907675f7bdb1072923da9ad56412dd7dcd59c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-wizard-screen-2"></a>Pantalla del Asistente para orígenes de datos 2

Especifique el método de autenticación y configurar las entradas de cliente avanzado de Microsoft SQL Server y el inicio de sesión y la contraseña que usará el controlador ODBC para SQL Server para conectarse a SQL Server al configurar el origen de datos.

## <a name="options"></a>Opciones

### <a name="with-integrated-windows-authentication"></a>Con la autenticación integrada de Windows

Especifica que el controlador solicita una conexión segura (o de confianza) a un servidor SQL Server. Una vez seleccionado, el servidor SQL Server utiliza la seguridad de inicio de sesión integrada para establecer las conexiones con este origen de datos sin tener en cuenta el modo de seguridad de inicio de sesión actual del servidor. Cualquier identificador o contraseña de inicio de sesión proporcionada no se tiene en cuenta. El administrador del sistema de SQL Server debe haber asociado su inicio de sesión de Windows con un identificador de inicio de sesión de SQL Server (por ejemplo, mediante SQL Server Management Studio).

También puede especificar un nombre principal de servicio (SPN) para el servidor.

### <a name="with-active-directory-integrated-authentication"></a>Con la autenticación integrada de Active Directory

Especifica que el controlador se autentiquen en SQL Server con Azure Active Directory. Cuando se selecciona esta opción, SQL Server utiliza la seguridad de inicio de sesión de Azure Active Directory integrado para establecer una conexión con este origen de datos, independientemente del modo de seguridad de inicio de sesión actual en el servidor.

### <a name="with-sql-server-authentication"></a>Con la autenticación de SQL Server

Especifica que el controlador se autentiquen en SQL Server mediante un identificador de inicio de sesión y contraseña.

### <a name="with-active-directory-password-authentication"></a>Con la autenticación de contraseña de Active Directory

Especifica que el controlador se autentiquen en SQL Server mediante un identificador de inicio de sesión de Azure Active Directory y una contraseña.

### <a name="with-active-directory-interactive-authentication"></a>Con la autenticación de Active Directory interactivo

Especifica que el controlador se autentiquen en SQL Server con Azure Active Directory el modo interactivo proporcionando el identificador de inicio de sesión. Esto desencadenará el cuadro de diálogo de autenticación de Windows Azure.

### <a name="login-id"></a>Id. de inicio de sesión

Especifica el identificador de inicio de sesión al conectarse a SQL Server si se utiliza el controlador **con autenticación de SQL Server mediante un identificador de inicio de sesión y una contraseña escritos por el usuario** o **autenticación con Active Directory contraseña mediante un Id. de inicio de sesión y una contraseña escritos por el usuario** o **autenticación con Active Directory interactivo mediante un identificador de inicio de sesión especificado por el usuario** está seleccionada. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el origen de datos una vez creado.

### <a name="password"></a>Contraseña

Especifica la contraseña que el controlador utiliza al conectarse a SQL Server si **con autenticación de SQL Server mediante un identificador de inicio de sesión y una contraseña escritos por el usuario** o **autenticación con Active Directory contraseña mediante un Id. de inicio de sesión y una contraseña escritos por el usuario** está seleccionada. Esto solo se aplica a la conexión que se realiza para determinar la configuración de servidor predeterminada; no se aplica a las conexiones subsiguientes realizadas utilizando el nuevo origen de datos.

Tanto el **Id. de inicio de sesión** y **contraseña** cuadros están deshabilitados si **con autenticación integrada de Windows** o **con Active Directory integrado autenticación** está seleccionada.

### <a name="next"></a>Siguiente

Continúa en la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Vuelve a la pantalla anterior del asistente.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla 1 del Asistente de origen de datos](../../../connect/odbc/windows/dsn-wizard-1.md)

[Pantalla 3 del Asistente de origen de datos](../../../connect/odbc/windows/dsn-wizard-3.md)

