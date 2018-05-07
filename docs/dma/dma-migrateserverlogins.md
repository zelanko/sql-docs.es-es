---
title: Migración de inicios de sesión de SQL Server (Asistente de migración de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 23da8fe364ffad914013719f54871e85213befc5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>Migrar los inicios de sesión de SQL Server mediante el Asistente de migración de datos

Este artículo proporciona información general de migración los inicios de sesión de SQL Server mediante el Asistente de migración de datos. 

## <a name="key-concepts"></a>Conceptos clave
Éstos son los conceptos clave.

- Puede migrar los inicios de sesión en función de una entidad de seguridad de Windows (por ejemplo, un usuario de dominio o un grupo de dominio de Windows). También puede migrar los inicios de sesión que se crea basándose en la autenticación de SQL, también denominada inicios de sesión de SQL Server.

- Asistente para migración de datos no admite actualmente los inicios de sesión asociados con un certificado de seguridad independiente (inicios de sesión asignados a certificado), una clave asimétrica independiente (inicios de sesión asignados a clave asimétrica) y los inicios de sesión asignados a las credenciales.

- Asistente para migración de datos no mover el **sa** principios de inicio de sesión y servidor con nombres incluidos entre signos de número dobles (\#\#), que son solo para uso interno.

- De forma predeterminada, Assistatn de migración de datos selecciona todos los inicios de sesión completos para migrar. Si lo desea, puede seleccionar inicios de sesión específicos para migrar. Cuando el Asistente de migración de datos se migra todos los inicios de sesión completos, la asignación de usuario de inicio de sesión permanece intacta en las bases de datos que se han migrado. 

  Si planea migrar inicios de sesión específicos, asegúrese de seleccionar los inicios de sesión que están asignados a uno o más usuarios en las bases de datos seleccionados para la migración.

- Como parte de la migración de inicio de sesión, el Asistente de migración de datos también mueve los roles de servidor definido por el usuario y permisos de nivel de servidor se agrega a los roles de servidor definidos por el usuario. El propietario del rol se establecerá en **sa** principal.

- Como parte de la migración de inicio de sesión, el Asistente de migración de datos asigna los permisos a los elementos protegibles en el destino de SQL Server tal como aparecen en el origen de SQL Server. 

  Si el inicio de sesión ya existe en el destino de SQL Server, el Asistente de migración de datos migra solo los permisos asignados a los elementos protegibles y no se volverá a crear el inicio de sesión completo.

- Asistente para migración de datos hace que el esfuerzo para asignar el inicio de sesión a los usuarios de base de datos si el inicio de sesión ya existe en el servidor de destino.

- Se recomienda que revise los resultados de la migración para entender el estado general de la migración de inicio de sesión y las acciones posteriores a la migración recomendadas.

## <a name="resources"></a>Recursos

[Asistente de migración de datos (DMA)](../dma/dma-overview.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
