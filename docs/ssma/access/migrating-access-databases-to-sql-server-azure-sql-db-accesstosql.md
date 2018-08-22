---
title: 'Migrar bases de datos de Access a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- instructions, migration
- migrating databases, overview
- overview, migration process
- procedure, migration
- recommended migration process
ms.assetid: 76a3abcf-2998-4712-9490-fe8d872c89ca
caps.latest.revision: 23
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: f3552b4617d4579be7beebccae357b417ea6a563
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394749"
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrar bases de datos de Access a SQL Server: Azure SQL DB (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) es una herramienta que proporciona un entorno completo que le permite migrar rápidamente bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Mediante el uso de SSMA, puede revisar el acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure los objetos de base de datos, evaluar la base de datos de acceso para la migración, convierte los objetos de base de datos de Access, cargarlos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, y, a continuación, migrar los datos.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendado  
Para migrar correctamente los objetos y datos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, utilice el siguiente proceso:  
  
1.  [Cree un nuevo proyecto de SSMA](creating-and-managing-projects-accesstosql.md). Después de crear el proyecto, puede [establecer opciones de proyecto](setting-conversion-and-migration-options-accesstosql.md), incluidas las opciones de conversión, las opciones de migración y asignaciones de tipos de datos.  
  
2.  [Agregar archivos de base de datos de Access](adding-and-removing-access-database-files-accesstosql.md) al proyecto.  
  
    Puede agregar archivos individuales, incluidos los archivos que encontrará en el equipo o red.  
  
3.  [Conectar a la instancia de destino de SQL Server](connecting-to-sql-server-accesstosql.md) o [conectar a la instancia de destino de SQL Azure](connecting-to-azure-sql-db-accesstosql.md).  
  
    Puede conectarse a SQL Server o SQL Azure.  
  
4.  Para personalizar la asignación entre una o varias bases de datos de Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de SQL Azure, [asignar las bases de datos de origen y destino](mapping-source-and-target-databases-accesstosql.md).  
  
5.  Opcionalmente, puede [crear un informe de evaluación](assessing-access-database-objects-for-conversion-accesstosql.md) para determinar si los objetos de base de datos de Access se pueden convertir correctamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
6.  [Convierte los objetos de base de datos de Access](converting-access-database-objects-accesstosql.md) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o definiciones de objetos de SQL Azure.  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
    Puede cargar objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure mediante el uso de SSMA, o bien puede guardar [!INCLUDE[tsql](../../includes/tsql-md.md)] secuencias de comandos.  
  
8.  [Migrar los datos de Access a SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
    > [!NOTE]  
    > Puede convertir, cargar y migrar esquemas y datos en un solo paso. Para realizar la migración de un solo clic, haga clic en el **convertir, cargar y migrar** botón.  
  
9. Si desea usar los datos en las aplicaciones de Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, use [vincular las tablas de acceso a las tablas de SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
También puede usar al Asistente para migración para guiarle a través de este proceso. Para obtener más información, consulte [Asistente para migración](migration-wizard-accesstosql.md).  
  
## <a name="see-also"></a>Vea también  
[Introducción a SQL Server Migration Assistant para Access](getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Preparar las bases de datos de acceso para la migración](preparing-access-databases-for-migration-accesstosql.md)
