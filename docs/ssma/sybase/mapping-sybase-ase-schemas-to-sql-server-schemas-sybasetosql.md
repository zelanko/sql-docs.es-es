---
title: Asignación de esquemas de Sybase ASE a esquemas de SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b2250ded7d76ad35de8ad960356d272358201e37
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985107"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Asignación de esquemas de Sybase ASE a esquemas de SQL Server (SybaseToSQL)
En Sybase Adaptive Server Enterprise (ASE), cada base de datos tiene uno o varios esquemas. De forma predeterminada, SSMA migra todos los objetos dentro de una base de datos y el esquema a la misma base de datos y esquema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure. Sin embargo, puede personalizar la asignación entre el ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o bases de datos de SQL Azure y esquemas.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>ASE y SQL Server o SQL Azure esquemas  
ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure ambos especificar bases de datos y sus esquemas mediante la notación de dos elementos como *database.schema*. Por ejemplo, en un entorno ASE **demostración** base de datos, es posible que haya un **dbo** esquema. Que el par de base de datos y el esquema se especifica como **demo.dbo**. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure tiene la misma base de datos y el esquema, el par también se especifica como **demo.dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, se puede asignar un esquema de ASE que haya disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquema de SQL Azure.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de Sybase, seleccione **bases de datos**.  
  
    El **esquema de asignación** ficha también está disponible cuando se selecciona una base de datos individual, el **esquemas** carpeta o esquemas individuales. La lista en el **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todas las bases de datos de ASE con sus esquemas, seguidos por un valor de destino. Este destino se indica en una notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o SQL Azure donde se migrarán los objetos y datos.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
4.  En el **elija el esquema de destino** cuadro de diálogo, puede examinar para la base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
5.  Cambia el destino en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que se está asignando es que no existe en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a continuación, se le pedirá con un mensaje **"la base de datos y/o esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De forma similar, se puede asignar el esquema al esquema que no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos que se creará durante la sincronización.  
  
-   Asignación de SQL Azure  
  
Puede asignar la base de datos de origen a la base de datos de SQL Azure de destino conectados o a cualquier esquema de la base de datos de SQL Azure de destino conectados. Si el esquema de origen se asignan a cualquier esquema que no existe en la base de datos de destino conectados, entonces se le pedirá con un mensaje **"esquema no existe en los metadatos de destino. Se crearán durante la sincronización. ¿Desea continuar? "** Haga clic en Sí.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de ASE y una [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquema de SQL Azure, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione cualquier fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea analizar la conversión de objetos de Sybase ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de SQL Azure, puede [crear un informe de conversión](http://msdn.microsoft.com/eb996b7c-1eef-4f73-b5e6-2fa6faf7336c). En caso contrario puede [convertir las definiciones de objeto de base de datos de ASE](http://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o definiciones de objetos de SQL Azure.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Sybase ASE a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
