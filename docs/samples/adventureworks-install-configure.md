---
title: Instalar & configurar la base de datos de ejemplo AdventureWorks
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0d9f6842ebe5e7d6ee923eef17f491f0cb7ef6ec
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056739"
---
# <a name="adventureworks-installation-and-configuration"></a>Instalación y configuración de AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Vínculos de descarga e instrucciones de instalación de AdventureWorks. 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) o [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para obtener la versión completa del ejemplo, use SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, use la versión de junio de 2016 o posterior.
 
## <a name="github-links"></a>Vínculos de github

- [Todos los archivos de AdventureWorks para SQL 2014-2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Todos los archivos de AdventureWorks para SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Todos los archivos de AdventureWorks para SQL 2008 y 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>Descargas de OLTP

A continuación encontrará vínculos directos a las versiones de OLTP de AdventureWorks:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Descargas de almacenamiento de datos

Los vínculos directos a las versiones de almacenamiento de datos de AdventureWorks se pueden encontrar a continuación:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>Scripts de creación
Los scripts siguientes se pueden usar para crear la base de datos de AdventureWorks completa, independientemente de la versión. 

- [Zip de scripts OLTP de AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [Código postal de los scripts de AdventureWorks DW](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>Instalar en SQL Server

### <a name="restore-backup"></a>Restaurar copia de seguridad
Siga los pasos que se indican a continuación para restaurar una copia de seguridad de la base de datos mediante SQL Server Management Studio. 

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga clic con el botón secundario en el nodo **bases** de datos y seleccione **restaurar base de datos**.
3. Seleccione **dispositivo** y haga clic en los puntos suspensivos ( **...** )
4. En el cuadro de diálogo **seleccionar dispositivos de copia de seguridad**, haga clic en **Agregar**, desplácese hasta la copia de seguridad de base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **Aceptar**.
5. Si es necesario, cambie la ubicación de destino de los archivos de datos y de registro, en el panel **archivos** . Tenga en cuenta que se recomienda colocar los archivos de datos y de registro en unidades diferentes.
6. Haga clic en **Aceptar**. Se iniciará la restauración de la base de datos. Una vez completado, tendrá la base de datos AdventureWorks instalada en la instancia de SQL Server.

Para obtener más información acerca de cómo restaurar una base de datos de SQL Server, consulte [restaurar una copia de seguridad de base de datos con SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Adjuntar un archivo de datos
Siga los pasos siguientes para adjuntar el archivo de datos para la base de datos mediante SQL Server Management Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga clic con el botón secundario en el nodo **bases** de datos y seleccione **adjuntar**.
3. Seleccione **Agregar** y navegue hasta el. Archivo MDF que desea adjuntar. 
1. Seleccione el archivo y haga clic en **Aceptar**. 
    1. La base de datos seleccionada debe aparecer en la ventana inferior. Si el archivo aparece como "no encontrado", seleccione los puntos suspensivos ( **...** ) junto al nombre de archivo y actualice la ruta de acceso a la ruta de acceso correcta. 
    1. Si solo tiene el archivo de datos (. MDF), y no el archivo de registro (. ldf), resalte el. ldf en la ventana inferior y seleccione **quitar**. Se creará un nuevo archivo de registro. 
1. Seleccione **Aceptar** para adjuntar el archivo. Una vez que se haya adjuntado el archivo, tendrá la base de datos AdventureWorks instalada en la instancia de SQL Server.  

Para obtener más información sobre cómo adjuntar archivos de base de datos, vea [adjuntar una base de datos](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Instalar en Azure SQL Database


Si aún no tiene un SQL Server en Azure, vaya al [Azure portal](https://portal.azure.com/) y cree un nuevo SQL Database. En el proceso de creación de una base de datos, creará un servidor. Tome nota del servidor. Vea [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en minutos.

1. Conéctese a su Azure Portal.
1. Seleccione **crear un recurso** en la parte superior izquierda del panel de navegación. 
1. Seleccione **bases de datos** y, a continuación, seleccione **SQL Database**. 
1. Escriba la información solicitada.
1. En el campo **Seleccionar origen** , seleccione **ejemplo (AdventureWorksLT)** para restaurar una copia de seguridad de la última copia de seguridad de AdventureWorksLT.
1. Seleccione **crear** para crear el nuevo SQL Database, que es la copia restaurada de la base de datos AdventureWorksLT. 


## <a name="see-also"></a>Vea también
[Tutoriales para SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Tutoriales de SQL Server motor de base de datos](../relational-databases/database-engine-tutorials.md)
