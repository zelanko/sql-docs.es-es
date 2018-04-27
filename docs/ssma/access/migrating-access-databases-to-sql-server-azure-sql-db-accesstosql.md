---
title: 'Migrar bases de datos de Access a SQL Server: base de datos de SQL Azure | Documentos de Microsoft'
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
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
ms.workload: On Demand
ms.openlocfilehash: bbbea4be309e1508620e9e067c94328905fcc824
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="migrating-access-databases-to-sql-server---azure-sql-db-accesstosql"></a>Migrar bases de datos de Access a SQL Server: base de datos de SQL de Azure (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) es una herramienta que proporciona un entorno completo que le ayuda a migrar rápidamente bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Mediante el uso de SSMA, puede revisar el acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure objetos de base de datos, evaluar la base de datos de Access para la migración, convierte los objetos de base de datos de Access, cargarlos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, y, a continuación, migrar los datos.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendada  
Para migrar correctamente los datos y objetos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, siga este procedimiento:  
  
1.  [Cree un nuevo proyecto de SSMA](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7). Después de crear el proyecto, puede [definir opciones de proyecto](http://msdn.microsoft.com/0a7304df-2f35-4453-96ef-7ac83dea1167), incluidas las opciones de conversión, opciones de migración y asignaciones de tipos de datos.  
  
2.  [Agregar archivos de base de datos de Access](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced) al proyecto.  
  
    Puede agregar archivos individuales, incluidos los archivos que encuentra en el equipo o red.  
  
3.  [Conectar a la instancia de destino de SQL Server](http://msdn.microsoft.com/f84cf007-ddf1-4396-a07c-3e0729abc769) o [conectar a la instancia de destino de SQL Azure](http://msdn.microsoft.com/1ba0d113-dc05-4431-8689-e14a8821bafd).  
  
    Puede conectarse a SQL Server o SQL Azure.  
  
4.  Para personalizar la asignación entre una o varias bases de datos de Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de SQL Azure, [asignar las bases de datos de origen y de destino](http://msdn.microsoft.com/69bee937-7b2c-49ee-8866-7518c683fad4).  
  
5.  Si lo desea, puede [crear un informe de evaluación](http://msdn.microsoft.com/8b9e23d6-da62-437a-8c05-8ad2628b9441) para determinar si los objetos de base de datos de Access se pueden convertir correctamente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure.  
  
6.  [Convierte los objetos de base de datos de Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o definiciones de objetos de SQL Azure.  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
    Puede cargar objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure usando SSMA, o bien puede ahorrar [!INCLUDE[tsql](../../includes/tsql_md.md)] secuencias de comandos.  
  
8.  [Migrar datos de Access a SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
    > [!NOTE]  
    > Puede convertir, cargar y migrar esquemas y datos en un solo paso. Para realizar la migración de un solo clic, haga clic en el **convertir, cargar y migrar** botón.  
  
9. Si desea que las aplicaciones de Access para usar los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure, use [vincular las tablas de acceso a las tablas de SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4).  
  
También puede usar al Asistente para migración para guiarle a través de este proceso. Para obtener más información, consulte [Asistente para migración de](http://msdn.microsoft.com/5bab5914-b2ae-4795-8cf5-83e42d64bef2).  
  
## <a name="see-also"></a>Vea también  
[Introducción a SQL Server Migration Assistant para Access](http://msdn.microsoft.com/462a731f-08f1-44e1-9eeb-4deac6d2f6c5)  
[Preparar las bases de datos de acceso para la migración](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)
