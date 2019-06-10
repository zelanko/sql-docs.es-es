---
title: Migrar los inicios de sesión de SQL Server con Data Migration Assistant | Microsoft Docs
description: Obtenga información sobre cómo migrar los inicios de sesión de SQL Server con Data Migration Assistant
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: jroth
ms.openlocfilehash: 25e60b4c51e6a4a5ac38a1b7f0e3268a0cee3e3b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794334"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Migrar los inicios de sesión de SQL Server con Data Migration Assistant

En este artículo se proporciona información general de migrar los inicios de sesión de SQL Server mediante Data Migration Assistant. 

## <a name="which-logins-are-migrated"></a>Se migran los inicios de sesión

- Puede migrar los inicios de sesión basados en una entidad de seguridad de Windows (por ejemplo, un usuario de dominio o un grupo de dominio de Windows). También puede migrar los inicios de sesión que se crean en función de la autenticación de SQL, también denominada inicios de sesión de SQL Server.

- Asistente para migración de datos no admite actualmente los inicios de sesión asociados con un certificado de seguridad independiente (inicios de sesión asignados a certificado), una clave asimétrica independiente (inicios de sesión asignados a clave asimétrica) y los inicios de sesión asignados a las credenciales.

- Asistente para migración de datos no mover el **sa** principios de inicio de sesión y servidor con nombres incluidos entre signos de número dobles (\#\#), que son solo para uso interno.

- De forma predeterminada, Data Migration Assistant selecciona todos los inicios de sesión completos para migrar. Si lo desea, puede seleccionar inicios de sesión específicos para migrar. Cuando Data Migration Assistant migra todos los inicios de sesión completos, la asignación de usuario de inicio de sesión permanece intacta en las bases de datos que se migran. 

  Si va a migrar los inicios de sesión específicos, asegúrese de seleccionar los inicios de sesión que se asignan a los usuarios de una o varias de las bases de datos seleccionadas para la migración.

- Como parte de la migración de inicio de sesión, Data Migration Assistant también mueve los roles de servidor definido por el usuario y agrega los permisos de nivel de servidor a los roles de servidor definido por el usuario. El propietario de la función se establecerá en **sa** principal.

## <a name="during-and-after-migration"></a>Durante y después de la migración

- Como parte de la migración de inicio de sesión, Data Migration Assistant asigna los permisos a los elementos protegibles en el destino de SQL Server tal y como aparecen en el origen de SQL Server. 

  Si el inicio de sesión ya existe en el destino de SQL Server, Data Migration Assistant migra solo los permisos asignados a los elementos protegibles y no volver a crear el inicio de sesión completa.

- Asistente para migración de datos hace que sea el mejor esfuerzo para asignar el inicio de sesión a los usuarios de base de datos si el inicio de sesión ya existe en el servidor de destino.

- Se recomienda que revise los resultados de la migración para comprender el estado general de la migración de inicio de sesión y las acciones posteriores a la migración recomendadas.

## <a name="resources"></a>Recursos

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Asistente para la migración de datos: Opciones de configuración](../dma/dma-configurationsettings.md)
