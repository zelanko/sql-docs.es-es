---
title: Instale y configure la base de datos de ejemplo AdventureWorks
description: Siga estas instrucciones para descargar e instalar bases de datos de ejemplo AdventureWorks con SQL Server Management StudioSQL Server Management Studio o en Azure SQL Database.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484584"
---
# <a name="adventureworks-installation-and-configuration"></a>Instalación y configuración de AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Enlaces de descarga de AdventureWorks e instrucciones de instalación. 

## <a name="prerequisites"></a>Prerrequisitos

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) o [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para la versión completa del ejemplo, use SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, utilice la versión de junio de 2016 o posterior.
 
## <a name="oltp-downloads"></a>Descargas de OLTP

Los enlaces directos a las versiones OLTP de AdventureWorks se pueden encontrar a continuación:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Descargas de Data Warehouse

Los enlaces directos a las versiones de Almacenamiento de datos de AdventureWorks se pueden encontrar a continuación:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>Guiones de creación
Los siguientes scripts se pueden utilizar para crear toda la base de datos AdventureWorks, independientemente de la versión. 

- [AdventureWorks OLTP Scripts Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW Scripts Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>Enlaces de GitHub

- [Todos los archivos AdventureWorks para SQL 2014 - 2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos los archivos AdventureWorks para SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos los archivos AdventureWorks para SQL 2008 y 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>Instalar en SQL Server

### <a name="restore-backup"></a>Restaurar copia de seguridad
Siga los pasos que se indican a continuación para restaurar una copia de seguridad de la base de datos mediante SQL Server Management StudioSQL Server Management Studio. 

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL ServerSQL Server de destino.
2. Haga clic con el botón derecho en el nodo **Bases de datos** y seleccione Restaurar base de **datos**.
3. Seleccione **Dispositivo** y haga clic en las elipses (**...**)
4. En el cuadro de diálogo **Seleccionar dispositivos**de copia de seguridad , haga clic en **Agregar**, vaya a la copia de seguridad de la base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **OK**.
5. Si es necesario, cambie la ubicación de destino de los archivos de datos y de registro en el panel **Archivos.** Tenga en cuenta que se recomienda colocar datos y archivos de registro en diferentes unidades.
6. Haga clic en **OK**. Esto iniciará la restauración de la base de datos. Una vez completada, tendrá la base de datos AdventureWorks instalada en la instancia de SQL Server.

Para obtener más información sobre cómo restaurar una base de datos de SQL Server, vea Restaurar una copia de seguridad de base de [datos mediante SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Adjuntar un archivo de datos
Siga los pasos que se indican a continuación para adjuntar el archivo de datos de la base de datos mediante SQL Server Management StudioSQL Server Management Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL ServerSQL Server de destino.
2. Haga clic con el botón derecho en el nodo **Bases de datos** y seleccione **Adjuntar**.
3. Seleccione **Agregar** y vaya al archivo . MDF que desea adjuntar. 
1. Seleccione el archivo y haga clic en **Aceptar**. 
    1. La base de datos seleccionada debe mostrarse en la ventana inferior. Si el archivo aparece como "no encontrado", seleccione los puntos suspensivos (**...**) junto al nombre del archivo y actualice la ruta de acceso a la ruta correcta. 
    1. Si solo tiene el archivo de datos (.mdf) y no el archivo de registro (.ldf), resalte el archivo .ldf en la ventana inferior y seleccione **Quitar**. Esto creará un nuevo archivo de registro. 
1. Seleccione **Aceptar** para adjuntar el archivo. Después de adjuntar el archivo, tendrá la base de datos AdventureWorks instalada en la instancia de SQL Server.  

Para obtener más información sobre cómo adjuntar archivos de base de datos, vea [Adjuntar una base](../relational-databases/databases/attach-a-database.md)de datos . 

## <a name="install-to-azure-sql-database"></a>Instalar en Azure SQL Database


Si aún no tiene un servidor SQL Server en Azure, vaya a [Azure Portal](https://portal.azure.com/) y cree una nueva base de datos SQL. En el proceso de creación de una base de datos, creará un servidor. Anote el servidor. Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en minutos.

1. Conéctese a Azure Portal.
1. Seleccione **Crear un recurso** en la parte superior izquierda del panel de navegación. 
1. Seleccione **Bases de datos** y, luego, **SQL Database**. 
1. Rellene la información solicitada.
1. En el campo **Seleccionar origen,** seleccione **Ejemplo (AdventureWorksLT)** para restaurar una copia de seguridad de la copia de seguridad más reciente de AdventureWorksLT.
1. Seleccione **Crear** para crear la nueva base de datos SQL, que es la copia restaurada de la base de datos AdventureWorksLT. 


## <a name="see-also"></a>Consulte también
[Tutoriales para SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Tutoriales para el motor de base de datos de SQL Server](../relational-databases/database-engine-tutorials.md)
