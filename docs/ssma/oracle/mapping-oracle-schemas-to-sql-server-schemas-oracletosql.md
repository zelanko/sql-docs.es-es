---
title: "Asignación de esquemas de Oracle a esquemas SQL Server (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: On Demand
ms.openlocfilehash: 025f3f049b5efccb83e13d5baebacbe8b0fa2a1c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Asignación de esquemas de Oracle a esquemas SQL Server (OracleToSQL)
En Oracle, cada base de datos tiene uno o más esquemas. De forma predeterminada, SSMA migra todos los objetos en un esquema de Oracle para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con el nombre para el esquema de la base de datos. Sin embargo, puede personalizar la asignación entre esquemas de Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] las bases de datos.  
  
## <a name="oracle-and-sql-server-schemas"></a>Esquemas SQL Server y Oracle  
Una base de datos de Oracle contiene esquemas. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] contiene varias bases de datos, cada uno de los cuales puede tener varios esquemas.  
  
El concepto de Oracle de un esquema se asigna a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] concepto de una base de datos y uno de sus esquemas. Por ejemplo, Oracle podría tener un esquema denominado **HR**. Una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] podría tener una base de datos denominada **HR**, y dentro de esa base de datos son esquemas. Un esquema es el **dbo** (o el propietario de la base de datos) esquema. De forma predeterminada, el esquema de Oracle **HR** va a asignar la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos y esquema **HR.dbo**. SSMA hace referencia a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] combinación de base de datos y el esquema como un esquema.  
  
Puede modificar la asignación entre Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modificación de la base de datos de destino y el esquema  
En SSMA, puede asignar un esquema de Oracle a disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema.  
  
**Para modificar la base de datos y esquema**  
  
1.  En el Explorador de metadatos de Oracle, seleccione **esquemas**.  
  
    El **esquema de asignación** ficha también está disponible cuando se selecciona una base de datos individual, el **esquemas** carpeta o esquemas individuales. La lista en la **esquema de asignación** ficha se personaliza para el objeto seleccionado.  
  
2.  En el panel derecho, haga clic en el **esquema de asignación** ficha.  
  
    Verá una lista de todos los esquemas de Oracle, seguido por un valor de destino. Este destino se indica en la notación de dos partes (*database.schema*) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] donde se migrarán los objetos y datos.  
  
3.  Seleccione la fila que contiene la asignación que desea cambiar y, a continuación, haga clic en **modificar**.  
  
    En el **elegir el esquema de destino** cuadro de diálogo, puede buscar base de datos de destino disponibles y el esquema o el tipo de la base de datos y el esquema de nombre en el cuadro de texto en una notación de dos partes (database.schema) y, a continuación, haga clic en **Aceptar**.  
  
4.  El destino se cambia en el **esquema de asignación** ficha.  
  
**Modos de asignación**  
  
-   Asignar a SQL Server  
  
Base de datos de origen se puede asignar a cualquier base de datos de destino. De forma predeterminada se asigna la base de datos de origen a destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos con el que se ha conectado con SSMA. Si la base de datos de destino que va a asignar es no existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], a continuación, se le pedirá con un mensaje **"la base de datos o el esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] metadatos. Se crearán durante la sincronización. ¿Desea continuar?"** Haga clic en Sí. De igual forma, se puede asignar el esquema al esquema no existe en el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos que se creará durante la sincronización.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Revertir a la base de datos predeterminada y el esquema  
Si personaliza la asignación entre un esquema de Oracle y un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquema, puede revertir la asignación a los valores predeterminados.  
  
**Para revertir a la base de datos predeterminada y el esquema**  
  
1.  En la pestaña asignación de esquema, seleccione una fila y haga clic en **Restablecer valores predeterminados** para revertir a la base de datos predeterminada y el esquema.  
  
## <a name="next-steps"></a>Next Steps  
Si desea analizar la conversión de objetos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos, también puede [crear un informe de conversión](http://msdn.microsoft.com/en-us/4de9bcf6-1346-4740-87f9-7f24a8226357). En caso contrario, puede [convertir las definiciones de objeto de base de datos de Oracle](http://msdn.microsoft.com/en-us/e021182d-31da-443d-b110-937f5db27272) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definiciones de objetos.  
  
## <a name="see-also"></a>Vea también  
[Conectarse a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
