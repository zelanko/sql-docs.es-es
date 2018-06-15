---
title: Usar SSMS para administrar SQL Server en Linux | Documentos de Microsoft
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/21/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: sql-linux
ms.openlocfilehash: 2b6293e7c0d80eb1ebe02d6cd03f17626d793c05
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34455333"
---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Usar SQL Server Management Studio en Windows para administrar SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo se detallan [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) y le guía a través de un par de tareas comunes. SSMS es una aplicación de Windows, así que usa SSMS cuando tiene una máquina de Windows que se puede conectar a una instancia remota de SQL Server en Linux.

> [!TIP]
> Si no tiene un equipo de Windows para ejecutar SSMS en, considere la posibilidad de la nueva [Studio de operaciones de SQL Server](../sql-operations-studio/index.md). Se proporciona una herramienta gráfica para administrar SQL Server y se ejecuta en Linux y Windows.

[SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md) forma parte de un conjunto de herramientas SQL que Microsoft ofrece gratuitamente para sus necesidades de desarrollo y administración. SSMS es un entorno integrado para tener acceso, configurar, administrar, administrar y desarrollar todos los componentes de SQL Server. Se puede conectar a SQL Server que se ejecutan en cualquier plataforma tanto de forma local, en contenedores de Docker y en la nube. También se conecta a la base de datos de SQL Azure y almacenamiento de datos de SQL Azure. SSMS combina un amplio grupo de herramientas gráficas con una serie de editores de script enriquecidos para proporcionar acceso a SQL Server a desarrolladores y administradores de todos los niveles.

SSMS ofrece un amplio conjunto de capacidades de administración y desarrollo para SQL Server, incluidas herramientas para:

- Configurar, supervisar y administrar una o varias instancias de SQL Server
- implementar, supervisar y actualizar los componentes de capa de datos como bases de datos y almacenamientos de datos
- bases de datos de copia de seguridad y restauración
- compilar y ejecutar secuencias de comandos y consultas de T-SQL y ver resultados
- generar scripts de T-SQL para objetos de base de datos
- ver y editar datos en las bases de datos
- Diseñe visualmente consultas de T-SQL y objetos de base de datos, como vistas, tablas y procedimientos almacenados

Vea [¿qué es SSMS?](../ssms/sql-server-management-studio-ssms.md) para obtener más información en SSMS.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Instale la versión más reciente de SQL Server Management Studio (SSMS)

Al trabajar con SQL Server, debe utilizar siempre la versión más reciente de SQL Server Management Studio (SSMS). La versión más reciente de SSMS se actualiza continuamente y optimizado y funciona con SQL Server actualmente Linux de 2017. Para descargar e instalar la versión más reciente, consulte [descargar SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para mantenerse al día, la versión más reciente de SSMS le avisa cuando hay una nueva versión disponible para su descarga.

> [!NOTE]
> Antes de usar SSMS para administrar Linux, revise la [problemas conocidos](sql-server-linux-release-notes.md) de SSMS en Linux.

## <a name="connect-to-sql-server-on-linux"></a>Conectarse a SQL Server en Linux

Use los siguientes pasos básicos para conectarse:

1. Inicie SSMS escribiendo **Microsoft SQL Server Management Studio** en las ventanas del cuadro de búsqueda y, a continuación, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png)

1. En el **conectar al servidor** ventana, escriba la información siguiente (si SSMS ya se está ejecutando, haga clic en **conectar > motor de base de datos** para abrir el **conectar al servidor** ventana):

   | Configuración | Description |
   |-----|-----|
   | **Tipo de servidor** | El valor predeterminado es el motor de base de datos; No cambie este valor. |
   | **Nombre del servidor** | Escriba el nombre de la máquina de SQL Server de Linux de destino o su dirección IP. |
   | **Autenticación** | Para SQL Server de 2017 en Linux, use **autenticación de SQL Server**. |
   | **Inicio de sesión** | Escriba el nombre de un usuario con acceso a una base de datos en el servidor (por ejemplo, el valor predeterminado **SA** cuenta creada durante la instalación). |
   | **Contraseña** | Escriba la contraseña para el usuario especificado (para el **SA** cuenta, creó esto durante la instalación). |

    ![SQL Server Management Studio: Conectarse al servidor de base de datos SQL](./media/sql-server-linux-manage-ssms/connect.png)

