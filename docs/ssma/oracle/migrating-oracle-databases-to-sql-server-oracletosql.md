---
title: Bases de datos de migración de Oracle a SQL Server (OracleToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 04/22/2018
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1d196dd6-4322-4c98-bb72-602c57d96134
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: c5137a8be3aa05b4d7f445e467750780ceba8c6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-oracle-databases-to-sql-server-oracletosql"></a>Migrar bases de datos de Oracle a SQL Server (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) para Oracle es un entorno integral que le ayuda a migrar rápidamente bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], base de datos de SQL Azure o almacenamiento de datos de SQL Azure. Mediante el uso de SSMA para Oracle, puede revisar los objetos de base de datos y los datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], base de datos de SQL Azure o almacenamiento de datos de SQL Azure, y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], base de datos de SQL Azure o de datos de SQL Azure Almacenamiento. Tenga en cuenta que no puede migrar esquemas SYS y sistema Oracle.
  
## <a name="recommended-migration-process"></a>El proceso de migración recomendado  
Para migrar correctamente los datos y objetos de bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], base de datos de SQL Azure o almacenamiento de datos de SQL Azure, siga este procedimiento:
  
1.  [Cree un nuevo proyecto SSMA](http://msdn.microsoft.com/en-us/ee5d94c0-c7a6-4779-bd32-729bdaf61e1b).  
  
    Después de crear el proyecto, puede establecer la conversión del proyecto, migración y opciones de la asignación de tipos. Para obtener información acerca de la configuración de proyecto, vea [establecer las opciones del proyecto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md). Para obtener información sobre cómo personalizar las asignaciones de tipos de datos, vea [asignación de Oracle y tipos de datos de SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
2.  [Conectar con el servidor de base de datos de Oracle](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
3.  [Conéctese a una instancia de SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
4.  [Esquemas de base de datos de Oracle se asignan a los esquemas de base de datos de SQL Server](http://msdn.microsoft.com/en-us/0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc).  
  
5.  Si lo desea, [crear informes de evaluación](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357) para evaluar los objetos de base de datos para la conversión y calcular el tiempo de conversión.  
  
6.  [Convertir esquemas de base de datos de Oracle en esquemas de SQL Server](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272).  
  
7.  [Cargar los objetos de base de datos convertida en SQL Server](http://msdn.microsoft.com/en-us/a8ae33b2-1883-4785-922b-ea0e31c0b37a).  
  
    Puede hacerlo en una de las maneras siguientes:  
  
    -   Guardar un script y ejecútelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Sincronizar los objetos de base de datos.  
  
8.  [Migrar datos a SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13).  
  
9. Si es necesario, actualizar las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Vea también  
[Instalación de SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md)  
[Introducción a SSMA para Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/getting-started-with-ssma-for-oracle-oracletosql.md)  
  
