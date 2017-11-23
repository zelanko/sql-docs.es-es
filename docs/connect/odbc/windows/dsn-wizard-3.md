---
title: Pantalla del asistente 3 (controlador ODBC para SQL Server) del origen de datos | Documentos de Microsoft
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a8803b1a18ce1a0987c9ebfcbd718345cfc3ef60
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="data-source-wizard-screen-3"></a>Pantalla 3 del Asistente de origen de datos

Especifique la base de datos predeterminada, diversas opciones de ANSI que va a usar el controlador y el nombre de un servidor reflejado.

## <a name="options"></a>Opciones

### <a name="change-the-default-database-to"></a>Cambiar la base de datos predeterminada

Especifica el nombre de la base de datos predeterminada para cualquier conexión establecida utilizando este origen de datos. Cuando este cuadro está desactivado, las conexiones utilizan la base de datos predeterminada definida para el identificador de inicio de sesión en el servidor. Cuando este cuadro está activado, la base de datos denominada en el cuadro invalida la base de datos predeterminada definida para el identificador de inicio de sesión. Si el **Adjuntar nombre de archivo de base de datos** cuadro contiene el nombre de un archivo principal, la base de datos descrita por el archivo principal se adjunta como una base de datos con el nombre de base de datos especificado en el **cambiar la base de datos predeterminada a**cuadro.

Utilizar la base de datos predeterminada para el identificador de inicio de sesión es más eficaz que especificar una base de datos predeterminada en el origen de datos ODBC.

### <a name="mirror-server"></a>Servidor reflejado

Especifica el nombre del asociado de conmutación por error de la base de datos que se va a reflejar. Si un nombre de base de datos no se muestra en el **cambiar la base de datos predeterminada a** cuadro, o el nombre que aparece es la base de datos de forma predeterminada, **servidor reflejado** está atenuado.

Si lo desea, puede especificar un nombre principal de servicio (SPN) para el servidor reflejado. El SPN para el servidor reflejado se utiliza para la autenticación mutua entre cliente y servidor.

### <a name="attach-database-filename"></a>Adjuntar el nombre de archivo de base de datos

Especifica el nombre del archivo principal de una base de datos que se puede adjuntar. Esta base de datos se adjunta y se utiliza como predeterminada para el origen de datos. Especifique la ruta de acceso completa y el nombre del archivo principal. El nombre de base de datos especificado en el **cambiar la base de datos predeterminada** cuadro se utiliza como el nombre de la base de datos adjunta.

### <a name="use-ansi-quoted-identifiers"></a>Usar identificadores entrecomillados ANSI

Especifica que QUOTED_IDENTIFIERS se active cuando se conecta el controlador ODBC para SQL Server. Cuando esta casilla está activada, SQL Server aplica las reglas ANSI con respecto a las comillas. Las comillas dobles solo se pueden utilizar para los identificadores, por ejemplo en los nombres de columna y de tabla. Las cadenas de caracteres se deben incluir entre comillas simples:

```
SELECT "LastName"
FROM "Person.Contact"
WHERE "LastName" = 'O''Brien'
```

Cuando esta casilla está desactivada, las aplicaciones que utilizan identificadores entrecomillados, como la utilidad Microsoft Query que se incluye con Microsoft Excel, encuentran errores al generar instrucciones SQL con identificadores entrecomillados.

### <a name="use-ansi-nulls-paddings-and-warnings"></a>Usar valores nulos, rellenos y advertencias ANSI

Especifica que las opciones ANSI_NULLS, ANSI_WARNINGS y ANSI_PADDINGS se active cuando se conecta el controlador ODBC para SQL Server.

Si la opción ANSI_NULLS está activada, el servidor exige las reglas ANSI relativas a la comparación de las columnas para NULL. La sintaxis de ANSI "IS NULL" o "IS NOT NULL" se debe utilizar para todas las comparaciones de NULL. La sintaxis de Transact-SQL "=NULL" no se admite.

Con ANSI_WARNINGS está activada, SQL Server emite mensajes de advertencia para las condiciones que infrinjan las reglas ANSI pero no infringen las reglas de Transact-SQL. Algunos ejemplos de tales errores son el truncamiento de datos en la ejecución de una instrucción UPDATE o INSERT, o encontrar un valor NULL durante una función de agregado. 

Con la opción ANSI_PADDING está activada, espacios en blanco finales en **varchar** valores iniciales y finales ceros en **varbinary** valores no se recortan automáticamente.

### <a name="application-intent"></a>Intento de aplicación

Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.

### <a name="multi-subnet-failover"></a>Conmutación por error de múltiples subredes.

Si la aplicación se conecta a un grupo de disponibilidad de (grupos de disponibilidad AlwaysOn) de recuperación de desastres alta disponibilidad (AG) en subredes diferentes, lo que permite **conmutación por error de múltiples subredes.** configura el controlador ODBC para SQL Server proporcionar una detección más rápida y conexión con el servidor (actualmente) activo.

### <a name="transparent-network-ip-resolution"></a>Resolución IP de red transparente.

Modifica el comportamiento de **conmutación por error de múltiples subredes** para permitir una reconexión más rápida durante la conmutación por error. Vea [utilizando resolución de IP de red transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md) para obtener más información.

### <a name="column-encryption"></a>Cifrado de columna.

Habilita el descifrado automático y el cifrado de las transferencias de datos a y desde columnas cifradas con la [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) característica disponible en SQL Server 2016 y versiones posterior.

### <a name="next"></a>Siguiente

Continúa en la siguiente pantalla del asistente.

### <a name="back"></a>Atrás

Vuelve a la pantalla anterior del asistente.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla 2 del Asistente de origen de datos](../../../connect/odbc/windows/dsn-wizard-2.md)

[Pantalla 4 del Asistente de origen de datos](../../../connect/odbc/windows/dsn-wizard-4.md)
