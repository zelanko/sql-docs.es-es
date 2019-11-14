---
title: Migre SQL Server inicios de sesión con Data Migration Assistant
description: Obtenga información sobre cómo migrar inicios de sesión de SQL Server con Data Migration Assistant
ms.date: 10/22/2019
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
ms.author: jtoland
ms.custom: seo-lt-2019
ms.openlocfilehash: 368372ab7324b11e9f7fdaa6af94d5ba2c0534ad
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056477"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Migre SQL Server inicios de sesión con Data Migration Assistant

En este artículo se proporciona información general sobre la migración de inicios de sesión de SQL Server mediante Data Migration Assistant.

> [!IMPORTANT]
> Este tema se aplica a escenarios en los que se realizan actualizaciones de SQL Server en versiones posteriores del producto local o en SQL Server en Azure Virtual Machines.

## <a name="which-logins-are-migrated"></a>Qué inicios de sesión se migran

- Puede migrar los inicios de sesión en función de una entidad de seguridad de Windows (como un usuario de dominio o un grupo de dominio de Windows). También puede migrar los inicios de sesión creados en función de la autenticación de SQL, también denominada inicios de sesión de SQL Server.

- Actualmente, Data Migration Assistant no admite los inicios de sesión asociados a un certificado de seguridad independiente (inicios de sesión asignados a certificados), una clave asimétrica independiente (inicios de sesión asignados a la clave asimétrica) e inicios de sesión asignados a las credenciales.

- Data Migration Assistant no mueve el inicio de sesión **SA** y los principios del servidor con nombres delimitados por marcas hash dobles (\#\#), que solo son para uso interno.

- De forma predeterminada, Data Migration Assistant selecciona todos los inicios de sesión calificados que se van a migrar. Opcionalmente, puede seleccionar inicios de sesión específicos para migrar. Cuando Data Migration Assistant migra todos los inicios de sesión calificados, la asignación de usuario de inicio de sesión permanece intacta en las bases de datos que se migran.

  Si tiene previsto migrar inicios de sesión específicos, asegúrese de seleccionar los inicios de sesión asignados a uno o más usuarios en las bases de datos seleccionadas para la migración.

- Como parte de la migración de inicio de sesión, Data Migration Assistant también mueve roles de servidor definidos por el usuario y agrega permisos de nivel de servidor a los roles de servidor definidos por el usuario. El propietario del rol se establecerá en **SA** principal.

## <a name="during-and-after-migration"></a>Durante y después de la migración

- Como parte de la migración de inicio de sesión, Data Migration Assistant asigna los permisos a elementos protegibles en el SQL Server de destino tal y como existen en el SQL Server de origen.

  Si el inicio de sesión ya existe en el SQL Server de destino, Data Migration Assistant migra solo los permisos asignados a elementos protegibles y no volverá a crear el inicio de sesión completo.

- Data Migration Assistant hace el mejor esfuerzo para asignar el inicio de sesión a los usuarios de la base de datos si el inicio de sesión ya existe en el servidor de destino.

- Se recomienda revisar los resultados de la migración para comprender el estado general de la migración de inicio de sesión y las acciones posteriores a la migración recomendadas.

## <a name="resources"></a>Recursos

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant: opciones de configuración](../dma/dma-configurationsettings.md)
