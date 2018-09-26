---
title: Exportar e importar una base de datos en Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: sql-linux
ms.openlocfilehash: 36e18344efe0e3e329d4cb2672b51f23f0900128
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713187"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Exportar e importar una base de datos en Linux con SSMS o SqlPackage.exe en Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) y [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) para exportar e importar una base de datos en SQL Server en Linux. SSMS y SqlPackage.exe son las aplicaciones de Windows, así que use esta técnica cuando tenga una máquina de Windows que se puede conectar a una instancia remota de SQL Server en Linux.

Siempre debe instalar y usar la versión más reciente de SQL Server Management Studio (SSMS) como se describe en [utilizar SSMS en Windows para conectarse a SQL Server en Linux](sql-server-linux-manage-ssms.md)

> [!NOTE]
> Si va a migrar una base de datos de una instancia de SQL Server a otro, la recomendación es usar [copias de seguridad y restauración](sql-server-linux-migrate-restore-database.md).

## <a name="export-a-database-with-ssms"></a>Exportar una base de datos con SSMS

1. Inicie SSMS escribiendo **Microsoft SQL Server Management Studio** cuadro de búsqueda en el Windows y, a continuación, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conéctese a la base de datos de origen en el Explorador de objetos. La base de datos de origen puede ser en Microsoft SQL Server que se ejecutan en local o en la nube, en Linux, Windows o Docker y Azure SQL Database o Azure SQL Data Warehouse.

3. Haga clic en la base de datos de origen en el Explorador de objetos, seleccione **tareas**y haga clic en **Exportar aplicación de capa de datos...**

4. En el Asistente para exportación, haga clic en **siguiente**y, a continuación, en el **configuración** pestaña, configure la exportación para guardar el archivo BACPAC en una ubicación de disco local o en un blob de Azure.

5. De forma predeterminada, se exportan todos los objetos de la base de datos. Haga clic en el **ficha Opciones avanzadas** y elegir los objetos de base de datos que desea exportar.

6. Haga clic en **Siguiente** y, a continuación, en **Finalizar**.

El *. Archivo BACPAC se creó correctamente en la ubicación que elija y está listo para importarlo en una base de datos de destino.

## <a name="import-a-database-with-ssms"></a>Importar una base de datos con SSMS

1. Inicie SSMS escribiendo **Microsoft SQL Server Management Studio** cuadro de búsqueda en el Windows y, a continuación, haga clic en la aplicación de escritorio.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. Conéctese al servidor de destino en el Explorador de objetos. El servidor de destino puede ser Microsoft SQL Server que se ejecutan en local o en la nube, en Linux, Windows o Docker y Azure SQL Database o Azure SQL Data Warehouse.

3. Haga clic en el **bases de datos** carpeta en el Explorador de objetos y haga clic en **importar aplicación de capa de datos...**

4. Para crear la base de datos en el servidor de destino, especifique un archivo BACPAC desde el disco local o seleccione la cuenta de almacenamiento de Azure y el contenedor al que se cargó el archivo BACPAC.

5. Proporcione el nombre de base de datos nueva para la base de datos. Si va a importar una base de datos en Azure SQL Database, establezca la edición de Microsoft Azure SQL Database (nivel de servicio), tamaño máximo de la base de datos y el objetivo de servicio (nivel de rendimiento).

6. Haga clic en **siguiente** y, a continuación, haga clic en **finalizar** para importar el archivo BACPAC en una base de datos en el servidor de destino.

El *. Se importa el archivo BACPAC para crear una nueva base de datos en el servidor de destino especificado.

## <a id="sqlpackage"></a> Opción de línea de comandos SqlPackage

También es posible utilizar la herramienta de línea de comandos de SQL Server Data Tools (SSDT), [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx), para exportar e importar archivos BACPAC.

El siguiente comando de ejemplo exporta un archivo BACPAC:

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

Use el siguiente comando para importar datos de usuario y el esquema de base de datos de una. Archivo BACPAC:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>Vea también
Para obtener más información sobre cómo usar SSMS, consulte [usar SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx). Para obtener más información sobre SqlPackage.exe, consulte el [documentación de referencia de SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx).
