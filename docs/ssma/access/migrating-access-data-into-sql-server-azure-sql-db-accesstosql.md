---
title: 'Migración de datos de Access a SQL Server: Azure SQL DB (AccessToSQL) | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: d15d7608879d9116832e083654cc07717c72e23e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666474"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-db-accesstosql"></a>Migración de datos de Access a SQL Server: Azure SQL DB (AccessToSQL)
Después de haber creado correctamente los objetos de base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede migrar datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
## <a name="setting-migration-options"></a>Establecer las opciones de migración  
Antes de migrar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, revise las opciones de migración de proyecto en el **configuración del proyecto** cuadro de diálogo. En este cuadro de diálogo, puede establecer el tamaño de lote de migración, bloqueo de tablas, la restricción de comprobación, el desencadenador de inserción desencadenar, identidad y el valor null de control y cómo administrar fechas que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intervalo. Para obtener más información, consulte [configuración del proyecto (migración)](https://msdn.microsoft.com/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
## <a name="migrating-data"></a>Migración de datos  
Migración de datos están una operación de carga masiva que mueve las filas de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure en las transacciones. El número de filas que se carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure en cada transacción se configura en la configuración del proyecto.  
  
Para ver los mensajes de la migración, asegúrese de que está visible el panel de salida. Si no lo es, en el **vista** menú, seleccione **salida**.  
  
**Para migrar datos**  
  
1.  Asegúrese de que ha cargado los objetos de base de datos de Access en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
2.  En el Explorador de metadatos de acceso, seleccione los objetos que contienen los datos que se van a migrar:  
  
    -   Para migrar datos de una base de datos completa, active la casilla situada junto al nombre de la base de datos.  
  
    -   Para migrar datos de tablas individuales, expanda la base de datos, **tablas**y, a continuación, seleccione la casilla de verificación junto a la tabla. Para omitir los datos de tablas individuales, desactive la casilla de verificación.  
  
3.  Haga clic en **bases de datos** y, a continuación, seleccione **migrar datos**.  
  
También puede migrar datos fuera de SSMA mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bcp** utilidad de línea de comandos o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obtener más información acerca de estas herramientas, consulte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="next-step"></a>Paso siguiente  
Si tiene aplicaciones de base de datos de acceso que desea seguir usando después de la migración, vincular las tablas de base de datos de acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de SQL Azure. Para obtener más información, consulte [vincular aplicaciones de Access a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md).  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Conversión de la configuración y opciones de migración](setting-conversion-and-migration-options-accesstosql.md)  
  
