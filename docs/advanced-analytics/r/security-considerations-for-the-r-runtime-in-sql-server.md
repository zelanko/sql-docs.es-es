---
title: "Consideraciones de seguridad para el aprendizaje automático en SQL Server | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b5fba856cc40c11f218faf0a61f66ee5451aa4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Consideraciones de seguridad para el aprendizaje automático en SQL Server

Este artículo enumeran las consideraciones de seguridad que el administrador o el arquitecto debe tener en cuenta al usar los servicios de aprendizaje de máquina.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="use-a-firewall-to-restrict-network-access-by-r"></a>Utilice un firewall para restringir el acceso de red mediante R

En una instalación predeterminada, se utiliza una regla de firewall de Windows para bloquear todo el acceso de red saliente de los procesos del runtime de R. Se deben crear reglas de Firewall para impedir al proceso de runtime de R descargar paquetes o realizar otras llamadas de red que podrían ser malintencionadas.

Si usa otro programa de firewall, también puede crear reglas para bloquear la conexión de red saliente para el runtime de R estableciendo reglas para las cuentas de usuario locales o para el grupo representado por el grupo de cuentas de usuario.

Se recomienda encarecidamente que active Firewall de Windows (u otro firewall de su elección) para evitar el acceso de red sin restricciones por los tiempos de ejecución de R o Python.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Métodos de autenticación admitidos para contextos de proceso remoto

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]es compatible con los inicios de sesión de autenticación integrada de Windows y SQL al crear conexiones entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un cliente de ciencia de datos remotos.

Por ejemplo, si está desarrollando una solución de R en el equipo portátil y quiere realizar cálculos en el equipo de SQL Server, debe crear un origen de datos de SQL Server en R. Para ello, use las funciones **rx** y defina una cadena de conexión basada en sus credenciales de Windows.

Al cambiar la _cálculo_ desde su portátil al equipo de SQL Server, si la cuenta de Windows tiene los permisos necesarios, todo el código de R se ejecuta en el equipo de SQL Server. Además, las consultas SQL ejecutadas como parte del código de R se ejecutan bajo también sus credenciales.

También se admite el uso de inicios de sesión SQL en este escenario, que requiere que la instancia de SQL Server esté configurado para permitir la autenticación de modo mixto.

### <a name="implied-authentication"></a>Autenticación implícita

 En general, la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] inicia el tiempo de ejecución de scripts externos y ejecuta las secuencias de comandos en su propia cuenta. Sin embargo, si el tiempo de ejecución externo realiza una llamada ODBC, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] suplanta las credenciales del usuario que envía el comando para asegurarse de que la llamada ODBC no se producen errores. Esto se denomina *autenticación implícita*.
 
 > [!IMPORTANT]
 >
 > Para que la autenticación implícita se realice correctamente, el grupo de usuarios de Windows que contiene las cuentas de trabajo (de forma predeterminada, **SQLRUser**) debe tener una cuenta en la base de datos maestra para la instancia, y deben asignarse permisos a esta cuenta para conectarse a la instancia.
 > 
 > El grupo de **SQLRUser** también se utiliza al ejecutar scripts de Python. 

## <a name="no-support-for-encryption-at-rest"></a>No se admite para el cifrado en reposo

No se admite el cifrado de datos transparente para los datos enviados o recibidos desde el tiempo de ejecución de script externo. Como consecuencia, cifrado en reposo **no es** se aplicará a cualquier dato que se utilice en scripts de R o Python, ningún dato guardado en disco o ningún resultado intermedio persistente.

## <a name="resources"></a>Recursos

Para obtener más información acerca de cómo administrar el servicio y sobre cómo aprovisionar las cuentas de usuario utilizadas para ejecutar scripts de R, consulte [configurar y administrar extensiones de análisis avanzado](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Para obtener una descripción de la arquitectura de seguridad, vea:

+ [Introducción a la seguridad para R](security-overview-sql-server-r.md)
+ [Introducción a la seguridad para Python](../python/security-overview-sql-server-python-services.md)
