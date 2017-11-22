---
title: "Asignación de esquemas de DB2 a esquemas SQL Server (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e422c99f45b5da02214aee96bb0520dc8c851e74
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>Asignación de esquemas de DB2 a esquemas SQL Server (DB2ToSQL)
En DB2, cada base de datos tiene uno o más esquemas. De forma predeterminada, SSMA migra todos los objetos en un esquema de DB2 a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con el nombre para el esquema de la base de datos. Sin embargo, puede personalizar la asignación entre esquemas de DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] las bases de datos.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 y esquemas SQL Server  
Una base de datos de DB2 contiene esquemas. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contiene varias bases de datos, cada uno de los cuales puede tener varios esquemas.  
  
El concepto de DB2 de un esquema se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] concepto de una base de datos y uno de sus esquemas. Por ejemplo, DB2 podría tener un esquema denominado **HR**. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] podría tener una base de datos denominada **HR**, y dentro de esa base de datos son esquemas. Un esquema es el **dbo** (o el propietario de la base de datos) esquema. De forma predeterminada, el esquema de DB2 **HR** va a asignar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos y esquema **HR.dbo**. SSMA hace referencia a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinación de base de datos y el esquema como un esquema.  
  
Puede modificar la asignación entre DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, puede asignar un esquema de DB2 a disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de DB2, seleccione **esquemas**.  
  
    El **esquema de asignación** ficha también está disponible cuando se selecciona una base de datos individual, el **esquemas** carpeta o esquemas individuales. La lista en la **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todos los esquemas de DB2, seguido por un valor de destino. Este destino se indica en la notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde se migrarán los objetos y datos.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
    En el **elegir el esquema de destino** cuadro de diálogo, puede buscar base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
4.  El destino se cambia en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que va a asignar es no existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a continuación, se le pedirá con un mensaje **"la base de datos o el esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De igual forma, se puede asignar el esquema al esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos que se creará durante la sincronización.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de DB2 y un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione una fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Pasos siguientes  
Si desea analizar la conversión de objetos de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, también puede [informe de migración de datos (SSMA común)](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Vea también  
[Conectarse a SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Migrar bases de datos de DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
