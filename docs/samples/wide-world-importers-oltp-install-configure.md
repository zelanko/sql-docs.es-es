---
title: Instalar y configurar la base de datos de ejemplo de WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8d1d00b5d3e5650e628935c840f280b278869b62
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984847"
---
# <a name="installation-and-configuration"></a>Instalación y configuración
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Instrucciones de instalación y configuración de base de datos OLTP de Wide World Importers.

## <a name="prerequisites"></a>Requisitos previos

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) (o posterior) o [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). Para obtener la versión completa del ejemplo, utilice SQL Server Evaluation, Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Para obtener los mejores resultados, use la versión de junio de 2016 o posterior.

## <a name="download"></a>Descargar

La versión más reciente del ejemplo:

[Wide world importers versión](http://go.microsoft.com/fwlink/?LinkID=800630)

Descargar el ejemplo WideWorldImporters base de datos copia de seguridad/bacpac que corresponde a la edición de SQL Server o Azure SQL Database.

Código fuente para volver a crear la base de datos de ejemplo está disponible en la siguiente ubicación. Tenga en cuenta que volver a crear el ejemplo tendrá como resultado ligeras diferencias en los datos, ya que no hay un factor aleatorio en la generación de datos:

[importadores de todo el mundo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

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
5. En **configuración de la base de datos** cambie el nombre de la base de datos a *WideWorldImporters* y seleccione el objetivo de edición y el servicio de destino para usar.
6. Haga clic en **siguiente** y **finalizar** a fin de iniciar la implementación. Lo hará de unos minutos en completarse en un P1. Si un precio más bajo nivel es el deseado, se recomienda importar a una base de datos P1 y, a continuación, cambiar el plan de tarifa en el nivel deseado.

## <a name="configuration"></a>Configuración

### <a name="full-text-indexing"></a>Indización de texto completo

La base de datos de ejemplo puede hacer uso de la indización de texto completo. Sin embargo, esa característica no está instalada de forma predeterminada con SQL Server, tiene que seleccionarla durante la instalación de SQL Server (está habilitado de forma predeterminada en la base de datos de SQL Azure). Por lo tanto, un paso posterior a la instalación es necesario.

1. En SQL Server Management Studio, conéctese a la base de datos WideWorldImporters y abra una nueva ventana de consulta.
2. Ejecute el siguiente comando de T-SQL para habilitar el uso de la indización de texto completo en la base de datos:  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

Se aplica a: SQL Server

Habilitar la auditoría en SQL Server requiere la configuración del servidor. Para habilitar la auditoría de SQL Server para el ejemplo de WideWorldImporters, ejecute la siguiente instrucción en la base de datos:

    EXECUTE [Application].[Configuration_ApplyAuditing]

En Azure SQL Database, la auditoría se configura mediante el [portal Azure](https://portal.azure.com/).

### <a name="row-level-security"></a>Seguridad de nivel de fila

Se aplica a: base de datos SQL Azure

Seguridad de nivel de fila no está habilitada de forma predeterminada en la descarga de bacpac de WideWorldImporters. Para habilitar la seguridad de nivel de fila en la base de datos, ejecute el siguiente procedimiento almacenado:

    EXECUTE [Application].[Configuration_ApplyAuditing]

