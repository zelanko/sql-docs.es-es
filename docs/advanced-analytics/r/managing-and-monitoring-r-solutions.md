---
title: Administrar e integrar las cargas de trabajo de machine learning en SQL Server | Microsoft Docs
description: Como un DBA de SQL Server, revise las tareas administrativas para la implementación de un subsistema de R y Python en una instancia del motor de base de datos de aprendizaje automático.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e24f9974c55d6d189f7d650902352393e3e62627
ms.sourcegitcommit: c2322c1a1dca33b47601eb06c4b2331b603829f1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2018
ms.locfileid: "50743210"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Administrar e integrar las cargas de trabajo de machine learning en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es para los administradores de base de datos de SQL Server que son responsables de implementar una infraestructura de ciencia de datos eficiente en un recurso de servidor que admiten varias cargas de trabajo. Rodea el espacio del problema administrativo relevante para la administración de R y código de Python de ejecución en SQL Server. 

## <a name="what-is-feature-integration"></a>¿Qué es la integración de características

Aprendizaje automático R y Python proporcionado por [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) como una extensión a una instancia del motor de base de datos. La integración es principalmente a través de la capa de seguridad y el lenguaje de definición de datos, resumida del siguiente modo:

+ Los procedimientos almacenados están equipados con la capacidad para aceptar R y Python de código como parámetros de entrada. Los desarrolladores y científicos de datos pueden utilizar un [procedimiento almacenado del sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) o crear un procedimiento personalizado que contiene su código.
+ Funciones de Transact-SQL (es decir, [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) que puede consumir un modelo de datos previamente entrenado. Esta funcionalidad está disponible a través de Transact-SQL. Por lo tanto, se puede llamar en un sistema concreto no tiene instaladas las extensiones de aprendizaje automático.
+ Inicios de sesión de base de datos existentes y los permisos basados en rol cubren las secuencias de comandos invocada por el usuario utilizando esos mismos datos. Como norma general, si los usuarios no pueden tener acceso a datos a través de una consulta, no puedan acceder a él a través de la secuencia de comandos o bien.

## <a name="feature-availability"></a>Disponibilidad de características

Integración de R y Python esté disponible a través de una sucesión de pasos. El primero es el programa de instalación, cuando se [incluir o agregar el **Machine Learning Services** ](../install/sql-machine-learning-services-windows-install.md) característica a una instancia del motor de base de datos. Como un paso posterior, debe habilitar los scripts externos en la instancia del motor de base de datos (está desactivada de forma predeterminada).

En este momento, solo los administradores de base de datos tendrán permisos completos para crear y ejecutar scripts externos, agregar o eliminar paquetes y creación procedimientos almacenados y otros objetos.

Todos los demás usuarios deben tener el permiso EXECUTE ANY EXTERNAL SCRIPT. Adicionales [permisos de base de datos estándar](../security/user-permission.md) determinar si los usuarios pueden crear objetos, ejecutar secuencias de comandos, consumir modelos entrenados y serializados y así sucesivamente. 

## <a name="resource-allocation"></a>Asignación de recursos

Procedimientos almacenados y consultas de T-SQL que invocan el procesamiento externo utilizan los recursos disponibles para el grupo de recursos predeterminado. Como parte de la configuración predeterminada, los procesos externos, como las sesiones de R y Python se permiten hasta un 20% del total de memoria en el sistema host. 

Si desea ajustar los recursos, puede modificar el grupo predeterminado, con un efecto correspondiente en cargas de trabajo de machine learning que se ejecutan en ese sistema.

Otra opción es crear un grupo de recursos externos personalizado para capturar las sesiones procedentes de programas específicos, hosts o actividades que se producen durante los intervalos de tiempo específico. Para obtener más información, consulte [regulación de recursos para modificar los niveles de recursos para la ejecución de R y Python](../administration/resource-governance.md) y [cómo crear un grupo de recursos](../administration/how-to-create-a-resource-pool.md) para obtener instrucciones paso a paso.

## <a name="isolation-and-containment"></a>Aislamiento y contención

La arquitectura de procesamiento está diseñada para aislar los scripts externos de procesamiento básico de motor. Scripts de R y Python que se ejecutan como procesos independientes, en cuentas de trabajo local. En el Administrador de tareas, puede supervisar los procesos de R y Python, que se ejecuta bajo una cuenta de usuario local con pocos privilegios, distinta de la cuenta de servicio de SQL Server. 

Ejecución de procesos de R y Python en las cuentas individuales con pocos privilegios tiene las siguientes ventajas:

+ Aísla los procesos del motor principal de las sesiones de R y Python que puede finalizar un proceso de R o Python sin afectar las operaciones de base de datos principal. 

+ Reduce los privilegios de los procesos en tiempo de ejecución de script externo en el equipo host.

Las cuentas con privilegios mínimos se creó durante la instalación y se colocan en un Windows *grupo de cuentas de usuario* llamado **SQLRUserGroup**. De forma predeterminada, este grupo tiene permiso para usar los archivos ejecutables, bibliotecas y los conjuntos de datos integrados en la carpeta de programas para R y Python en SQL Server. 

Como un DBA, puede usar seguridad de datos de SQL Server para especificar quién tiene permiso para ejecutar scripts y que los datos utilizados en los trabajos se administran en los mismos roles de seguridad que controlan el acceso a través de consultas de Transact-SQL. Como administrador del sistema, puede denegar explícitamente **SQLRUserGroup** acceso a datos confidenciales en el servidor local mediante la creación de ACL.

>[!NOTE]
> De forma predeterminada, el **SQLRUserGroup** no tiene permisos o un inicio de sesión de SQL Server. Si las cuentas de trabajo requiere un inicio de sesión para el acceso a datos, debe crearla usted mismo. Es un escenario que requiere la creación de un inicio de sesión específicamente admitir las solicitudes de una secuencia de comandos en ejecución para las operaciones en la instancia del motor de base de datos, o datos cuando la identidad del usuario es un usuario de Windows y la cadena de conexión especifica un usuario de confianza. Para obtener más información, consulte [agregar SQLRUserGroup como un usuario de base de datos](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

## <a name="disable-script-execution"></a>Deshabilitar la ejecución del script

En el caso de secuencias de comandos descontroladas, puede deshabilitar toda la ejecución del script, invertir los pasos que se llevan a cabo anteriormente para habilitar la ejecución de scripts externos en primer lugar.

1. En SQL Server Management Studio u otra herramienta de consulta, ejecute este comando para establecer `external scripts enabled` en 0 o FALSE.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Reinicie el servicio de motor de base de datos.

Una vez que se resuelve el problema, recuerde volver a habilitar la ejecución del script en la instancia si desea reanudar R y compatible con scripting de Python en la instancia del motor de base de datos. Para obtener más información, consulte [habilitar la ejecución del script](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>Extender funcionalidad

Ciencia de datos a menudo presenta nuevos requisitos para la implementación de paquetes y administración. Para un científico de datos, es una práctica común para aprovechar los paquetes de código abierto y de terceros en soluciones personalizadas. Algunos de esos paquetes tendrá dependencias de otros paquetes, en cuyo caso es posible que deba evaluar e instalar varios paquetes para alcanzar su objetivo.

Como un DBA responsable de un recurso de servidor, la implementación de paquetes de R y Python arbitrarios en un servidor de producción representa un reto desconocido. Antes de agregar los paquetes, debe evaluar si la funcionalidad proporcionada por el paquete externo es realmente necesaria, con ningún equivalente integrado [lenguaje R](r-libraries-and-data-types.md) y [bibliotecas de Python](../python/python-libraries-and-data-types.md) instalado programa de instalación de SQL Server. 

Como alternativa a la instalación del paquete de servidor, un científico de datos podría ser capaz de [compilar y ejecutar soluciones en una estación de trabajo externo](../r/set-up-a-data-science-client.md), recuperación de datos de SQL Server, pero con todos los análisis desde el sistema local en la estación de trabajo en lugar de en el mismo servidor. 

Si posteriormente decide que las funciones de biblioteca externa son necesarias y no suponen un riesgo para las operaciones del servidor o los datos como un todo, puede elegir desde varias metodologías para agregar paquetes. En la mayoría de los casos, se necesitan derechos de administrador para agregar paquetes a SQL Server. Para obtener más información, consulte [paquetes de instalación de Python en SQL Server](../python/install-additional-python-packages-on-sql-server.md) y [instalar paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> Para paquetes de R, derechos de administrador del servidor no son necesarios específicamente para la instalación del paquete si usa los métodos alternativos. Consulte [instalar paquetes de R en SQL Server](install-additional-r-packages-on-sql-server.md) para obtener más información.

## <a name="monitoring-script-execution"></a>Supervisión de la ejecución del script

Scripts de R y Python que se ejecutan en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] iniciados por el [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interfaz. Sin embargo, Launchpad no es un recurso controlado ni supervisado por separado, ya que es un servicio seguro proporcionado por Microsoft que administra los recursos adecuadamente.

Los scripts externos que se ejecutan en el servicio Launchpad se administran mediante el [objeto de trabajo de Windows](/windows/desktop/ProcThread/job-objects). Un objeto de trabajo permite administrar grupos de procesos como una unidad. Cada objeto de trabajo es jerárquico y controla los atributos de todos los procesos asociados con él. Las operaciones realizadas en un objeto de trabajo afectan a todos los procesos asociados con el objeto de trabajo.

Por tanto, si es necesario finalizar un trabajo asociado a un objeto, tenga en cuenta que todos los procesos relacionados también se finalizarán. Si se está ejecutando un script de R asignado a un objeto de trabajo de Windows y ese script ejecuta un trabajo de ODBC relacionado que debe finalizarse, también se finalizará el proceso de script de R primario.

Si inicia un script externo que usa el procesamiento paralelo, un único objeto de trabajo de Windows administra todos los procesos secundarios en paralelo.

Para determinar si un proceso se ejecuta en un trabajo, use la función `IsProcessInJob`.

## <a name="next-steps"></a>Pasos siguientes

+ Revise los conceptos y componentes de la [arquitectura de extensibilidad](../concepts/extensibility-framework.md) y [seguridad](../concepts/security.md) para obtener más información.

+ Como parte de la instalación de características, posiblemente ya esté familiarizado con los usuarios finales, control de acceso a datos, pero si no, consulte [conceder permisos de usuario para el aprendizaje automático de SQL Server](../security/user-permission.md) para obtener más información. 

+ Obtenga información sobre cómo ajustar los recursos del sistema para las cargas de trabajo de aprendizaje de automático de cálculo intensivo. Para obtener más información, consulte [cómo crear un grupo de recursos](../administration/how-to-create-a-resource-pool.md).
