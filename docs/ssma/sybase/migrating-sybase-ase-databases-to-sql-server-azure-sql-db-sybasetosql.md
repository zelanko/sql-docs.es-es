---
title: 'Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL de Azure | Microsoft Docs'
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a021ac1cfc442943b15ade737c54d0b9e227ef03
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38982217"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrar bases de datos de SAP ASE a SQL Server: Azure SQL Database (SybaseToSQL)
SQL Server Migration Assistant (SSMA) para SAP Adaptive Server Enterprise (ASE) es un entorno integral que le ayuda a migrar rápidamente bases de datos de SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Azure SQL Database. Mediante el uso de SSMA para SAP ASE, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Azure SQL Database, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Azure SQL Database.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendado  
Para migrar correctamente los objetos y datos de bases de datos de SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Azure SQL Database, utilice el siguiente proceso:  
  
1.  [Cree un nuevo proyecto SSMA](http://msdn.microsoft.com/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Después de crear el proyecto, puede establecer las opciones de la asignación de tipos, migración y conversión del proyecto. Para obtener información acerca de la configuración del proyecto, vea [definir opciones de proyecto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obtener información acerca de cómo personalizar las asignaciones de tipos de datos, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar con el servidor de base de datos de SAP ASE](http://msdn.microsoft.com/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Conectarse a una instancia de SQL Server](http://msdn.microsoft.com/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) o [conecta a una instancia de Azure SQL Database](http://msdn.microsoft.com/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Asignar los esquemas de base de datos de SAP ASE a SQL Server / esquemas de base de datos de Azure SQL Database](http://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Si lo desea, [crear informes de evaluación](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) para evaluar los objetos de base de datos para la conversión y estimar el tiempo de conversión.  
  
6.  [Convertir esquemas de base de datos de SAP ASE en SQL Server / esquemas de base de datos de SQL Azure](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server / Azure SQL Database](http://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Guardar un script y ejecutarlo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Azure SQL Database, o sincronizar los objetos de base de datos.  
  
8.  [Migrar datos a SQL Server / Azure SQL Database](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introducción a SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
