---
title: Configuración del proyecto (Azure SQL Database) (AccessToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3dd47039f6bbfaa15eb16776487191a66a17db59
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937584"
---
# <a name="project-settings-azure-sql-database-accesstosql"></a>Configuración del proyecto (Azure SQL Database) (AccessToSQL)
La configuración del proyecto SQL Azure permite configurar el sufijo de Azure SQL Database que se va a agregar en el cuadro de diálogo de conexión y permitir también la implementación del mecanismo de latido en SQL Azure conexión.  
  
El panel SQL Azure está disponible en los cuadros de diálogo **configuración del proyecto** y **configuración predeterminada del proyecto** .  
  
-   Utilice el cuadro de diálogo Configuración del proyecto para establecer las opciones de configuración del proyecto actual. Para obtener acceso a la configuración de SQL Azure, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
-   Utilice el cuadro de diálogo Configuración predeterminada del proyecto para establecer las opciones de configuración de todos los proyectos. Para obtener acceso a la configuración de SQL Azure, en el menú **herramientas** , seleccione **configuración de DefaultProject**, seleccione el tipo de proyecto como "SQL Azure" en el cuadro combinado versión de **destino de migración** para acceder a la configuración en el panel SQL Azure, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
## <a name="options"></a>Opciones  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo entre latidos**  
  
Especifica un intervalo de tiempo que se va a usar para que el mecanismo de latido mantenga el SQL Azure conexión activa en formato "minutos: segundos".  
  
**Valor predeterminado**: ' 4:45 '  
  
El valor debe especificarse en formato "m:SS" (por ejemplo, "4:45" o "0:50").  
  
**Sufijo de servidor SQL Azure**  
  
Especifica el sufijo del servidor SQL Azure  
  
**Valor predeterminado**: ' Database.Windows.net '.  
  
