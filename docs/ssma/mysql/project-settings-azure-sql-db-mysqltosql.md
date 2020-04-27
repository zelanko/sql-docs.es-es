---
title: Configuración del proyecto (Azure SQL DB) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8c06420a-533b-4de0-948d-a0c6b368c544
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e4cf080d7a3bcb2d121a58a57be9f3fd41a4c18a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908818"
---
# <a name="project-settings-azure-sql-db-mysqltosql"></a>Configuración del proyecto (Azure SQL DB) (MySQLToSQL)
La configuración del proyecto SQL Azure permite configurar el sufijo de la base de datos SQL Azure que se va a agregar en el cuadro de diálogo de conexión y también permitir la implementación del mecanismo de latido en SQL Azure conexión.  
  
El panel SQL Azure está disponible en los cuadros de diálogo **configuración del proyecto** y **configuración predeterminada del proyecto** .  
  
-   Utilice el cuadro de diálogo Configuración del proyecto para establecer las opciones de configuración del proyecto actual. Para obtener acceso a la configuración de SQL Azure, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
-   Utilice el cuadro de diálogo Configuración predeterminada del proyecto para establecer las opciones de configuración de todos los proyectos. Para obtener acceso a la configuración de SQL Azure, en el menú **herramientas** , seleccione **configuración de DefaultProject**, seleccione tipo de proyecto de migración como SQL Azure de la lista desplegable de versiones de **destino de migración** para acceder a la configuración en SQL Azure panel, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **SQL Azure**.  
  
## <a name="options"></a>Opciones  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo entre latidos**  
  
Especifica un intervalo de tiempo que se va a usar para que el mecanismo de latido mantenga el SQL Azure conexión activa en formato "minutos: segundos".  
  
**Valor predeterminado**: ' 4:45 '  
  
El valor debe especificarse en formato "m:SS" (por ejemplo, "4:45" o "0:50").  
  
**Sufijo de servidor SQL Azure**  
  
Especifica el sufijo del servidor SQL Azure  
  
**Valor predeterminado**: ' Database.Windows.net '.  
  
