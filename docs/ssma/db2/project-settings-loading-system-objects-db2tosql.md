---
title: Configuración del proyecto (cargar objetos del sistema) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9a545233-1b0a-488a-a1ec-c33aa608dcc1
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5c12a2ddb97c6d599e5adfc57277e0a5f64288e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68060194"
---
# <a name="project-settingsloading-system-objects-db2tosql"></a>Configuración del proyecto (cargar objetos del sistema) (DB2ToSQL)
La página cargando objetos del sistema del cuadro de diálogo **configuración del proyecto** le permite especificar qué objetos del sistema DB2 SSMA convierte y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carga en.  
  
El panel cargando objetos del sistema está disponible en los cuadros de diálogo Configuración del **proyecto** y **configuración predeterminada del proyecto** :  
  
-   Para especificar la configuración de todos los proyectos de SSMA, en el menú **herramientas** , seleccione **configuración predeterminada del proyecto**, seleccione tipo de proyecto de migración para el que se deben ver o cambiar las opciones de configuración en la lista desplegable de la **versión de destino** de la migración, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **cargar objetos del sistema**.  
  
-   Para especificar la configuración del proyecto actual, en el menú **herramientas** , seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **cargar objetos del sistema**.  
  
## <a name="default-settings"></a>Configuración predeterminada  
La conversión de objetos del sistema consume recursos del sistema y lleva tiempo. Para mejorar el rendimiento, SSMA selecciona solo los objetos del sistema que se usan con más frecuencia, como se muestra en la lista siguiente:  
  
-   Sist. DBMS_OUTPUT  
  
-   Sist. DBMS_PIPE  
  
-   Sist. DBMS_UTILITY  
  
-   Sist. NORMAL  
  
-   Sist. UTL_FILE  
  
-   Sist. DBMS_LOB  
  
-   Sist. DBMS_SQL  
  
-   Sist. DBMS_SESSION  
  
Si los objetos DB2 hacen referencia a objetos del sistema adicionales, debe seleccionar esos objetos. Si no selecciona los objetos del sistema a los que hacen referencia los objetos de base de datos de DB2, SSMA notificará los errores de conversión. Si recibe errores de conversión causados por objetos del sistema que faltan, seleccione los objetos que faltan en este cuadro de diálogo. Después, puede repetir la conversión según sea necesario.  
  
