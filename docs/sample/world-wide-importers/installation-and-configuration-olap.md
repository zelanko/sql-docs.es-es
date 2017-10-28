---
title: "Instalación y configuración | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d07ffb9a-ac4f-4295-9aeb-ecfb97600134
caps.latest.revision: 3
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: f40894ea8ee3d7b998a8a45170e9833f2e6c763f
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW instalación y configuración
Instrucciones de instalación y configuración para la base de datos de WideWorldImportersDW.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (o superior) o [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/). Para usar la versión completa del ejemplo, use SQL Server Evaluation, Developer o Enterprise Edition.
- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados utilizando la versión de junio de 2016 o posterior.

## <a name="download"></a>Descargar

La versión más reciente del ejemplo:

[Wide world importers versión](http://go.microsoft.com/fwlink/?LinkID=800630)

Descargar el ejemplo WideWorldImportersDW base de datos copia de seguridad/bacpac que corresponde a la edición de SQL Server o base de datos de SQL Azure.

Código fuente para volver a crear la base de datos de ejemplo está disponible en la ubicación siguiente. Tenga en cuenta que el rellenado de datos se basa en ETL de la base de datos OLTP (WideWorldImporters):

[Wide world importers origen](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

Para restaurar una copia de seguridad a una instancia de SQL Server, puede utilizar Management Studio.

1. Abra SQL Server Management Studio y conéctese a la instancia de SQL Server de destino.
2. Haga doble clic en el **bases de datos** nodo y seleccione **Restaurar base de datos**.
3. Seleccione **dispositivo** y haga clic en el botón **...**
4. En el cuadro de diálogo **seleccionar dispositivos de copia de seguridad**, haga clic en **agregar**, vaya a la copia de seguridad de base de datos en el sistema de archivos del servidor y seleccione la copia de seguridad. Haga clic en **Aceptar**.
5. Si es necesario, cambie la ubicación de destino para los datos y archivos de registro, en la **archivos** panel. Tenga en cuenta que es una práctica recomendada para colocar datos y archivos de registro en unidades diferentes.
6. Haga clic en **Aceptar**. Se iniciará la restauración de base de datos. Una vez que se complete, tendrá la base de datos WideWorldImporters instalados en su instancia de SQL Server.

### <a name="azure-sql-database"></a>Base de datos SQL de Azure

Para importar un bacpac en una base de datos SQL, puede utilizar Management Studio.

1. (opcional) Si aún no dispone de un servidor SQL Server en Azure, navegue hasta la [portal de Azure](https://portal.azure.com/) y crear una nueva base de datos de SQL. Durante el proceso de crear una base de datos, se creará un servidor. Tome nota del servidor.
   - Vea [este tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) para crear una base de datos en minutos
2. Abra SQL Server Management Studio y conéctese a su servidor en Azure.
3. Haga doble clic en el **bases de datos** nodo y seleccione **importación Data-Tier Application**.
4. En el **importar la configuración** seleccione **importar desde el disco local** y seleccione el archivo bacpac de la base de datos de ejemplo en el sistema de archivos.
5. En **configuración de base de datos** cambie el nombre de la base de datos a *WideWorldImportersDW* y seleccione el objetivo de edición y el servicio de destino para usar.
6. Haga clic en **siguiente** y **finalizar** para comenzar la implementación. Tardará unos minutos en completarse. Al especificar un objetivo de servicio inferior S2 puede tardar más.

## <a name="configuration"></a>Configuración

[Se aplica a SQL Server 2016 (y versiones posteriores) Developer, Evaluation y Enterprise Edition]

La base de datos de ejemplo puede hacer uso de PolyBase en archivos de consulta en el almacenamiento de blobs de Azure o Hadoop. Sin embargo, esta característica no está instalada de forma predeterminada con SQL Server, debe seleccionar durante la instalación de SQL Server. Por lo tanto, se requiere un paso de posterior a la instalación.

1. En SQL Server Management Studio, conéctese a la base de datos de WideWorldImportersDW y abrir una nueva ventana de consulta.
2. Ejecute el siguiente comando de T-SQL para habilitar el uso de PolyBase en la base de datos:

   EJECUTE [aplicación]. [Configuration_ApplyPolyBase]

