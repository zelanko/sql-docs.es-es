---
title: Configuración de migración de datos (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c331f396f43534387803e71a22bd636c0d3d767c
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984237"
---
# <a name="data-migration-settings-sybasetosql"></a>Configuración de migración de datos (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
**Configuración de la migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **opciones de migración de datos ampliado** está establecido en **mostrar** y se oculta cuando el valor se establece en **ocultar** en configuración del proyecto. Para obtener más información acerca de la configuración del proyecto de migración, consulte [configuración del proyecto (migración)](http://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
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
  
-   **Aplicar:** haga clic en **aplicar** para aplicar la configuración que han cambiado.  
  
-   **Cancelar:** haga clic en **cancelar** para restaurar los valores de configuración antes de que se realizan los cambios.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de Sybase a SQL Server o SQL Azure](http://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
