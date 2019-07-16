---
title: Instalar y configurar la base de datos de ejemplo de AdventureWorks - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99cdd6fdf5db075cc8fd46b738f468fd5d9a028d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894926"
---
# <a name="adventureworks-installation-and-configuration"></a>Configuración e instalación de AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks descargar vínculos e instrucciones de instalación. 

## <a name="prerequisites"></a>Requisitos previos

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) o [base de datos SQL Azure](https://azure.microsoft.com/services/sql-database/). Para obtener la versión completa del ejemplo, utilice SQL Server Evaluation, Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, use la versión de junio de 2016 o posterior.
 
## <a name="github-links"></a>Vínculos de Github

- [Todos los archivos de AdventureWorks para SQL 2014 2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos los archivos de AdventureWorks de SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos los archivos de AdventureWorks para SQL 2008 y 2008 R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>Descargas OLTP

A continuación, se pueden encontrar vínculos directos a las versiones OLTP de AdventureWorks:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Descargas de almacén de datos

A continuación, se pueden encontrar vínculos directos a las versiones de almacén de datos de AdventureWorks:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>Scripts de creación
Los siguientes scripts puede usarse para crear la base de datos completo de AdventureWorks, con independencia de la versión. 

- [Zip de Scripts de AdventureWorks OLTP](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [Zip de Scripts de AdventureWorks DW](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>Instalar SQL Server

### <a name="restore-backup"></a>Restaurar copia de seguridad
Siga los pasos siguientes para restaurar una copia de seguridad de la base de datos con SQL Server Management Studio. 

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga doble clic en el **bases de datos** nodo y seleccione **Restore Database**.
3. Seleccione **dispositivo** y haga clic en el botón de puntos suspensivos ( **...** )
4. En el cuadro de diálogo **seleccionar dispositivos de copia de seguridad**, haga clic en **agregar**, vaya a la copia de seguridad de base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **Aceptar**.
5. Si es necesario, cambie la ubicación de destino para los datos y archivos de registro, en el **archivos** panel. Tenga en cuenta que es una práctica recomendada para colocar los datos y archivos de registro en unidades distintas.
6. Haga clic en **Aceptar**. Esto iniciará la restauración de base de datos. Una vez haya terminado, tendrá la base de datos de AdventureWorks instalada en su instancia de SQL Server.

Para obtener más información acerca de cómo restaurar una base de datos de SQL Server, vea [restaurar una copia de seguridad de base de datos con SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Adjuntar un archivo de datos
Siga los pasos siguientes para adjuntar el archivo de datos para la base de datos con SQL Server Management Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga doble clic en el **bases de datos** nodo y seleccione **adjuntar**.
3. Seleccione **agregar** y vaya a la. Archivo MDF que desea adjuntar. 
1. Seleccione el archivo y haga clic en **Aceptar**. 
    1. La base de datos seleccionada debe mostrarse en la ventana inferior. Si el archivo aparece como "no encontrado", seleccione el botón de puntos suspensivos ( **...** ) junto al nombre de archivo y actualización de la ruta de acceso a la ruta correcta. 
    1. Si solo tiene el archivo de datos (.mdf) y no el archivo de registro (.ldf), a continuación, resalte el .ldf en la ventana inferior y seleccione **quitar**. Esto creará un nuevo archivo de registro. 
1. Seleccione **Aceptar** para adjuntar el archivo. Una vez que se adjunta el archivo, tendrá la base de datos de AdventureWorks instalada en su instancia de SQL Server.  

Para obtener más información sobre cómo conectar los archivos de base de datos, vea [adjuntar una base de datos](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Instalar en la base de datos SQL Azure


Si aún no tiene un servidor SQL Server en Azure, vaya a la [portal Azure](https://portal.azure.com/) y crear una nueva base de datos de SQL. En el proceso de creación de una base de datos, se creará un servidor. Tome nota del servidor. Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en cuestión de minutos.

1. Conectarse a Azure portal.
1. Seleccione **crear un recurso** en la parte superior izquierda del panel de navegación. 
1. Seleccione **bases de datos** y, a continuación, seleccione **base de datos SQL**. 
1. Escriba la información solicitada.
1. En el **Seleccionar origen** campo, seleccione **ejemplo (AdventureWorksLT)** para restaurar una copia de seguridad de la copia de seguridad más reciente de AdventureWorksLT.
1. Seleccione **crear** para crear la base de datos SQL nueva, que es la copia restaurada de la base de datos AdventureWorksLT. 


## <a name="see-also"></a>Vea también
[Tutoriales de SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Tutoriales para el motor de base de datos de SQL Server](../relational-databases/database-engine-tutorials.md)
