---
title: Instalar & configurar la base de datos de ejemplo de DW WideWorldImporters
description: Siga estas instrucciones para descargar, instalar y configurar la base de datos de ejemplo WideWorldImportersDW con SQL Server Management Studio.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488561"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW Instalación y configuración
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Instrucciones de instalación y configuración para la base de datos WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o superior) o [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para usar la versión completa del ejemplo, use EVALUAción/Desarrollador/Empresa de SQL ServerSQL Server .
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, utilice la versión de junio de 2016 o posterior.

## <a name="download"></a>Descargar

La última versión del ejemplo:

[liberación de importadores de todo el mundo](https://go.microsoft.com/fwlink/?LinkID=800630)

Descargue la copia de seguridad/bacpac de base de datos WideWorldImportersDW de ejemplo que corresponde a la edición de SQL Server SQL Server o Azure SQL Database.

El código fuente para volver a crear la base de datos de ejemplo está disponible en la siguiente ubicación. Tenga en cuenta que la población de datos se basa en ETL de la base de datos OLTP (WideWorldImporters):

[gran parte del mundo-importadores-fuente](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>Instalar


### <a name="sql-server"></a>SQL Server

Para restaurar una copia de seguridad en una instancia de SQL Server, puede usar Management StudioManagement Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL ServerSQL Server de destino.
2. Haga clic con el botón derecho en el nodo **Bases de datos** y seleccione Restaurar base de **datos**.
3. Seleccione **Dispositivo** y haga clic en el botón **...**
4. En el cuadro de diálogo **Seleccionar dispositivos**de copia de seguridad , haga clic en **Agregar**, vaya a la copia de seguridad de la base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **OK**.
5. Si es necesario, cambie la ubicación de destino de los archivos de datos y de registro en el panel **Archivos.** Tenga en cuenta que se recomienda colocar datos y archivos de registro en diferentes unidades.
6. Haga clic en **OK**. Esto iniciará la restauración de la base de datos. Una vez completada, tendrá la base de datos WideWorldImporters instalada en la instancia de SQL Server.

### <a name="azure-sql-database"></a>Azure SQL Database

Para importar un bacpac en una nueva base de datos SQL, puede usar Management StudioManagement Studio.

1. (opcional) Si aún no tiene un servidor SQL Server en Azure, vaya a [Azure Portal](https://portal.azure.com/) y cree una nueva base de datos SQL. En el proceso de crear una base de datos, creará un servidor. Anote el servidor.
   - Vea [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en minutos
2. Abra SQL Server Management Studio y conéctese al servidor en Azure.
3. Haga clic con el botón derecho en el nodo Bases de **datos** y seleccione **Importar aplicación de capa de datos**.
4. En Configuración de **importación,** seleccione **Importar desde el disco local** y seleccione el bacpac de la base de datos de ejemplo del sistema de archivos.
5. En **Configuración** de la base de datos, cambie el nombre de la base de datos a *WideWorldImportersDW* y seleccione la edición de destino y el objetivo de servicio que desea usar.
6. Haga clic en **Siguiente** y **Finalizar** para iniciar la implementación. Esta operación tardará algunos minutos en completarse. Al especificar un objetivo de servicio inferior a S2, puede tardar más tiempo.

## <a name="configuration"></a>Configuración

[Se aplica a SQL Server 2016 (y versiones posteriores) Desarrollador/Evaluación/Enterprise Edition]

La base de datos de ejemplo puede hacer uso de PolyBase para consultar archivos en Hadoop o Azure Blob Storage. Sin embargo, esa característica no está instalada de forma predeterminada con SQL Server: debe seleccionarla durante la instalación de SQL ServerSQL Server . Por lo tanto, se requiere un paso posterior a la instalación.

1. En SQL Server Management StudioSQL Server Management Studio, conéctese a la base de datos WideWorldImportersDW y abra una nueva ventana de consulta.
2. Ejecute el siguiente comando T-SQL para habilitar el uso de PolyBase en la base de datos:

   EXECUTE [Aplicación]. [Configuration_ApplyPolyBase]
