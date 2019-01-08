---
title: Configuración del proyecto (Azure SQL DB) (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Project Settings dialog box, SQL Azure
- SQL Azure settings
ms.assetid: bbb8a204-d0e4-4f0b-9709-271feb1f136e
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2307a62c05503a231c3ee16b79efb25e964f55bd
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402130"
---
# <a name="project-settings-azure-sql-db-accesstosql"></a>Configuración del proyecto (Azure SQL DB) (AccessToSQL)
La configuración del proyecto de SQL Azure le permite configurar el sufijo de la base de datos de SQL Azure que desea agregar en el cuadro de diálogo de conexión y también permite implementar el mecanismo de latidos de conexión de SQL Azure.  
  
El panel de SQL Azure está disponible en el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo.  
  
-   Utilice el cuadro de diálogo de configuración del proyecto para establecer las opciones de configuración para el proyecto actual. Para obtener acceso a la configuración de SQL Azure, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y a continuación, seleccione **SQL Azure**.  
  
-   Utilice el cuadro de diálogo Configuración de proyecto predeterminada para establecer las opciones de configuración para todos los proyectos. Para obtener acceso a la configuración de SQL Azure, en el **herramientas** menú, seleccione **DefaultProject configuración**, seleccione el tipo de proyecto como "SQL Azure" en **versión de destino de migración** un cuadro combinado acceso a la configuración en el panel de SQL Azure, haga clic en **General** en la parte inferior del panel izquierdo y a continuación, seleccione **SQL Azure**.  
  
## <a name="options"></a>Opciones  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo de latidos**  
  
Especifica un intervalo de tiempo que se usará para el mecanismo de latidos para mantener activa en la conexión de SQL Azure "minutos: formato de segundos.  
  
**Valor predeterminado**:' 4:45 '  
  
El valor debe especificarse en estoy: formato de ss (por ejemplo, ' 4:45 ' o ' 0:50 ').  
  
**Sufijo del servidor de SQL Azure**  
  
Especifica el sufijo del servidor de SQL Azure  
  
**Valor predeterminado**: 'database.windows.net'.  
  
