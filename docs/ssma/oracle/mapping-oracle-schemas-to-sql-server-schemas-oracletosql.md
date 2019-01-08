---
title: Asignación de esquemas de Oracle a esquemas de SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 61b706145f708e9b2e8a04ba4e7bc574c503a742
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407890"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Asignación de esquemas de Oracle a esquemas de SQL Server (OracleToSQL)
En Oracle, cada base de datos tiene uno o varios esquemas. De forma predeterminada, SSMA migra todos los objetos en un esquema de Oracle para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominado para el esquema de base de datos. Sin embargo, puede personalizar la asignación entre esquemas de Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
## <a name="oracle-and-sql-server-schemas"></a>Esquemas de SQL Server y Oracle  
Una base de datos de Oracle contiene esquemas. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene varias bases de datos, cada uno de los cuales puede tener varios esquemas.  
  
El concepto de Oracle de un esquema se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concepto de una base de datos y uno de sus esquemas. Por ejemplo, Oracle podría tener un esquema denominado **HR**. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría tener una base de datos denominada **HR**, y dentro de esa base de datos son los esquemas. Un esquema es el **dbo** (o el propietario de la base de datos) esquema. De forma predeterminada, el esquema de Oracle **HR** se asignará a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos y esquema **HR.dbo**. SSMA se refiere a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinación de la base de datos y el esquema como un esquema.  
  
Puede modificar la asignación entre Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, se puede asignar un esquema de Oracle que haya disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de Oracle, seleccione **esquemas**.  
  
    El **esquema de asignación** ficha también está disponible cuando se selecciona una base de datos individual, el **esquemas** carpeta o esquemas individuales. La lista en el **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todos los esquemas de Oracle, seguido por un valor de destino. Este destino se indica en una notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se migrarán los objetos y datos.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
    En el **elija el esquema de destino** cuadro de diálogo, puede examinar para la base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
4.  Cambia el destino en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que se está asignando es que no existe en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a continuación, se le pedirá con un mensaje **"la base de datos y/o esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De forma similar, se puede asignar el esquema al esquema que no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos que se creará durante la sincronización.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de Oracle y un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione cualquier fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea analizar la conversión de los objetos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos, puede [crear un informe de conversión](assessing-oracle-schemas-for-conversion-oracletosql.md). En caso contrario puede [convertir las definiciones de objeto de base de datos de Oracle](converting-oracle-schemas-oracletosql.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiciones de objetos.  
  
## <a name="see-also"></a>Vea también  
[Conectarse a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Bases de datos de migración de Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
