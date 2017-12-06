---
title: "Asignación de las bases de datos de MySQL a esquemas SQL Server (MySQLToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77a150ac9568f614869b3e6f168c96eb47d2e764
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Asignación de las bases de datos de MySQL a esquemas SQL Server (MySQLToSQL)
De forma predeterminada, SSMA para MySQL migra todos los objetos de un esquema de MySQL para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o con el nombre para el esquema de base de datos de SQL Azure. Sin embargo, puede personalizar la asignación entre esquemas de MySQL y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o bases de datos de SQL Azure.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL y SQL Server o SQL Azure esquemas  
El concepto de MySQL de un esquema se asigna a los conceptos de SQL Server de una base de datos y uno de sus esquemas. SSMA hace referencia a la combinación de SQL Server de la base de datos y el esquema como un esquema.  
  
El concepto de MySQL de un esquema se asigna a los conceptos de SQL Server de una base de datos y uno de sus esquemas. Por ejemplo, MySQL podría tener un esquema denominado **HR**. Una instancia de SQL Server podría tener una base de datos denominada **HR**, y dentro de esa base de datos son esquemas. Un esquema es el **dbo** (o el propietario de la base de datos) esquema. De forma predeterminada, el esquema de MySQL **HR** va a asignar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos y esquema **HR.dbo**. SSMA hace referencia a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinación de base de datos y el esquema como un esquema.  
  
Puede modificar la asignación entre MySQL y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de Azure.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, puede asignar un esquema de MySQL a disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquema de SQL Azure.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de MySQL, seleccione **esquemas**.  
  
    El **esquema de asignación** ficha también está disponible al seleccionar esquemas individuales. La lista en la **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todos los esquemas de MySQL, seguido por un valor de destino. Este destino se indica en la notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o que se migrarán los objetos y datos de SQL Azure.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
    En el **elegir el esquema de destino** cuadro de diálogo, puede buscar base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
4.  El destino se cambia en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que va a asignar es no existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a continuación, se le pedirá con un mensaje **"la base de datos o el esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De igual forma, se puede asignar el esquema al esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos que se creará durante la sincronización.  
  
-   Asignación a SQL Azure  
  
Puede asignar la base de datos de origen al destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos o al cualquier esquema en el destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos. Si asignar el esquema de origen ningún esquema no existe en la base de datos de destino conectados, se le pedirá con un mensaje **"esquema no existe en los metadatos de destino. Se crearán durante la sincronización. ¿Desea continuar? "** Haga clic en Sí.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de MySQL y un esquema de SQL Server, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione una fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea analizar la conversión de objetos de MySQL en objetos de SQL Server o SQL Azure, también puede [crear un informe de conversión](http://msdn.microsoft.com/en-us/2a56a003-3b0f-453a-963c-00c9e40933ec) en caso contrario, puede [convertir las definiciones de objeto de base de datos de MySQL](http://msdn.microsoft.com/en-us/ac21850b-fb32-4704-9985-5759b7c688c7) en esquemas de SQL Server o SQL Azure  
  
## <a name="see-also"></a>Vea también  
[Configuración del proyecto &#40; Conversión &#41; &#40; MySQLToSQL &#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Conectarse a la base de datos de SQL Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Migrar bases de datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectarse a SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
