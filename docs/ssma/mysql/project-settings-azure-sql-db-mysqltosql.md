---
title: "Configuración (base de datos de SQL Azure) del proyecto (MySQLToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
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
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a71ecfe91f04e45382ac6ab9f1ec3aa18dd64d04
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Configuración (base de datos de SQL Azure) del proyecto (MySQLToSQL)
La configuración del proyecto de SQL Azure le permite configurar el sufijo de la base de datos de SQL Azure para agregar en el cuadro de diálogo de conexión y también permite implementar el mecanismo de latidos de conexión de SQL Azure.  
  
El panel de SQL Azure está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Utilice el cuadro de diálogo de configuración del proyecto para establecer las opciones de configuración para el proyecto actual. Para acceder a la configuración de SQL Azure, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
-   Utilice el cuadro de diálogo de configuración de proyecto predeterminada para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de SQL Azure, en la **herramientas** menú, seleccione **DefaultProject configuración**, seleccione el tipo de proyecto de migración como SQL Azure desde **versión de destino de migración** de lista desplegable para acceder a la configuración en el panel de SQL Azure, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
## <a name="options"></a>.  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo de latidos**  
  
Especifica un intervalo de tiempo que se usará para el mecanismo de latidos para mantener activa en la conexión de SQL Azure ' minutos: formato de segundo.  
  
**Valor predeterminado**:' 4:45 '  
  
El valor debe especificarse en estoy: formato de ss (por ejemplo, ' 4:45 ' o ' 0:50 ').  
  
**Sufijo del servidor de Azure SQL**  
  
Especifica el sufijo del servidor de SQL Azure  
  
**Valor predeterminado**: 'database.windows.net'.  
  
