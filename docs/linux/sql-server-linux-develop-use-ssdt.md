---
title: Desarrollar e implementar SQL Server las bases de datos de Linux | Documentos de Microsoft
description: 
author: erickangMSFT
ms.author: erickang
manager: jroth
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 9a639559de35573c7fb6dfdcc98c9d9680312659
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Usar Visual Studio para crear bases de datos de SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

SQL Server Data Tools (SSDT) se convierte Visual Studio en un entorno de administración (DLM) de ciclo de vida de desarrollo y base de datos eficaz para SQL Server en Linux. Puede desarrollar, compilar, probar y publicar la base de datos desde un proyecto controlado por código fuente, al igual que desarrollar el código de aplicación.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalar Visual Studio y las herramientas de datos SQL Server

1. Si ya no ha instalado Visual Studio en el equipo de Windows, [descargar e instalar Visual Studio]. Si no tiene una licencia de Visual Studio, edición de Visual Studio Community es un IDE libre, con características completas para estudiantes, los desarrolladores de código abierto e individuales.

2. Durante la instalación de Visual Studio, seleccione **personalizado** para el **elegir el tipo de instalación** opción. Haga clic en **Siguiente**.

3. Seleccione **Microsoft SQL Server Data Tools**, **Git para Windows**, y **extensión de GitHub para Visual Studio** desde la lista de selección de características.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continuar y completar la instalación de Visual Studio. Puede tardar unos minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Actualizar las herramientas de datos de SQL Server a la versión de SSDT 17,0 RC

SQL Server 2017 en Linux es compatible con SSDT versión 17,0 RC o posterior.

* [Descargue e instale SSDT 17,0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Crear un nuevo proyecto de base de datos de control de código fuente

1. Inicie Visual Studio.

2. Seleccione **Team Explorer** en el **vista** menú. 

3. Haga clic en **New** en **repositorio de Git Local** sección en la **conectar** página.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Haga clic en **Crear**. Una vez creado el repositorio de Git local, haga doble clic en **SSDTRepo**.

4. Haga clic en **New** en el **soluciones** sección. Seleccione **SQL Server** en **otros lenguajes** nodo en el **nuevo proyecto** cuadro de diálogo.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Escriba en **TutorialDB** para el nombre y haga clic en **Aceptar** para crear un nuevo proyecto de base de datos.

## <a name="create-a-new-table-in-the-database-project"></a>Cree una nueva tabla en el proyecto de base de datos

1. Seleccione **el Explorador de soluciones** en el **vista** menú.

2. Abra el proyecto de base de datos con el botón secundario en **TutorialDB** en el Explorador de soluciones.

3. Seleccione **tabla** en **agregar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Usando el Diseñador de tablas, agregar dos columnas, nombre `nvarchar(50)` y la ubicación `nvarchar(50)`, tal y como se muestra en la imagen. SSDT genera el `CREATE TABLE` script a medida que agregue las columnas en el diseñador.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Guardar el **Table1.sql** archivo.

## <a name="build-and-validate-the-database"></a>Generar y validar la base de datos

1. Abra el proyecto de base de datos en **TutorialDB** y seleccione **generar**. SSDT compila archivos de código fuente de SQL en el proyecto y crea un archivo de paquete (dacpac) de aplicación de capa de datos. Esto puede usarse para publicar una base de datos a la instancia de SQL Server 2017 en Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Compruebe el mensaje de confirmación de la compilación **salida** ventana de Visual Studio. 

## <a name="publish-the-database-to-sql-server-2017-instance-on-linux"></a>Publicar la base de datos en la instancia de SQL Server 2017 en Linux

1. Abra el proyecto de base de datos en **TutorialDB** y seleccione **publicar**.

2. Haga clic en **editar** para seleccionar la instancia de SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. En el cuadro de diálogo de conexión, escriba el nombre de host o dirección IP de la instancia de SQL Server en Linux, el nombre de usuario y la contraseña.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Haga clic en el **publicar** botón en el cuadro de diálogo de publicación.

5. Comprobar el estado de publicación en el **operaciones de Data Tools** ventana.

6. Haga clic en **vista Reulst** o **ver Script** para ver los detalles de la databsae publicar resultados en el servidor SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Ha creado una nueva base de datos en la instancia de SQL Server en Linux y conoce los conceptos básicos sobre el desarrollo de una base de datos con un proyecto de base de datos controlados por código fuente.

## <a name="next-steps"></a>Pasos siguientes

Si está familiarizado con T-SQL, vea [Tutorial: escribir instrucciones de Transact-SQL] y [referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el desarrollo de una base de datos con las herramientas de datos de SQL, vea [documentos de MSDN de SSDT]

[descargar e instalar Visual Studio]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[documentos de MSDN de SSDT]: https://msdn.microsoft.com/en-us/library/hh272686(v=vs.103).aspx
[Tutorial: escribir instrucciones de Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[referencia de Transact-SQL (motor de base de datos)]:https://msdn.microsoft.com/library/bb510741.aspx
