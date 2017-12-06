---
title: "Configuración de la migración de datos (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 688d9884b63ab1f4343bb3269250f0ab368500e3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="data-migration-settings-oracletosql"></a>Configuración de la migración de datos (OracleToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
**Configuración de la migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **opciones de migración de datos ampliado** está establecido en **mostrar** y se oculta cuando el valor está establecido en **ocultar** en configuración del proyecto. Para obtener más información acerca de la configuración del proyecto de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   Análisis de instrucciones SQL personalizada que se implementará en **configuración de la migración de datos** ficha del nodo de la tabla.  
  
-   Siguientes son las dos casillas de verificación disponibles en la **configuración de la migración de datos** especialmente.:  
  
    1.  Puede truncar la tabla de SQL Server  
  
    2.  Seleccione uso personalizado  
  
1.  **Puede truncar la tabla de SQL Server:**  
     Esta opción permite al usuario tener una visión clara de los datos migrados en la base de datos de destino.  
  
    -   De forma predeterminada, este cuadro de texto está activada.  
  
    -   Si este cuadro de texto no está activada, los datos que se migren se agregará a los datos existentes en la base de datos de destino.  
  
2.  **Seleccione uso personalizado:**  
     Esta opción permite al usuario modificar el **seleccione** instrucción presente (**seleccione** instrucción permite a los usuarios seleccionar los datos que se mostrará en la base de datos de destino).  
  
    1.  De forma predeterminada, este cuadro de texto está desactivada.  
  
    2.  Si se activa este cuadro de texto, que permite a los usuarios modificar la **seleccione** instrucción está presente.  
  
Hay dos botones presentes lleve.:  
  
-   **Aplicar:** haga clic en **aplicar** para aplicar la configuración que se han cambiado.  
  
-   **Cancelar:** haga clic en **cancelar** para restaurar la configuración está presente antes de que se realizaron los cambios.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de Oracle a SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
