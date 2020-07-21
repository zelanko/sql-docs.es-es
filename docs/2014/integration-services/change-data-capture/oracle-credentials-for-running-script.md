---
title: Credenciales de Oracle para ejecutar script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 683b313e5b1065c3709c4637ddf968641612cc0b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438562"
---
# <a name="oracle-credentials-for-running-script"></a>Credenciales de Oracle para ejecutar script
  Para ejecutar el script de registro complementario de Oracle desde la consola del Diseñador CDC de Oracle, el programa le solicitará las credenciales del usuario de Oracle que está ejecutando el script. Para ejecutar este script, el usuario de Oracle debe tener el permiso ALTER TABLE para todas las tablas que se van a capturar y el permiso SELECT en la vista DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de tareas  
 Escriba lo siguiente en este cuadro de diálogo:  
  
 **Autenticación**  
  
 Seleccione uno de los siguientes:  
  
-   **Autenticación de Windows**: seleccione esta opción para usar las credenciales del dominio de Windows actual. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: si selecciona esta opción, debe escribir el **Nombre de usuario** y la **Contraseña** para el usuario en la base de datos de Oracle de origen a la que se está conectando.  
  
## <a name="see-also"></a>Consulte también  
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [Revisar y generar Scripts de registro complementario](review-and-generate-supplemental-logging-scripts.md)  
  
  
