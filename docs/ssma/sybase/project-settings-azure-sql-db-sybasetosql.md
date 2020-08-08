---
title: Configuración del proyecto (Azure SQL Database) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b79d4e94126676e128d803176463b314348ed8a1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930926"
---
# <a name="project-settings-azure-sql-database--sybasetosql"></a>Configuración del proyecto (Azure SQL Database) (SybaseToSQL)
La configuración del proyecto Azure SQL Database permite configurar el sufijo de la base de datos Azure SQL Database que se va a agregar en el cuadro de diálogo de conexión y también permitir la implementación del mecanismo de latido en Azure SQL Database conexión.  
  
El panel Azure SQL Database está disponible en los cuadros de diálogo **configuración del proyecto** y **configuración predeterminada del proyecto** .  
  
-   Utilice el cuadro de diálogo Configuración del proyecto para establecer las opciones de configuración del proyecto actual. Para obtener acceso a la configuración de Azure SQL Database, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Azure SQL Database**.  
  
-   Utilice el cuadro de diálogo Configuración predeterminada del proyecto para establecer las opciones de configuración de todos los proyectos. Para obtener acceso a la configuración de Azure SQL Database, en el menú **herramientas** , seleccione **configuración de DefaultProject**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Azure SQL Database**.  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo entre latidos**  
  
Especifica un intervalo de tiempo que se va a usar para que el mecanismo de latido mantenga el Azure SQL Database conexión activa en formato "minutos: segundos".  
  
**Valor predeterminado**: ' 4:45 '  
  
El valor debe especificarse en formato "m:SS" (por ejemplo, "4:45" o "0:50").  
  
**Sufijo de servidor Azure SQL Database**  
  
Especifica un sufijo de servidor Azure SQL Database  
  
**Valor predeterminado**: ' Database.Windows.net '.  
  
