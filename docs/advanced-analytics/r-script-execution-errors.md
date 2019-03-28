---
title: 'R scripting errores y solución de problemas: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2df4fa2fd9ef52fe5edbca9440f73f351553f1ed
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511532"
---
# <a name="r-scripting-errors-in-sql-server"></a>Errores de scripting de R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se documenta varios gerrors scriptin al ejecutar código R en SQL Server. La lista no es exhaustiva. Hay muchos paquetes y errores pueden variar entre las versiones del mismo paquete. Se recomienda registrar errores de script en el [foro de Machine Learning Server](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), que es compatible con los componentes utilizados en R Services (In-Database), Microsoft R Client y Microsoft R Server de aprendizaje automático.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>Se produce un error en la secuencia de comandos válida en T-SQL o en los procedimientos almacenados

Antes de ajustar el código de R en un procedimiento almacenado, es una buena idea para ejecutar el código de R en un IDE externo o en una de las herramientas de R como RGui y RTerm. Mediante estos métodos, puede probar y depurar el código mediante el uso de los mensajes de error detallados que se devuelven por R.

Sin embargo, en ocasiones, el código que funciona perfectamente en un IDE externo o la utilidad podría no se ejecute en un procedimiento almacenado o contexto de proceso en un servidor SQL Server. Si esto ocurre, hay una variedad de problemas para buscar antes de que se puede suponer que el paquete no funciona en SQL Server.

1. Compruebe si Launchpad se está ejecutando.

2. Revise los mensajes para ver si los datos de entrada o datos de salida contienen columnas con tipos de datos no compatible o incompatible. Por ejemplo, las consultas en una base de datos SQL a menudo devuelven ROWGUID, ambos de los cuales no son compatibles o GUID. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

3. Revise las páginas de ayuda para las funciones de R individuales determinar si se admiten todos los parámetros para el contexto de cálculo de SQL Server. Para obtener ayuda de ScaleR, use los comandos de ayuda en línea R o vea [referencia de paquete](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

Si funciona el runtime de R, pero el script devuelve errores, se recomienda que intente depurar el script en un entorno de desarrollo de R dedicado, como las herramientas de R para Visual Studio.

También se recomienda que revise y escribir un poco el script para corregir cualquier problema con los tipos de datos que pueden surgir al mover datos entre R y el motor de base de datos. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

Además, puede usar el paquete sqlrutils para incluir el script de R en un formato que sea más fácil uso como un procedimiento almacenado. Para obtener más información, vea:
* [sqlrutils package](r/ref-r-sqlrutils.md)
* [Crear un procedimiento almacenado mediante sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>Script devuelve resultados incoherentes

Scripts de R pueden devolver valores diferentes en un contexto de SQL Server, por varias razones:

- Conversión de tipos implícita se realiza automáticamente en algunos tipos de datos, los datos se pasan entre SQL Server y R. Para obtener más información, consulte [tipos de datos y las bibliotecas de R](r/r-libraries-and-data-types.md).

- Determinar si el valor de bits es un factor. Por ejemplo, a menudo hay diferencias en los resultados de las bibliotecas de punto flotante de 32 bits y 64 bits de las operaciones matemáticas.

- Determinar si los valores NaN se hayan producido en cualquier operación. Esto puede invalidar los resultados.

- Al tomar un recíproco de un número cerca de cero, se pueden amplificar pequeñas diferencias.

- Errores de redondeo acumulados pueden provocar tales como los valores que son inferiores a cero en lugar de cero.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>Autenticación implícita para la ejecución remota a través de ODBC

Si se conecta a la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] comandos del equipo para ejecutar R mediante el uso de la **RevoScaleR** funciones, podría obtener un error al usar llamadas ODBC que escriben datos en el servidor. Este error se produce cuando se utiliza la autenticación de Windows.

El motivo es que las cuentas de trabajo que se crean para R Services no tiene permiso para conectarse al servidor. Por lo tanto, no se puede ejecutar llamadas ODBC en su nombre. El problema no ocurre con los inicios de sesión SQL porque, con los inicios de sesión SQL, las credenciales se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, a continuación, a ODBC. Sin embargo, también es menos seguro que usar la autenticación de Windows mediante inicios de sesión SQL.

Para habilitar las credenciales de Windows que se pasará de forma segura desde un script que ha iniciado de forma remota, SQL Server debe emular las credenciales. Este proceso se denomina _autenticación implícita_. Para solucionar este problema, las cuentas de trabajo que se ejecutan scripts de R o Python en el equipo de SQL Server deben tener los permisos correctos.

1. Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] como administrador en la instancia en la que desea ejecutar código R.

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuario, si ha cambiado el valor predeterminado y los nombres de equipo y de instancia.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>Evitar borrar el área de trabajo mientras se ejecuta R en un contexto de cálculo SQL

Aunque es habitual borrar el área de trabajo cuando se trabaja en la consola de R, puede tener consecuencias no deseadas en una instancia de SQL de contexto de proceso.

`revoScriptConnection` es un objeto en el área de trabajo de R que contiene información sobre una sesión de R que se llama desde SQL Server. Sin embargo, si el código de R incluye un comando para borrar el área de trabajo (como `rm(list=ls())`), también se borrarán toda la información acerca de la sesión y otros objetos en el área de trabajo de R.

Como alternativa, evite borrar indiscriminadamente las variables y otros objetos mientras se ejecuta R en SQL Server. Puede eliminar variables específicas mediante la **quitar** función:

```R
remove('name1', 'name2', ...)
```

Si hay varias variables para eliminar, se recomienda que guarde los nombres de variables temporales a una lista y, a continuación, realizar las colecciones de elementos no utilizados periódicamente en la lista.



## <a name="next-steps"></a>Pasos siguientes

[Problemas conocidos y solución de problemas de Machine Learning Services](machine-learning-troubleshooting-faq.md)

[Recopilación de datos para la solución de problemas de aprendizaje automático](data-collection-ml-troubleshooting-process.md)

[Preguntas más frecuentes sobre actualización e instalación](r/upgrade-and-installation-faq-sql-server-r-services.md)

[Solucionar problemas de conexiones de motor de base de datos](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
