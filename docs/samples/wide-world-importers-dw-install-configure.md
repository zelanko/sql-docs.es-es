---
title: Base de datos de ejemplo de WideWorldImporters OLAP - instalar y configurar - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: ed3c5f1a4f2168196a651aea64c9c88311a197b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104251"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW instalación y configuración
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Instrucciones de instalación y configuración para la base de datos WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o posterior) o [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para usar la versión completa del ejemplo, use SQL Server Evaluation, Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, use la versión de junio de 2016 o posterior.

## <a name="download"></a>Descargar

La versión más reciente del ejemplo:

[Wide world importers versión](https://go.microsoft.com/fwlink/?LinkID=800630)

Descargar el ejemplo WideWorldImportersDW base de datos copia de seguridad/bacpac que corresponde a la edición de SQL Server o Azure SQL Database.

Código fuente para volver a crear la base de datos de ejemplo está disponible en la siguiente ubicación. Tenga en cuenta que el rellenado de datos se basa en ETL de la base de datos OLTP (WideWorldImporters):

[Wide world importers origen](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

Para restaurar una copia de seguridad a una instancia de SQL Server, puede usar Management Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga doble clic en el **bases de datos** nodo y seleccione **Restore Database**.
3. Seleccione **dispositivo** y haga clic en el botón **...**
4. En el cuadro de diálogo **seleccionar dispositivos de copia de seguridad**, haga clic en **agregar**, vaya a la copia de seguridad de base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **Aceptar**.
5. Si es necesario, cambie la ubicación de destino para los datos y archivos de registro, en el **archivos** panel. Tenga en cuenta que es una práctica recomendada para colocar los datos y archivos de registro en unidades distintas.
6. Haga clic en **Aceptar**. Esto iniciará la restauración de base de datos. Una vez haya terminado, tendrá la base de datos WideWorldImporters instalado en su instancia de SQL Server.

### <a name="azure-sql-database"></a>Se aplica a: Base de datos SQL de Azure

Para importar un archivo bacpac en una base de datos SQL, puede usar Management Studio.

1. (opcional) Si aún no tiene un servidor SQL Server en Azure, vaya a la [portal Azure](https://portal.azure.com/) y crear una nueva base de datos de SQL. En el proceso de creación de una base de datos, se creará un servidor. Tome nota del servidor.
   - Consulte [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en cuestión de minutos
2. Abra SQL Server Management Studio y conéctese a su servidor en Azure.
3. Haga doble clic en el **bases de datos** nodo y seleccione **Import Data-Tier Application**.
4. En el **importar la configuración** seleccione **importar desde el disco local** y seleccione el archivo bacpac de la base de datos de ejemplo en el sistema de archivos.
5. En **configuración de la base de datos** cambie el nombre de la base de datos a *WideWorldImportersDW* y seleccione el objetivo de edición y el servicio de destino para usar.
6. Haga clic en **siguiente** y **finalizar** a fin de iniciar la implementación. Se tardará unos minutos en completarse. Al especificar un objetivo de servicio inferior a S2 puede tardar más.

## <a name="configuration"></a>Configuración

[Se aplica a SQL Server 2016 (y versiones posteriores) Developer, Evaluation y Enterprise Edition]

La base de datos de ejemplo puede hacer uso de PolyBase para consultar los archivos de Hadoop o Azure blob storage. Sin embargo, esa característica no está instalada de forma predeterminada con SQL Server, tiene que seleccionarla durante la instalación de SQL Server. Por lo tanto, un paso posterior a la instalación es necesario.

1. En SQL Server Management Studio, conéctese a la base de datos WideWorldImportersDW y abra una nueva ventana de consulta.
2. Ejecute el siguiente comando de T-SQL para habilitar el uso de PolyBase en la base de datos:

   EJECUTE [aplicaciones]. [Configuration_ApplyPolyBase]
