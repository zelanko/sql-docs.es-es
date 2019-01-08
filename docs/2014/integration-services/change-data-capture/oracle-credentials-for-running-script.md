---
title: Credenciales de Oracle para ejecutar script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ca3f76c49b950f6830c4d60f011bbdb158055179
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796097"
---
# <a name="oracle-credentials-for-running-script"></a>Credenciales de Oracle para ejecutar script
  Para ejecutar el script de registro complementario de Oracle desde la consola del Diseñador CDC de Oracle, el programa le solicitará las credenciales del usuario de Oracle que está ejecutando el script. Para ejecutar este script, el usuario de Oracle debe tener el permiso ALTER TABLE para todas las tablas que se van a capturar y el permiso SELECT en la vista DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de tareas  
 Escriba lo siguiente en este cuadro de diálogo:  
  
 **Autenticación**  
  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**: Seleccione esta opción para usar las credenciales de dominio de Windows actuales. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: Si selecciona esta opción, debe escribir el **nombre de usuario** y **contraseña** para el usuario en la base de datos de Oracle de origen que se conecta.  
  
## <a name="see-also"></a>Vea también  
 [Cómo administrar una instancia CDC](manage-a-cdc-instance.md)   
 [Revisar y generar Scripts de registro complementario](review-and-generate-supplemental-logging-scripts.md)  
  
  
