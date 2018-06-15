---
title: Migrar bases de datos a SQL Server en Linux | Documentos de Microsoft
description: En este artículo se describe las distintas opciones para migrar bases de datos y los datos a SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.custom: sql-linux
ms.openlocfilehash: c7b7225ae4e981244ee06194ea9e4ef595ba283d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321926"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>Migrar bases de datos y los datos estructurados a SQL Server en Linux 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede migrar los datos y las bases de datos a SQL Server 2017 ejecutando en Linux. El método que elija para utilizar depende de los datos de origen y su escenario concreto. Las secciones siguientes proporcionan recomendaciones para diversos escenarios de migración.

## <a name="migrate-from-sql-server-on-windows"></a>Migrar de SQL Server en Windows
Si van a migrar bases de datos de SQL Server en Windows para SQL Server 2017 en Linux, la técnica recomendada es utilizar copia de seguridad de SQL Server y restauración.

1. Cree una copia de seguridad de la base de datos en el equipo de Windows.
2. Transfiera el archivo de copia de seguridad para el equipo de SQL Server para Linux de destino.
3. Restaure la copia de seguridad en el equipo Linux. 

Para obtener un tutorial sobre cómo migrar una base de datos con copia de seguridad y restauración, vea el tema siguiente:

- [Restaurar una base de datos de SQL Server de Windows en Linux](sql-server-linux-migrate-restore-database.md).

También es posible exportar la base de datos a un archivo BACPAC (un archivo comprimido que contiene el esquema de base de datos y los datos). Si tiene un archivo BACPAC, puede transferir este archivo en el equipo Linux y, a continuación, importarlo en SQL Server. Para obtener más información, consulte los temas siguientes:

- [Exportar e importar una base de datos con SSMS o SqlPackage.exe](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>Migrar desde otros servidores de base de datos
Puede migrar las bases de datos en otros sistemas de base de datos a SQL Server 2017 en Linux. Esto incluye las bases de datos de Microsoft Access, DB2, MySQL, Oracle y Sybase. En este escenario, use SQL Server Management Assistant (SSMA) para automatizar la migración a SQL Server en Linux. Para obtener más información, consulte [SSMA de uso para migrar bases de datos a SQL Server en Linux](sql-server-linux-migrate-ssma.md).  

## <a name="migrate-structured-data"></a>Migrar datos estructurados
También hay técnicas para la importación de datos sin procesar. Podría haber estructurado archivos de datos que se exportaron desde otras bases de datos u orígenes de datos. En este caso, puede usar la herramienta bcp para una inserción masiva los datos. O bien, puede ejecutar SQL Server Integration Services en Windows para importar los datos en una base de datos de SQL Server en Linux. SQL Server Integration Services permite ejecutar transformaciones más complejas en los datos durante la importación. 

Para obtener más información acerca de estas técnicas, vea los temas siguientes:

- [Datos de copia masiva con bcp](sql-server-linux-migrate-bcp.md)
- [Extraer, transformar y cargar datos de SQL Server en Linux con SSIS](sql-server-linux-migrate-ssis.md) 
