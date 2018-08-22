---
title: Configuración (cargar objetos del sistema) del proyecto (DB2ToSQL) | Microsoft Docs
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
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 3b2398732bc920b926a3db3352eacca6e39f7399
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396153"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Configuración (cargar objetos del sistema) del proyecto (DB2ToSQL)
La página cargar objetos del sistema de la **configuración del proyecto** cuadro de diálogo le permite especificar qué objetos del sistema DB2 SSMA convierte y se carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Está disponible en el panel de objetos del sistema al cargar el **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Para especificar la configuración para todos los proyectos SSMA, en el **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que la configuración es necesaria para ver o cambiar de **Versión de destino de migración** desplegable clic **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **cargar objetos del sistema**.  
  
-   Para especificar la configuración para el proyecto actual, en el **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **Al cargar los objetos del sistema**.  
  
## <a name="default-settings"></a>Configuración predeterminada  
Convertir los objetos del sistema consume recursos del sistema y lleva tiempo. Para mejorar el rendimiento, SSMA selecciona sólo los objetos del sistema utilizadas con frecuencia, como se muestra en la lista siguiente:  
  
-   SYS. DBMS_OUTPUT  
  
-   SYS. DBMS_PIPE  
  
-   SYS. DBMS_UTILITY  
  
-   SYS. ESTÁNDAR  
  
-   SYS. UTL_FILE  
  
-   SYS.DBMS_LOB  
  
-   SYS.DBMS_SQL  
  
-   SYS. DBMS_SESSION  
  
Si los objetos de DB2 que hacen referencia a objetos del sistema adicionales, debe seleccionar esos objetos. Si no selecciona los objetos del sistema que hacen referencia los objetos de base de datos de DB2, SSMA va a notificar errores de conversión. Si recibe errores de conversión que se debe a que faltan los objetos del sistema, seleccione los objetos que faltan en este cuadro de diálogo. A continuación, puede repetir la conversión según sea necesario.  
  
