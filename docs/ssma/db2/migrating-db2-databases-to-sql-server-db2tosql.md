---
title: Migración de bases de datos DB2 a SQL Server (DB2ToSQL) | Microsoft Docs
description: Utilice este proceso recomendado para migrar bases de datos de DB2 a SQL Server o Azure SQL Database mediante SQL Server Migration Assistant (SSMA).
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 14d2e655-af7e-4aa5-ba28-0e3d0d025518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c0a762cbe49a3186a29feb5aa3424b083d2f8978
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933746"
---
# <a name="migrating-db2-databases-to-sql-server-db2tosql"></a>Migración de bases de datos DB2 a SQL Server (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Migration Assistant (SSMA) para DB2 es un entorno completo que le ayuda a migrar rápidamente las bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Con SSMA para DB2, puede revisar los datos y los objetos de base de datos, evaluar las bases de datos para la migración, migrar objetos de base de datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database y, a continuación, migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Tenga en cuenta que no puede migrar los esquemas SYS y SYSTEM DB2.  
  
## <a name="recommended-migration-process"></a>Proceso de migración recomendado  
Para migrar correctamente objetos y datos de bases de datos DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, utilice el siguiente proceso:  
  
1.  [Nuevo proyecto de SSMA](https://msdn.microsoft.com/66437b45-4686-4fc7-a91b-ebde45e0f1b0).  
  
    Después de crear el proyecto, puede establecer las opciones de conversión de proyectos, migración y asignación de tipos. Para obtener información sobre la configuración del proyecto, vea [configuración del proyecto &#40;conversión&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md) y secciones relacionadas. Para obtener información acerca de cómo personalizar las asignaciones de tipos de datos, consulte [asignar tipos de datos de DB2 y SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
2.  [Conéctese a la base de datos DB2](https://msdn.microsoft.com/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
3.  [Conexión a SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e).  
  
4.  [Asigne esquemas DB2 a esquemas de SQL Server](https://msdn.microsoft.com/05ff7bd4-e60b-4f48-a893-bc2346aa9a8a).  
  
5.  Opcionalmente, los [informes de evaluación](https://msdn.microsoft.com/9e13eba0-e3cf-4205-974f-c00f982061de) para evaluar los objetos de base de datos para la conversión y estiman el tiempo de conversión.  
  
6.  [Convertir esquemas DB2](https://msdn.microsoft.com/7947efc3-ca86-4ec5-87ce-7603059c75a0).  
  
7.  [Cargue los objetos de base de datos convertidos en SQL Server](https://msdn.microsoft.com/f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3).  
  
    Para ello, siga uno de estos métodos:  
  
    -   Guarde un script y ejecútelo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Sincronizar los objetos de base de datos.  
  
8.  [Migración de datos de DB2 a SQL Server](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b).  
  
9. Si es necesario, actualice las aplicaciones de base de datos.  
  
## <a name="see-also"></a>Consulte también  
[Instalación de SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)  
[Introducción con SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/getting-started-with-ssma-for-db2-db2tosql.md)  
  
