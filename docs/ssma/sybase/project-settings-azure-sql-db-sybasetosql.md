---
title: Configuración del proyecto (Azure SQL DB) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 57002374-0d4d-43c1-b4e9-cbec02355a9c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 829e7b0c51cd341193944fb2f28241f48618c407
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176225"
---
# <a name="project-settings-azure-sql-db--sybasetosql"></a>Configuración del proyecto (Azure SQL DB ) (SybaseToSQL)
La configuración del proyecto de Azure SQL DB permite configurar el sufijo de base de datos de Azure SQL Database que se va a agregar en el cuadro de diálogo de conexión y también permitir la implementación del mecanismo de latido en la conexión de Azure SQL DB.  
  
El panel Azure SQL DB está disponible en los cuadros de diálogo **configuración del proyecto** y **configuración predeterminada del proyecto** .  
  
-   Utilice el cuadro de diálogo Configuración del proyecto para establecer las opciones de configuración del proyecto actual. Para acceder a la configuración de Azure SQL DB, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Azure SQL dB**.  
  
-   Utilice el cuadro de diálogo Configuración predeterminada del proyecto para establecer las opciones de configuración de todos los proyectos. Para acceder a la configuración de Azure SQL DB, en el menú **herramientas** , seleccione **configuración de DefaultProject**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, seleccione **Azure SQL dB**.  
  
## <a name="connectivity"></a>Conectividad  
**Intervalo entre latidos**  
  
Especifica un intervalo de tiempo que se va a usar para que el mecanismo de latido mantenga la conexión de Azure SQL DB activa en formato "minutos: segundos".  
  
**Valor predeterminado**: ' 4:45 '  
  
El valor debe especificarse en formato "m:SS" (por ejemplo, "4:45" o "0:50").  
  
**Sufijo del servidor de Azure SQL Database**  
  
Especifica un sufijo de servidor de Azure SQL Database.  
  
**Valor predeterminado**: ' Database.Windows.net '.  
  
