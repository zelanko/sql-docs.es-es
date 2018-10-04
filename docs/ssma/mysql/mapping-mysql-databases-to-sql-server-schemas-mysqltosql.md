---
title: Asignación de bases de datos MySQL a esquemas de SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: ba413a15f0d201ecaddadf83e353d28ee3010c50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721953"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Asignación de bases de datos de MySQL a esquemas de SQL Server (MySQLToSQL)
De forma predeterminada, SSMA para MySQL migra todos los objetos en un esquema de MySQL a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o con nombre para el esquema de base de datos de SQL Azure. Sin embargo, puede personalizar la asignación entre esquemas de MySQL y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos de SQL Azure.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL y SQL Server o SQL Azure esquemas  
El concepto de MySQL de un esquema se asigna al concepto de una base de datos y uno de sus esquemas de SQL Server. SSMA se refiere a la combinación de SQL Server de base de datos y el esquema como un esquema.  
  
El concepto de MySQL de un esquema se asigna al concepto de una base de datos y uno de sus esquemas de SQL Server. Por ejemplo, MySQL podría tener un esquema denominado **HR**. Una instancia de SQL Server podría tener una base de datos denominada **HR**, y dentro de esa base de datos son los esquemas. Un esquema es el **dbo** (o el propietario de la base de datos) esquema. De forma predeterminada, el esquema de MySQL **HR** se asignará a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos y esquema **HR.dbo**. SSMA se refiere a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinación de la base de datos y el esquema como un esquema.  
  
Puede modificar la asignación entre MySQL y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de Azure.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, puede asignar un esquema de MySQL para que haya disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquema de SQL Azure.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de MySQL, seleccione **esquemas**.  
  
    El **esquema de asignación** ficha también está disponible al seleccionar esquemas individuales. La lista en el **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todos los esquemas de MySQL, seguido por un valor de destino. Este destino se indica en una notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure donde se migrarán los objetos y datos.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
    En el **elija el esquema de destino** cuadro de diálogo, puede examinar para la base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
4.  Cambia el destino en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que se está asignando es que no existe en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a continuación, se le pedirá con un mensaje **"la base de datos y/o esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De forma similar, se puede asignar el esquema al esquema que no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos que se creará durante la sincronización.  
  
-   Asignación de SQL Azure  
  
Puede asignar la base de datos de origen al destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos o al cualquier esquema en el destino conectado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Si el esquema de origen se asignan a cualquier esquema que no existe en la base de datos de destino conectados, entonces se le pedirá con un mensaje **"esquema no existe en los metadatos de destino. Se crearán durante la sincronización. ¿Desea continuar? "** Haga clic en Sí.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de MySQL y un esquema de SQL Server, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione cualquier fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea analizar la conversión de objetos de MySQL en objetos de SQL Server o SQL Azure, puede [crear un informe de conversión](assessing-mysql-databases-for-conversion-mysqltosql.md) en caso contrario puede [convertir las definiciones de objeto de base de datos MySQL](converting-mysql-databases-mysqltosql.md) en SQL Esquemas de servidor o de SQL Azure  
  
## <a name="see-also"></a>Vea también  
[Configuración del proyecto &#40;conversión&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Conexión a Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Bases de datos de migración desde MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Conectarse a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
