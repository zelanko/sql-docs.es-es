---
title: "Consideraciones de seguridad para el aprendizaje automático en SQL Server | Documentos de Microsoft"
ms.date: 11/16/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 8c1cc4c65d35f6c2806a9890464cccfb6c621494
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="security-considerations-for-machine-learning-in-sql-server"></a>Consideraciones de seguridad para el aprendizaje automático en SQL Server

Este artículo enumeran las consideraciones de seguridad que el administrador o el arquitecto debe tener en cuenta al usar los servicios de aprendizaje de máquina.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="use-a-firewall-to-restrict-network-access"></a>Utilice un firewall para restringir el acceso de red

En una instalación predeterminada, se utiliza una regla de firewall de Windows para bloquear todo el acceso de red saliente desde procesos externos en tiempo de ejecución. Deben crear reglas de Firewall para impedir que los procesos externos en tiempo de ejecución de la descarga de paquetes o realizar otras llamadas de red que podrían ser malintencionadas.

Si está utilizando otro programa de firewall, también puede crear reglas para bloquear la conexión de red saliente para tiempos de ejecución externos, estableciendo reglas para las cuentas de usuario local o para el grupo representado por el grupo de cuentas de usuario.

Se recomienda encarecidamente que active Firewall de Windows (u otro firewall de su elección) para evitar el acceso de red sin restricciones por los tiempos de ejecución de R o Python.

## <a name="authentication-methods-supported-for-remote-compute-contexts"></a>Métodos de autenticación admitidos para contextos de proceso remoto

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]es compatible con los inicios de sesión de autenticación integrada de Windows y SQL al crear conexiones entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un cliente de ciencia de datos remotos.

Por ejemplo, supongamos que está desarrollando una solución en R en su equipo portátil y realizar cálculos en el equipo de SQL Server. Debe crear un origen de datos de SQL Server en R, utilizando la **rx** funciones y la definición de una cadena de conexión en función de sus credenciales de Windows.

Al cambiar la _cálculo_ desde su portátil al equipo de SQL Server, todo el código de R se ejecuta en el equipo de SQL Server, si la cuenta de Windows tiene los permisos necesarios. Además, las consultas SQL ejecutadas como parte del código de R se ejecutan bajo también sus credenciales.

También se admite el uso de inicios de sesión SQL en este escenario. Sin embargo, esto requiere que la instancia de SQL Server se configura para permitir la autenticación de modo mixto.

### <a name="implied-authentication"></a>Autenticación implícita

 En general, la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] inicia el tiempo de ejecución de scripts externos y ejecuta las secuencias de comandos en su propia cuenta. Sin embargo, si el tiempo de ejecución externo realiza una llamada ODBC, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] suplanta las credenciales del usuario que envía el comando para asegurarse de que la llamada ODBC no se producen errores. Esto se denomina *autenticación implícita*.
 
 > [!IMPORTANT]
 > Para que la autenticación implícita se realice correctamente, el grupo de usuarios de Windows que contiene las cuentas de trabajo (de forma predeterminada, **SQLRUser**) debe tener una cuenta en la base de datos maestra para la instancia, y deben asignarse permisos a esta cuenta para conectarse a la instancia.
 > 
 > El grupo de **SQLRUser** también se utiliza al ejecutar scripts de Python. 

En general, se recomienda que se mover conjuntos de datos grandes en SQL Server con antelación, en lugar de intentar leer datos con RODBC u otra biblioteca. Además, utilice una consulta de SQL Server o la vista como el origen de datos principal, para mejorar el rendimiento. 

Por ejemplo, puede obtener los datos de entrenamiento (normalmente, los datos más grandes) de SQL Server y obtener una lista de factores desde un origen externo. Puede definir un servidor vinculado para obtener datos de la mayoría de los orígenes de datos ODBC. Para obtener más información, consulte [crear un servidor vinculado](https://docs.microsoft.com/sql/relational-databases/linked-servers/create-linked-servers-sql-server-database-engine).

Para minimizar la dependencia en las llamadas ODBC a orígenes de datos externos, también puede realizar ingeniería de datos como un proceso independiente y guardar los resultados en una tabla o usar T-SQL. Vea este tutorial para un buen ejemplo de ingeniería de datos en SQL vs. R: [crear características de datos mediante T-SQL](../tutorials/sqldev-create-data-features-using-t-sql.md).

## <a name="no-support-for-encryption-at-rest"></a>No se admite para el cifrado en reposo

[Cifrado de datos transparente (TDE)](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption) no se admite para los datos enviados o recibidos desde el tiempo de ejecución de script externo. El motivo es que R (o Python) se ejecuta fuera del proceso de SQL Server; por lo tanto, los datos utilizados por el tiempo de ejecución externo no está protegidos por las características de cifrado del motor de base de datos.  Este comportamiento es similar a cualquier otro cliente que se ejecuta en el equipo de SQL Server que lee datos de la base de datos y realiza una copia.

Como consecuencia, TDE **no** aplicar a los datos que se utilice en scripts de R o Python, o a ningún dato guardado en disco, o en ningún resultado intermedio persistente. Sin embargo, otros tipos de cifrado, como el cifrado de BitLocker de Windows o aplicaciones de terceros que se aplicarán en el nivel de archivo o carpeta, todavía se aplican.

En el caso de [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/overview-of-key-management-for-always-encrypted), tiempos de ejecución externos no tienen acceso a las claves de cifrado; por lo tanto, no se puede enviar datos a las secuencias de comandos.

## <a name="resources"></a>Recursos

Para obtener más información acerca de cómo administrar el servicio y sobre cómo aprovisionar las cuentas de usuario usadas para ejecutar scripts de aprendizaje de máquina, vea [configurar y administrar extensiones de análisis avanzado](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md).

Para obtener una explicación de la arquitectura de seguridad general, consulte:

+ [Introducción a la seguridad para R](security-overview-sql-server-r.md)
+ [Introducción a la seguridad para Python](../python/security-overview-sql-server-python-services.md)
