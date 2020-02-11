---
title: Conectar con el servidor (página Parámetros de conexión adicionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e92fbb8bc29aed54e43925a0670d9a365388df62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62808686"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>Conectar con el servidor (página Parámetros de conexión adicionales)
  El cuadro de diálogo **Conectar con** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] presenta los valores de cadena de conexión más comunes como opciones. Utilice la página **Parámetros de conexión adicionales** para agregar más parámetros de conexión a la cadena de conexión.  
  
-   Los parámetros de conexión adicionales pueden ser cualquier parámetro de conexión ODBC.  
  
-   Los parámetros de conexión adicionales se deberían agregar con el formato **;parameter1=value1;parameter2=value2**.  
  
-   Los parámetros que se agregan utilizando la página **Parámetros de conexión adicionales** se agregan a los parámetros seleccionados utilizando las opciones del cuadro de diálogo **Conectar a** .  
  
-   La última instancia de cada parámetro proporcionado invalida cualquier instancia anterior del mismo. Los parámetros que se agregan con la página **Parámetros de conexión adicionales** siguen y reemplazan a los parámetros proporcionados en las pestañas **Inicio de sesión** o **Propiedades de conexión** . Por ejemplo, si la pestaña **Inicio de sesión** proporciona **SERVER1** como **Nombre del servidor**y la página **Parámetros de conexión adicionales** contiene **;SERVER=SERVER2**, la conexión se realizará a **SERVER2**.  
  
-   Los parámetros que se agregan utilizando la página **Parámetros de conexión adicionales** siempre se pasan como texto simple.  
  
    > [!IMPORTANT]  
    >  No incluya credenciales de inicio de sesión y contraseñas en la página **Parámetros de conexión adicionales** . No se cifrarán cuando se pasen a través de la red. En su lugar, use la pestaña **Inicio de sesión** .  
  
## <a name="task-list"></a>Lista de tareas  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>Para mostrar la página Parámetros de conexión adicionales  
  
1.  En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], en el menú **Consulta** , seleccione **Conexión**y haga clic en **Conectar**.  
  
2.  En el cuadro de diálogo **Conectar a** , haga clic en **Opciones**y en la pestaña **Parámetros de conexión adicionales** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="example-a-connecting-to-the-database-engine"></a>Ejemplo A: conectarse al motor de base de datos  
 Para conectarse a la base de datos [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] en un servidor denominado ACCOUNTING, escriba lo siguiente en la página **Parámetros de conexión adicionales** :  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>Ejemplo B: conectarse a Analysis Services  
 Para conectarse a Analysis Services, hacer que todas las particiones que escuchan las notificaciones se consulten en tiempo real (omitiendo el almacenamiento en memoria caché) y establecer el valor de tiempo de espera de reescritura en 5, escriba lo siguiente en la página **Parámetros de conexión adicionales** :  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
