---
title: "Configuración (objetos del sistema de carga) del proyecto (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5cb5bdd526addeb11acf0553bbf022ff75415e70
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Configuración (objetos del sistema de carga) del proyecto (OracleToSQL)
La página cargar objetos de sistema de la **configuración del proyecto** cuadro de diálogo permite especificar qué objetos del sistema Oracle SSMA se convierte y se carga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
El panel de objetos del sistema de carga está disponible en la **configuración del proyecto** y **configuración de proyecto predeterminada** cuadros de diálogo:  
  
-   Para especificar la configuración para todos los proyectos SSMA, en la **herramientas** menú, seleccione **la configuración predeterminada del proyecto**, seleccione el tipo de proyecto de migración para el que se requiere para puede ver o cambiar de configuración **versión de destino de migración** desplegable haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **cargar objetos del sistema**.  
  
-   Para especificar la configuración para el proyecto actual, en la **herramientas** menú, seleccione **configuración del proyecto**, haga clic en **General** en la parte inferior del panel izquierdo y, a continuación, haga clic en **cargar objetos del sistema**.  
  
## <a name="default-settings"></a>Configuración predeterminada  
Convertir los objetos del sistema consume recursos del sistema y lleva tiempo. Para mejorar el rendimiento, SSMA selecciona sólo los objetos del sistema usados con más frecuencia, como se muestra en la lista siguiente:  
  
-   SYS. DBMS_OUTPUT  
  
-   SYS. DBMS_PIPE  
  
-   SYS. DBMS_UTILITY  
  
-   SYS. ESTÁNDAR  
  
-   SYS. UTL_FILE  
  
-   SYS. DBMS_LOB  
  
-   SYS. DBMS_SQL  
  
-   SYS. DBMS_SESSION  
  
Si los objetos de Oracle que hacen referencia a objetos del sistema adicionales, debe seleccionar los objetos. Si no selecciona los objetos del sistema que hacen referencia los objetos de base de datos de Oracle, SSMA va a notificar errores de conversión. Si recibe errores de conversión causados por falta de objetos del sistema, seleccione los objetos que faltan en este cuadro de diálogo. A continuación, puede repetir la conversión según sea necesario.  
  

