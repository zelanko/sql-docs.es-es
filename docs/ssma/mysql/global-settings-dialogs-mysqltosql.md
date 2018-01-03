---
title: "Configuración global (cuadros de diálogo) (MySQLToSQL) | Documentos de Microsoft"
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
ms.assetid: 6df20fbb-e92d-475f-a94d-aaf70b06eb9b
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d82e6356eca662a09c75f30e0d346a667d6d2343
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="global-settings-dialogs-mysqltosql"></a>Configuración global (cuadros de diálogo) (MySQLToSQL)
Use la página de los cuadros de diálogo de la **configuración Global** cuadro de diálogo para especificar la acción predeterminada del usuario y la configuración de advertencia de SSMA.  
  
Para acceder a la configuración del cuadro de diálogo en el **herramientas** menú, seleccione **configuración Global**, haga clic en **GUI** en la parte inferior del panel izquierdo y, a continuación, seleccione **cuadros de diálogo**.  
  
## <a name="options"></a>.  
**Advertir antes de sobrescribir objetos**  
Cuando SSMA convierte los objetos en SQL Server, es podrán que algunos objetos ya existan en los metadatos del proyecto SQL Server. Estos objetos pueden ya convertidos a o los objetos simplemente pueden tener el mismo nombre en el esquema de destino como objetos que se va a convertir.  
  
Utilice esta opción para especificar si SSMA le pedirá que sobrescriba las definiciones de objeto duplicados:  
  
-   Si selecciona **True**, SSMA mostrará un cuadro de diálogo de advertencia cuando encuentra un objeto duplicado. En este cuadro de diálogo, puede especificar para sobrescribir los objetos individuales o todos los objetos duplicados u omitir los objetos individuales o todos los objetos duplicados.  
  
-   Si selecciona **False**, **acción predeterminada de sobrescritura de objeto** opción aparece donde especificar la acción predeterminada.  
  
**Acción predeterminada de sobrescritura de objeto**  
Esta opción aparece si selecciona **False** para el **Avisar antes de sobrescribir objetos** opción.  
  
Utilice esta opción para especificar el comportamiento de sobrescritura de objeto predeterminado:  
  
-   Si selecciona **True**, SSMA sobrescribirá automáticamente los objetos en los metadatos de proyecto de SQL Server que tienen el mismo nombre y están en el mismo esquema de destino que el objeto que se va a convertir.  
  
-   Si selecciona **False**, SSMA no sobrescribe los metadatos del objeto durante la conversión.  
  
