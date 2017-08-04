---
title: 'Migrar bases de datos de Sybase ASE a SQL Server: base de datos de SQL Azure | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 63dc9188d93def41a5116386f93bf29e3b744e8e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-sybase-ase-databases-to-sql-server---azure-sql-db-sybasetosql"></a>Migrar bases de datos de ASE de Sybase a SQL Server: base de datos de SQL Azure (SybaseToSQL)
SQL Server Migration Assistant (SSMA) para Sybase es un entorno integral que le ayuda a migrar rápidamente las bases de datos de Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Mediante el uso de SSMA para Sybase, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar correctamente los objetos y datos de las bases de datos de la ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, siga este procedimiento:  
  
1.  [Cree un nuevo proyecto SSMA](http://msdn.microsoft.com/en-us/11091d95-c488-48c3-891a-743cac94ac93).  
  
    Después de crear el proyecto, puede establecer la conversión del proyecto, migración y opciones de la asignación de tipos. Para obtener información acerca de la configuración de proyecto, vea [establecer las opciones del proyecto &#40; SybaseToSQL &#41; ](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obtener información acerca de cómo personalizar las asignaciones de tipos de datos, vea [asignación Sybase ASE y tipos de datos de SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conectar con el servidor de base de datos de Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
3.  [Conectarse a una instancia de SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) o [conecta a una instancia de base de datos de SQL Azure](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7).  
  
4.  [Asignar esquemas de base de datos de ASE a SQL Server / base de datos de Azure SQL database esquemas](http://msdn.microsoft.com/en-us/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Si lo desea, [crear informes de evaluación](http://msdn.microsoft.com/en-us/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c) para evaluar los objetos de base de datos para la conversión y calcular el tiempo de conversión.  
  
6.  [Convertir esquemas de base de datos de Sybase ASE en SQL Server / esquemas de base de datos de SQL Azure](http://msdn.microsoft.com/en-us/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server / base de datos de SQL Azure](http://msdn.microsoft.com/en-us/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Puede, ya sea por guardar un script y ejecútelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, también puede sincronizar los objetos de base de datos.  
  
8.  [Migrar datos a SQL Server / base de datos de SQL Azure](http://msdn.microsoft.com/en-us/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introducción a SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

