---
title: Configuración de migración de datos (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 90f76ef4d52fd5a1b7ed04d268954d0fed756324
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183070"
---
# <a name="data-migration-settings-mysqltosql"></a>Configuración de la migración de datos (MySQLToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
**Configuración de la migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **opciones de migración de datos ampliado** está establecido en **mostrar** y se oculta cuando el valor se establece en **ocultar** en configuración del proyecto. Para obtener más información acerca de la configuración del proyecto de migración, consulte [configuración del proyecto (migración)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) .  
  
-   Análisis de instrucciones SQL personalizada que se implementará en **configuración de migración de datos** ficha del nodo de la tabla.  
  
-   Estos son las dos casillas de verificación disponibles en el **configuración de migración de datos** viz.:  
  
    1.  Truncar la tabla de SQL Server  
  
    2.  Seleccione uso personalizado  
  
1.  **Puede truncar la tabla de SQL Server:**  
     Esta opción permite al usuario que tiene una visión clara de los datos migrados en la base de datos de destino.  
  
    -   De forma predeterminada, este cuadro de texto está activada.  
  
    -   Si este cuadro de texto está desactivada, se agregarán los datos que se migren a los datos existentes en la base de datos de destino.  
  
2.  **Seleccione uso personalizado:**  
     Esta opción permite al usuario modificar el **seleccione** instrucción presente (**seleccione** instrucción permite a los usuarios seleccionar los datos que se muestra en la base de datos de destino).  
  
    1.  De forma predeterminada, este cuadro de texto está desactivada.  
  
    2.  Si este cuadro de texto está activada, permite a los usuarios modificar la **seleccione** instrucción presente.  
  
Hay dos botones que presentes viz.:  
  
-   **Se aplican:** Haga clic en **aplicar** para aplicar la configuración que han cambiado.  
  
-   **Cancelar:** Haga clic en **cancelar** para restaurar los valores de configuración antes de que se realizan los cambios.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de MySQL a SQL Server o SQL Azure](https://msdn.microsoft.com/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  
