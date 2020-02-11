---
title: 'Migración de datos de Access en SQL Server: Azure SQL DB (AccessToSQL) | Microsoft Docs'
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 8f0e93efee0c57c904c32ec52fbb560f973f21b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907144"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migración de datos de Access en SQL Server: Azure SQL DB (AccessToSQL)
Después de haber creado correctamente los objetos de base [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de datos en, puede migrar los datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Access a o SQL Azure.  
  
## <a name="setting-migration-options"></a>Establecer opciones de migración  
Antes de migrar datos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, revise las opciones de migración del proyecto en el cuadro de diálogo **configuración del proyecto** . En este cuadro de diálogo, puede establecer el tamaño del lote de migración, el bloqueo de tablas, la comprobación de restricciones, la activación del desencadenador de inserción, la identidad y el control de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valores NULL, y cómo controlar las fechas que están fuera del intervalo. Para obtener más información, vea [configuración del proyecto (migración)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migrar datos  
La migración de datos es una operación de carga masiva que mueve filas de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a o SQL Azure en transacciones. El número de filas que se van a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cargar en o SQL Azure en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de migración, asegúrese de que el panel de resultados esté visible. Si no es así, en el menú **Ver** , seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Asegúrese de que ha cargado los objetos de base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos de Access en o SQL Azure.  
  
2.  En el explorador de metadatos de Access, seleccione los objetos que contienen los datos que desea migrar:  
  
    -   Para migrar datos de una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para migrar datos de tablas individuales, expanda la base de datos, expanda **tablas**y, a continuación, active la casilla situada junto a la tabla. Para omitir los datos de tablas individuales, desactive la casilla.  
  
3.  Haga clic con el botón derecho en **bases** de **datos y seleccione migrar datos**.  
  
También puede migrar datos fuera de SSMA mediante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilidad de línea de comandos **BCP** o. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Para obtener más información acerca de estas herramientas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea los libros en pantalla de.  
  
## <a name="next-step"></a>siguiente paso  
Si tiene acceso a las aplicaciones de base de datos que desea seguir usando después de la migración, vincule las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos de Access a las tablas o SQL Azure. Para obtener más información, consulte [vincular aplicaciones de Access a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Consulte también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Configuración de las opciones de conversión y de migración](setting-conversion-and-migration-options-accesstosql.md)  
  