1. Haga clic en **Conectar**.

    > [!TIP]
    > Si recibe un error de conexión, intente primero diagnosticar el problema a partir del mensaje de error. Luego revise las [recomendaciones para solucionar problemas de conexión](sql-server-linux-troubleshooting-guide.md#connection).
 
1. Después de conectarse correctamente a SQL Server, **Explorador de objetos** se abre y ahora puede acceder a la base de datos para realizar tareas administrativas o consultar los datos.

## <a name="run-transact-sql-queries"></a>Ejecutar consultas Transact-SQL

Después de conectarse al servidor, puede conectarse a una base de datos y ejecutar consultas Transact-SQL. Consultas de Transact-SQL puede utilizarse para casi cualquier tarea de la base de datos.

1. En **Explorador de objetos**, vaya a la base de datos de destino en el servidor. Por ejemplo, expanda **bases de datos de sistema** para trabajar con la **maestro** base de datos.

1. Haga clic en la base de datos y, a continuación, seleccione **nueva consulta**.

1. En la ventana de consulta, escribir una consulta de Transact-SQL para seleccionar devuelven los nombres de todas las bases de datos en el servidor.

   ```sql
   SELECT [Name]
   FROM sys.Databases
   ```

   Si está familiarizado con la escritura de consultas, vea [escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Haga clic en el **Execute** botón para ejecutar la consulta y ver los resultados.

   ![Correcto. Conectarse al servidor de base de datos SQL: SQL Server Management Studio](./media/sql-server-linux-manage-ssms/execute-query.png)

Aunque es posible realizar casi cualquier tarea de administración con consultas Transact-SQL, SSMS es una herramienta gráfica que hace que sea más fácil administrar SQL Server. Las secciones siguientes proporcionan algunos ejemplos del uso de la interfaz gráfica de usuario.

## <a name="create-and-manage-databases"></a>Crear y administrar las bases de datos

Mientras está conectado a la *maestro* base de datos, puede crear bases de datos en el servidor y modificar o quitar bases de datos existentes. Los pasos siguientes describen cómo llevar a cabo varias tareas de administración de base de datos común a través de Management Studio. Para llevar a cabo estas tareas, asegúrese de que está conectado a la *maestro* base de datos con el inicio de sesión de la entidad de seguridad de nivel de servidor que creó al configurar SQL Server 2017 en Linux.

### <a name="create-a-new-database"></a>Creación de una base de datos

1. Inicie SSMS y conéctese a su servidor en SQL Server 2017 en Linux

2. En el Explorador de objetos, haga doble clic en el *bases de datos* carpeta y, a continuación, haga clic en * nueva base de datos... "

3. En el *nueva base de datos* cuadro de diálogo, escriba un nombre para la nueva base de datos y, a continuación, haga clic en *Aceptar*

La nueva base de datos se creó correctamente en el servidor. Si desea crear una nueva base de datos mediante T-SQL, vea [CREATE DATABASE (SQL Server Transact-SQL)](../t-sql/statements/create-database-sql-server-transact-sql.md).

### <a name="drop-a-database"></a>Quitar una base de datos

1. Inicie SSMS y conéctese a su servidor en SQL Server 2017 en Linux

2. En el Explorador de objetos, expanda el *bases de datos* carpeta para ver una lista de la base de datos en el servidor.

3. En el Explorador de objetos, haga doble clic en la base de datos que se va a quitar y, a continuación, haga clic en *eliminar*

4. En el *Eliminar objeto* cuadro de diálogo, verificación *cerrar conexiones existentes* y, a continuación, haga clic en *Aceptar*

La base de datos se quita correctamente desde el servidor. Si desea quitar una base de datos mediante T-SQL, vea [DROP DATABASE (SQL Server Transact-SQL)](../t-sql/statements/drop-database-transact-sql.md).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Utilice el Monitor de actividad para ver información acerca de la actividad de SQL Server

El [Monitor de actividad](../relational-databases/performance-monitor/activity-monitor.md) herramienta está integrada en SQL Server Management Studio (SSMS) y muestra información acerca de los procesos de SQL Server y cómo estos procesos afectan a la instancia actual de SQL Server.

1. Inicie SSMS y conéctese a su servidor en SQL Server 2017 en Linux

1. En el Explorador de objetos, haga clic en el *server* nodo y, a continuación, haga clic en *Monitor de actividad*

Monitor de actividad muestra pueden expandibles y contraer paneles con la siguiente información:

- Información general
- Procesos
- Esperas de recursos
- E/S de archivos de datos
- Consultas costosas recientes
- Consultas costosas activas

Cuando se expande un panel, Monitor de actividad consulta la instancia para obtener información. Si el panel está contraído, cualquier actividad de consulta se detiene en ese panel. Puede expandir uno o varios paneles al mismo tiempo para ver diferentes tipos de actividad en la instancia.

## <a name="see-also"></a>Vea también
- [¿Qué es SSMS?](../ssms/sql-server-management-studio-ssms.md)
- [Exportar e importar una base de datos con SSMS](sql-server-linux-migrate-ssms.md)
- [Tutorial: SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)
- [Tutorial: Escribir instrucciones Transact-SQL](../t-sql/tutorial-writing-transact-sql-statements.md)
- [Supervisión de la actividad y rendimiento del servidor](../relational-databases/performance/server-performance-and-activity-monitoring.md)
