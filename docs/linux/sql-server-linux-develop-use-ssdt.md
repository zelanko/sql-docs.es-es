---
title: Desarrollar e implementar SQL Server las bases de datos para Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: sql-linux
ms.openlocfilehash: 2053e338bf14d11f25e6e12b3d6c5aee6b8e636e
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51033582"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Use Visual Studio para crear bases de datos de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) convierte a Visual Studio en un eficaz entorno de administración (DLM) del ciclo de vida de desarrollo y base de datos de SQL Server en Linux. Puede desarrollar, compilar, probar y publicar la base de datos desde un proyecto de control de código fuente, al igual que desarrollar el código de aplicación.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Instalar Visual Studio y SQL Server Data Tools

1. Si ya no instala Visual Studio en el equipo de Windows, [Descargue e instale Visual Studio]. Si no tiene una licencia de Visual Studio, Visual Studio Community edition es un IDE gratuito con características completas para estudiantes, desarrolladores individuales y de código abierto.

2. Durante la instalación de Visual Studio, seleccione **personalizado** para el **elegir el tipo de instalación** opción. Haga clic en **Siguiente**.

3. Seleccione **Microsoft SQL Server Data Tools**, **Git para Windows**, y **extensión de GitHub para Visual Studio** desde la lista de selección de características.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. Continuar y finalizar la instalación de Visual Studio. Puede tardar unos minutos.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>Actualizar SQL Server Data Tools a la versión RC de SSDT 17.0

SQL Server en Linux es compatible con SSDT 17.0 RC o posterior de la versión.

* [Descargar e instalar SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939).

## <a name="create-a-new-database-project-in-source-control"></a>Cree un nuevo proyecto de base de datos en el control de código fuente

1. Inicie Visual Studio.

2. Seleccione **Team Explorer** en el **vista** menú. 

3. Haga clic en **New** en **repositorio de Git Local** sección en la **Connect** página.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. Haga clic en **Crear**. Una vez creado el repositorio de Git local, haga doble clic en **SSDTRepo**.

4. Haga clic en **New** en el **soluciones** sección. Seleccione **SQL Server** en **otros lenguajes** nodo en el **nuevo proyecto** cuadro de diálogo.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. Escriba en **TutorialDB** para el nombre y haga clic en **Aceptar** para crear un nuevo proyecto de base de datos.

## <a name="create-a-new-table-in-the-database-project"></a>Cree una nueva tabla en el proyecto de base de datos

1. Seleccione **el Explorador de soluciones** en el **vista** menú.

2. Abra el menú de proyecto de base de datos con el botón secundario en **TutorialDB** en el Explorador de soluciones.

3. Seleccione **tabla** en **agregar**.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. Usando el Diseñador de tablas, agregue dos columnas, nombre `nvarchar(50)` y la ubicación `nvarchar(50)`, tal y como se muestra en la imagen. SSDT genera el `CREATE TABLE` script a medida que agrega las columnas en el diseñador.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. Guardar el **Table1.sql** archivo.

## <a name="build-and-validate-the-database"></a>Crear y validar la base de datos

1. Abra el menú de proyecto de base de datos en **TutorialDB** y seleccione **compilar**. SSDT .sql archivos de código fuente en el proyecto compila y compila un archivo de paquete (dacpac) de la aplicación de capa de datos. Esto puede usarse para publicar una base de datos en la instancia de SQL Server en Linux. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Compruebe el mensaje de éxito de la compilación **salida** ventana de Visual Studio. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Publicar la base de datos en la instancia de SQL Server en Linux

1. Abra el menú de proyecto de base de datos en **TutorialDB** y seleccione **publicar**.

2. Haga clic en **editar** para seleccionar la instancia de SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. En el cuadro de diálogo de conexión, escriba el nombre de host o dirección IP de la instancia de SQL Server en Linux, el nombre de usuario y contraseña.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. Haga clic en el **publicar** botón en el cuadro de diálogo Publicar.

5. Comprobar el estado de publicación en el **operaciones de Data Tools** ventana.

6. Haga clic en **vista Reulst** o **ver Script** para ver los detalles de la base de datos publicar resultados en SQL Server en Linux.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Ha creado una nueva base de datos en la instancia de SQL Server en Linux y conoce los aspectos básicos del desarrollo de una base de datos con un proyecto de base de datos controlados por código fuente.

## <a name="next-steps"></a>Pasos siguientes

Si no conoce T-SQL, consulte [Tutorial: Escribir instrucciones Transact-SQL] y [Referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el desarrollo de una base de datos con herramientas de datos de SQL, consulte [documentos de MSDN de SSDT]

[Descargue e instale Visual Studio]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[Documentos de MSDN de SSDT]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[Tutorial: Escribir instrucciones Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[Referencia de Transact-SQL (motor de base de datos)]:https://msdn.microsoft.com/library/bb510741.aspx
