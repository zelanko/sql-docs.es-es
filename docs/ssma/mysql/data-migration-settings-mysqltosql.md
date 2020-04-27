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
ms.openlocfilehash: c2c903ef29ab1a103bc9aa4f7b061e83ee7f2a95
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67896370"
---
# <a name="data-migration-settings-mysqltosql"></a>Configuración de la migración de datos (MySQLToSQL)
  
## <a name="data-migration-settings"></a>Configuración de la migración de datos  
La **configuración de migración de datos** permite al usuario escribir consultas personalizadas para la migración de datos.  
  
-   Esta pestaña está disponible cuando **Opciones de migración de datos extendidos** está establecida en **Mostrar** y está oculta cuando el valor está establecido en **ocultar** en la configuración del proyecto. Para obtener más información sobre la configuración de la migración de proyectos, vea [configuración del proyecto (migración)](https://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) .  
  
-   El análisis de instrucciones SQL personalizadas se implementará en la pestaña **configuración de migración de datos** del nodo de tabla.  
  
-   A continuación se muestran las dos casillas disponibles en la **configuración de migración de datos** , es decir:  
  
    1.  Truncar SQL Server tabla  
  
    2.  Usar selección personalizada  
  
1.  **Truncar SQL Server tabla:**  
     Esta opción permite que el usuario tenga una vista clara de los datos migrados en la base de datos de destino.  
  
    -   De forma predeterminada, este cuadro de texto está activado.  
  
    -   Si este cuadro de texto está desactivado, los datos migrados se agregarán a los datos existentes en la base de datos de destino.  
  
2.  **Usar selección personalizada:**  
     Esta opción permite al usuario modificar la instrucción **Select** (la instrucción**Select** permite a los usuarios seleccionar los datos que se van a mostrar en la base de datos de destino).  
  
    1.  De forma predeterminada, este cuadro de texto está desactivado.  
  
    2.  Si este cuadro de texto está activado, permite a los usuarios modificar la instrucción **Select** .  
  
Hay dos botones presentes:  
  
-   **Aplicar:** Haga clic en **aplicar** para aplicar la configuración que ha cambiado.  
  
-   **Cancelar:** Haga clic en **Cancelar** para restaurar la configuración presente antes de que se realizaran los cambios.  
  
## <a name="see-also"></a>Consulte también  
[Migración de datos de MySQL a SQL Server/SQL Azure](https://msdn.microsoft.com/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  
