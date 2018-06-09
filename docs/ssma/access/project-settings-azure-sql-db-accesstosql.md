---
title: Configuración (base de datos de SQL Azure) del proyecto (AccessToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 9d1666bf70cb07e616995dbd8f14fe4522cadc99
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774121"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>Configuración (base de datos de SQL Azure) del proyecto (AccessToSQL)
La configuración del proyecto de SQL Azure le permite configurar el sufijo de la base de datos de SQL Azure para agregar en el cuadro de diálogo de conexión y también permite implementar el mecanismo de latidos de conexión de SQL Azure.  
  
El panel de SQL Azure está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Utilice el cuadro de diálogo de configuración del proyecto para establecer las opciones de configuración para el proyecto actual. Para acceder a la configuración de SQL Azure, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
-   Utilice el cuadro de diálogo de configuración de proyecto predeterminada para establecer las opciones de configuración para todos los proyectos. Para acceder a la configuración de SQL Azure, en la **herramientas** menú, seleccione **DefaultProject configuración**, seleccione el tipo de proyecto como "SQL Azure" en **versión de destino de migración** cuadro combinado para tener acceso a la configuración en el panel de SQL Azure, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
## <a name="options"></a>Opciones  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo de latidos**  
  
Especifica un intervalo de tiempo que se usará para el mecanismo de latidos para mantener activa en la conexión de SQL Azure ' minutos: formato de segundo.  
  
**Valor predeterminado**:' 4:45 '  
  
El valor debe especificarse en estoy: formato de ss (por ejemplo, ' 4:45 ' o ' 0:50 ').  
  
**Sufijo del servidor de Azure SQL**  
  
Especifica el sufijo del servidor de SQL Azure  
  
**Valor predeterminado**: 'database.windows.net'.  
  
