---
title: Administrar e integrar cargas de trabajo de aprendizaje automático
description: Como SQL Server DBA, revise las tareas administrativas para implementar un subsistema de machine learning R y Python en una instancia del motor de base de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2677b48daf253a85f2b74078bdad7de65e37d572
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715051"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Administrar e integrar cargas de trabajo de aprendizaje automático en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo está destinado a los administradores de SQL Server Database responsables de implementar una infraestructura de ciencia de datos eficaz en un recurso de servidor que admita varias cargas de trabajo. Trama el espacio de problemas administrativo relacionado con la administración de la ejecución de código de R y Python en SQL Server. 

## <a name="what-is-feature-integration"></a>Qué es la integración de características

El aprendizaje automático de R y Python lo proporciona [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) como una extensión a una instancia del motor de base de datos. La integración se realiza principalmente a través de la capa de seguridad y el lenguaje de definición de datos, resumido de la siguiente manera:

+ Los procedimientos almacenados están equipados con la capacidad de aceptar código de R y Python como parámetros de entrada. Los desarrolladores y científicos de datos pueden usar un [procedimiento almacenado del sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) o crear un procedimiento personalizado que ajuste su código.
+ Funciones de T-SQL (es decir, [predicción](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) que pueden consumir un modelo de datos entrenado previamente. Esta funcionalidad está disponible a través de T-SQL. Como tal, puede llamarse en un sistema que no tenga instaladas de forma específica las extensiones de aprendizaje automático.
+ Los inicios de sesión de base de datos existentes y los permisos basados en roles cubren los scripts invocados por el usuario que usan esos mismos datos. Como norma general, si los usuarios no pueden tener acceso a los datos a través de una consulta, no podrán tener acceso a ellos a través del script.

## <a name="feature-availability"></a>Disponibilidad de características

La integración de R y Python está disponible a través de una serie de pasos. El primero es el programa de instalación, cuando se [incluye o agrega la característica **Machine Learning Services** ](../install/sql-machine-learning-services-windows-install.md) a una instancia del motor de base de datos. Como paso posterior, debe habilitar el scripting externo en la instancia del motor de base de datos (está desactivada de forma predeterminada).

En este momento, solo los administradores de bases de datos tienen permiso total para crear y ejecutar scripts externos, agregar o eliminar paquetes, y crear procedimientos almacenados y otros objetos.

A todos los demás usuarios se les debe conceder el permiso ejecutar cualquier SCRIPT externo. [Los permisos de base de datos estándar](../security/user-permission.md) adicionales determinan si los usuarios pueden crear objetos, ejecutar scripts, consumir modelos en serie y entrenados, etc. 

## <a name="resource-allocation"></a>Asignación de recursos

Los procedimientos almacenados y las consultas de T-SQL que invocan el procesamiento externo usan los recursos disponibles para el grupo de recursos predeterminado. Como parte de la configuración predeterminada, los procesos externos como las sesiones de R y Python pueden tener hasta un 20% de la memoria total en el sistema host. 

Si desea reajustar el reabastecimiento, puede modificar el grupo predeterminado, con el efecto correspondiente en las cargas de trabajo de machine learning que se ejecutan en ese sistema.

Otra opción consiste en crear un grupo de recursos externos personalizado para capturar las sesiones procedentes de programas, hosts o actividad específicos que se producen durante intervalos de tiempo específicos. Para obtener más información, consulte [regulación de recursos para modificar los niveles de recursos para la ejecución de R y Python](../administration/resource-governance.md) y [Cómo crear un grupo de recursos](../administration/how-to-create-a-resource-pool.md) para obtener instrucciones paso a paso.

## <a name="isolation-and-containment"></a>Aislamiento y contención

La arquitectura de procesamiento está diseñada para aislar los scripts externos del procesamiento del motor principal. Los scripts de R y Python se ejecutan como procesos independientes, en cuentas de trabajo local. En el administrador de tareas, puede supervisar los procesos de R y Python, que se ejecutan con una cuenta de usuario local con pocos privilegios, distinta de la cuenta de servicio de SQL Server. 

La ejecución de procesos de R y Python en cuentas individuales con pocos privilegios tiene las siguientes ventajas:

+ Aísla los procesos principales del motor de las sesiones de R y Python puede finalizar un proceso de R o Python sin que ello afecte a las operaciones de base de datos principales. 

+ Reduce los privilegios de los procesos en tiempo de ejecución de scripts externos en el equipo host.

Las cuentas con privilegios mínimos se crean durante la instalación y se colocan en un *grupo de cuentas de usuario* de Windows llamado **SQLRUserGroup**. De forma predeterminada, este grupo tiene permiso para usar ejecutables, bibliotecas y conjuntos de archivos integrados en la carpeta de programas para R y Python en SQL Server. 

Como DBA, puede usar SQL Server seguridad de datos para especificar quién tiene permiso para ejecutar scripts y que los datos que se usan en los trabajos se administran con los mismos roles de seguridad que controlan el acceso a través de consultas de T-SQL. Como administrador del sistema, puede denegar explícitamente el acceso **SQLRUserGroup** a los datos confidenciales en el servidor local mediante la creación de ACL.

>[!NOTE]
> De forma predeterminada, **SQLRUserGroup** no tiene un inicio de sesión o permisos en SQL Server mismo. Si las cuentas de trabajo requieren un inicio de sesión para el acceso a datos, debe crearlo usted mismo. Un escenario que llama específicamente a para la creación de un inicio de sesión es admitir solicitudes de un script en ejecución, para los datos o las operaciones en la instancia del motor de base de datos, cuando la identidad del usuario es un usuario de Windows y la cadena de conexión especifica un usuario de confianza. Para obtener más información, vea [Agregar SQLRUserGroup como un usuario de base de datos](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="disable-script-execution"></a>Deshabilitar la ejecución de scripts

En el caso de los scripts descontrolados, puede deshabilitar toda la ejecución del script e invertir los pasos realizados previamente para habilitar la ejecución de scripts externos en primer lugar.

1. En SQL Server Management Studio u otra herramienta de consulta, ejecute este comando para `external scripts enabled` establecer en 0 o false.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Reinicie el servicio motor de base de datos.

Una vez resuelto el problema, recuerde volver a habilitar la ejecución de scripts en la instancia si desea reanudar la compatibilidad con scripting de R y Python en la instancia del motor de base de datos. Para obtener más información, consulte [Habilitar la ejecución](../install/sql-machine-learning-services-windows-install.md#enable-script-execution) de scripts.

## <a name="extend-functionality"></a>Extender la funcionalidad

La ciencia de datos a menudo presenta nuevos requisitos para la implementación y administración de paquetes. Para un científico de datos, es una práctica común aprovechar los paquetes de código abierto y de terceros en las soluciones personalizadas. Algunos de esos paquetes tendrán dependencias en otros paquetes, en cuyo caso es posible que tenga que evaluar e instalar varios paquetes para alcanzar su objetivo.

Como DBA responsable de un recurso de servidor, la implementación de paquetes de R y Python arbitrarios en un servidor de producción representa un desafío desconocido. Antes de agregar paquetes, debe evaluar si la funcionalidad proporcionada por el paquete externo es realmente necesaria, sin equivalente en el [lenguaje R](r-libraries-and-data-types.md) integrado y en las [bibliotecas de Python](../python/python-libraries-and-data-types.md) instaladas por SQL Server el programa de instalación. 

Como alternativa a la instalación de paquetes de servidor, un científico de datos podría [compilar y ejecutar soluciones en una estación de trabajo externa](../r/set-up-a-data-science-client.md), recuperar datos de SQL Server, pero con todo el análisis realizado localmente en la estación de trabajo en lugar de en el servidor propio. 

Si posteriormente determina que las funciones de biblioteca externa son necesarias y no supone un riesgo para las operaciones del servidor o los datos en conjunto, puede elegir entre varias metodologías para agregar paquetes. En la mayoría de los casos, se requieren derechos de administrador para agregar paquetes a SQL Server. Para obtener más información, consulte [instalación de paquetes de Python en SQL Server](../python/install-additional-python-packages-on-sql-server.md) e [instalación de paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> En el caso de los paquetes de R, los derechos de administrador del servidor no son necesarios específicamente para la instalación de paquetes si se usan métodos alternativos. Consulte [instalación de paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md) para obtener más información.

## <a name="monitoring-script-execution"></a>Supervisión de la ejecución del script

Los scripts de R y Python [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que se ejecutan [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] en se inician mediante la interfaz. Sin embargo, el Launchpad no se rige ni supervisa por separado, ya que es un servicio seguro proporcionado por Microsoft que administra los recursos de manera adecuada.

Los scripts externos que se ejecutan en el servicio Launchpad se administran mediante el [objeto de trabajo de Windows](/windows/desktop/ProcThread/job-objects). Un objeto de trabajo permite administrar grupos de procesos como una unidad. Cada objeto de trabajo es jerárquico y controla los atributos de todos los procesos asociados con él. Las operaciones realizadas en un objeto de trabajo afectan a todos los procesos asociados con el objeto de trabajo.

Por tanto, si es necesario finalizar un trabajo asociado a un objeto, tenga en cuenta que todos los procesos relacionados también se finalizarán. Si se está ejecutando un script de R asignado a un objeto de trabajo de Windows y ese script ejecuta un trabajo de ODBC relacionado que debe finalizarse, también se finalizará el proceso de script de R primario.

Si inicia un script externo que usa el procesamiento en paralelo, un único objeto de trabajo de Windows administra todos los procesos paralelos secundarios.

Para determinar si un proceso se ejecuta en un trabajo, use la función `IsProcessInJob`.

## <a name="next-steps"></a>Pasos siguientes

+ Revise los conceptos y los componentes de la [arquitectura](../concepts/extensibility-framework.md) de extensibilidad y la [seguridad](../concepts/security.md) para obtener más información.

+ Como parte de la instalación de características, es posible que ya esté familiarizado con el control de acceso a datos de usuario final, pero si no es así, consulte [concesión de permisos de usuario a SQL Server machine learning](../security/user-permission.md) para obtener más información. 

+ Obtenga información sobre cómo ajustar los recursos del sistema para cargas de trabajo de aprendizaje automático de proceso intensivo. Para obtener más información, vea [Cómo crear un grupo de recursos](../administration/how-to-create-a-resource-pool.md).
