---
title: Escenarios de seguridad de aplicaciones en SQL Server
description: Contiene temas que describen diferentes escenarios de seguridad de aplicaciones para aplicaciones de ADO.NET y SQL Server.
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 711086e881951d9e82fd34851c451e5472e49d7e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452341"
---
# <a name="application-security-scenarios-in-sql-server"></a>Escenarios de seguridad de aplicaciones en SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

No existe una única manera correcta de crear una aplicación cliente de SQL Server segura. Cada aplicación es única en sus requisitos, en el entorno de implementación y en el rellenado de usuarios. Una aplicación que es razonablemente segura cuando está implementada inicialmente puede volverse menos segura con el tiempo. No es posible predecir con precisión qué amenazas pueden surgir en el futuro.  
  
SQL Server, como producto, ha evolucionado muchas versiones para incorporar las características de seguridad más recientes que permiten a los desarrolladores crear aplicaciones de base de datos seguras. Sin embargo, la seguridad no se incluye en el cuadro; requiere una supervisión y una actualización continuas.  
  
## <a name="common-threats"></a>Amenazas comunes  
Los desarrolladores deben comprender las amenazas de seguridad, las herramientas proporcionadas para contrarrestarlas y cómo evitar las carencias de seguridad. La seguridad se puede considerar mejor como una cadena, en la que una interrupción en cualquier vínculo pone en peligro la seguridad del todo. La lista siguiente incluye algunas amenazas de seguridad comunes que se describen con más detalle en los temas de esta sección.  
  
### <a name="sql-injection"></a>Inyección de código SQL  
La inyección de SQL es el proceso por el que un usuario malintencionado escribe instrucciones Transact-SQL en lugar de entradas válidas. Si la entrada se pasa directamente al servidor sin ser validada y la aplicación ejecuta accidentalmente el código inyectado, el ataque tiene la posibilidad de dañar o destruir datos. Para evitar ataques de inyección de SQL Server, puede usar procedimientos almacenados y comandos con parámetros, con lo que se evita el SQL dinámico y se restringen los permisos en todos los usuarios.  
  
### <a name="elevation-of-privilege"></a>Elevación de privilegios  
Los ataques de elevación de privilegios se producen cuando un usuario puede asumir los privilegios de una cuenta de confianza, como un propietario o administrador. Ejecútelo siempre con cuentas de usuario con privilegios mínimos y asigne solo los permisos necesarios. Evite el uso de cuentas administrativas o de propietario para ejecutar código. Esto limita la cantidad de daños que pueden producirse si un ataque se realiza correctamente. Cuando realice tareas que requieran permisos adicionales, use la firma de procedimiento o la suplantación solo mientras dure la tarea. Puede firmar procedimientos almacenados con certificados o usar la suplantación para asignar permisos temporalmente.  
  
### <a name="probing-and-intelligent-observation"></a>Sondeo y observación inteligente  
Un ataque de sondeo puede utilizar los mensajes de error generados por una aplicación para buscar vulnerabilidades de seguridad. Implemente el control de errores en todo el código de procedimiento para evitar que se devuelva SQL Server información de error al usuario final.  
  
### <a name="authentication"></a>Autenticación  
Se puede producir un ataque por inyección de cadena de conexión al utilizar SQL Server inicios de sesión si una cadena de conexión basada en la entrada del usuario se construye en tiempo de ejecución. Si en la cadena de conexión no se comprueba si hay pares de palabras clave válidos, un atacante puede insertar caracteres adicionales, tener acceso a datos confidenciales o a otros recursos del servidor. Use la autenticación de Windows siempre que sea posible. Si debe utilizar inicios de sesión de SQL Server, utilice la <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> para crear y validar cadenas de conexión en tiempo de ejecución.  
  
### <a name="passwords"></a>Contraseñas  
Muchos ataques tienen éxito porque un intruso pudo obtener o adivinar una contraseña para un usuario con privilegios. Las contraseñas son la primera línea de defensa contra los intrusos, por lo que establecer contraseñas seguras es esencial para la seguridad del sistema. Crear y aplicar directivas de contraseñas para la autenticación en modo mixto.  
  
Asigne siempre una contraseña segura a la cuenta `sa`, incluso cuando use la autenticación de Windows.  
  
## <a name="in-this-section"></a>En esta sección  
[Escritura de SQL dinámico seguro en SQL Server](writing-secure-dynamic-sql.md)  
Describe técnicas para escribir SQL dinámico seguro mediante procedimientos almacenados.  

## <a name="next-steps"></a>Pasos siguientes
- [Seguridad de SQL Server](sql-server-security.md)
