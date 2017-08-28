---
title: Usar SSMS para administrar SQL Server en Linux | Documentos de Microsoft
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: b2fcf858-21c3-462a-8d49-50c85647d092
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 1f8fe782aa69f462366130418fce84a2654de3cf
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="use-sql-server-management-studio-on-windows-to-manage-sql-server-on-linux"></a>Usar SQL Server Management Studio en Windows para administrar SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tema se presentan [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/en-us/library/hh213248.aspx) y le guía a través de un par de tareas comunes. SSMS es una aplicación de Windows, así que usa SSMS cuando tiene una máquina de Windows que se puede conectar a una instancia remota de SQL Server en Linux.

[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/en-us/library/hh213248.aspx) forma parte de un conjunto de herramientas SQL que Microsoft ofrece gratuitamente para sus necesidades de desarrollo y administración. SSMS es un entorno integrado para tener acceso, configurar, administrar, administrar y desarrollar todos los componentes de SQL Server que se ejecutan de forma local o en la nube, en Linux, Windows o Docker en macOS y base de datos de SQL Azure y almacenamiento de datos de SQL Azure. SSMS combina un amplio grupo de herramientas gráficas con una serie de editores de script enriquecidos para proporcionar acceso a SQL Server a desarrolladores y administradores de todos los niveles.

SSMS ofrece un amplio conjunto de capacidades de administración y desarrollo para SQL Server, incluidas herramientas para:

- configurar, supervisar y administrar una o varias instancias de SQL Server
- implementar, supervisar y actualizar los componentes de capa de datos como bases de datos y almacenamientos de datos
- bases de datos de copia de seguridad y restauración
- compilar y ejecutar secuencias de comandos y consultas de T-SQL y ver resultados
- generar scripts de T-SQL para objetos de base de datos
- ver y editar datos en las bases de datos
- Diseñe visualmente consultas de T-SQL y objetos de base de datos, como vistas, tablas y procedimientos almacenados

Vea [Use SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx) para obtener más información.

## <a name="install-the-newest-version-of-sql-server-management-studio-ssms"></a>Instale la versión más reciente de SQL Server Management Studio (SSMS)

Al trabajar con SQL Server, debe utilizar siempre la versión más reciente de SQL Server Management Studio (SSMS). La versión más reciente de SSMS se actualiza continuamente y optimizado y funciona con SQL Server actualmente Linux de 2017. Para descargar e instalar la versión más reciente, consulte [descargar SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx). Para mantenerse al día, la versión más reciente de SSMS le avisa cuando hay una nueva versión disponible para su descarga. 

## <a name="before-you-begin"></a>Antes de empezar
- Vea [SSMS de uso en Windows para conectarse a SQL Server en Linux](sql-server-linux-develop-use-ssms.md) para saber cómo conectarse y consultar mediante SSMS
- Leer la [problemas conocidos](sql-server-linux-release-notes.md) para SQL Server de 2017 RC2 en Linux

## <a name="create-and-manage-databases"></a>Crear y administrar las bases de datos
Mientras está conectado a la *maestro* base de datos, puede crear bases de datos en el servidor y modificar o quitar bases de datos existentes. Los pasos siguientes describen cómo llevar a cabo varias tareas de administración de base de datos común a través de Management Studio. Para llevar a cabo estas tareas, asegúrese de que está conectado a la *maestro* base de datos con el inicio de sesión de la entidad de seguridad de nivel de servidor que creó al configurar SQL Server de 2017 RC2 en Linux.

### <a name="create-a-new-database"></a>Creación de una base de datos

1. Inicie SSMS y conéctese a su servidor en SQL Server de 2017 RC2 en Linux

2. En el Explorador de objetos, haga doble clic en el *bases de datos* carpeta y, a continuación, haga clic en * nueva base de datos... "

3. En el *nueva base de datos* cuadro de diálogo, escriba un nombre para la nueva base de datos y, a continuación, haga clic en *Aceptar*

La nueva base de datos se creó correctamente en el servidor. Si desea crear una nueva base de datos mediante T-SQL, vea [CREATE DATABASE (SQL Server Transact-SQL)](https://msdn.microsoft.com/en-us/library/ms176061.aspx).

### <a name="drop-a-database"></a>Quitar una base de datos

1. Inicie SSMS y conéctese a su servidor en SQL Server de 2017 RC2 en Linux

2. En el Explorador de objetos, expanda el *bases de datos* carpeta para ver una lista de la base de datos en el servidor.

3. En el Explorador de objetos, haga doble clic en la base de datos que se va a quitar y, a continuación, haga clic en *eliminar*

4. En el *Eliminar objeto* cuadro de diálogo, verificación *cerrar conexiones existentes* y, a continuación, haga clic en *Aceptar*

La base de datos se quita correctamente desde el servidor. Si desea quitar una base de datos mediante T-SQL, vea [DROP DATABASE (SQL Server Transact-SQL)](https://msdn.microsoft.com/en-us/library/ms178613.aspx).

## <a name="use-activity-monitor-to-see-information-about-sql-server-activity"></a>Utilice el Monitor de actividad para ver información acerca de la actividad de SQL Server

El [Monitor de actividad](https://msdn.microsoft.com/en-us/library/hh212951.aspx) herramienta está integrada en SQL Server Management Studio (SSMS) y muestra información acerca de los procesos de SQL Server y cómo estos procesos afectan a la instancia actual de SQL Server.

1. Inicie SSMS y conéctese a su servidor en SQL Server de 2017 RC2 en Linux

2. En el Explorador de objetos, haga clic en el *server* nodo y, a continuación, haga clic en *Monitor de actividad*

Monitor de actividad muestra pueden expandibles y contraer paneles con información acerca de lo siguiente:
- Información general
- Procesos
- Esperas de recursos
- E/S de archivos de datos
- Consultas costosas recientes
- Consultas costosas activas

Cuando se expande un panel, Monitor de actividad consulta la instancia para obtener información. Si el panel está contraído, cualquier actividad de consulta se detiene en ese panel. Puede expandir uno o varios paneles al mismo tiempo para ver diferentes tipos de actividad en la instancia.

## <a name="see-also"></a>Vea también
- [Usar SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/ms174173.aspx)
- [Exportar e importar una base de datos con SSMS](sql-server-linux-migrate-ssms.md)
- [Tutorial: SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/bb934498.aspx)
- [Tutorial: Escribir instrucciones Transact-SQL](https://msdn.microsoft.com/en-us/library/ms365303.aspx)
- [Supervisión de la actividad y rendimiento del servidor](https://msdn.microsoft.com/en-us/library/ms191511.aspx)

