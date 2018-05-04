---
title: Grupos de servidores en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información acerca de los grupos de servidor en las operaciones de SQL Studio (versión preliminar).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 07144aff1008499dcfba99a8afd58c535777e0da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="server-groups-in-includename-sosincludesname-sos-shortmd"></a>Grupos de servidores en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Grupos de servidores proporcionan una manera de organizar las conexiones a los servidores y trabajar con bases de datos. Al crear grupos de servidores, los detalles de configuración se guardan en *configuración de usuario*.

## <a name="create-and-edit-server-groups"></a>Crear y editar grupos de servidores

1. Haga clic en **nuevo grupo de servidores** en la parte superior de la *servidores* sidebar.
2. Escriba un nombre de grupo y seleccione un color para el grupo. Opcionalmente, agregue una descripción.

   ![Agregar grupo de servidores](./media/server-groups/add-server-group.png)

Para editar un grupo de servidores existente, haga clic en el grupo y seleccione **Editar grupo de servidores**.

Para modificar los colores de grupo de servidor disponible, modifique la *grupos de servidores* valores en [configuración de usuario](settings.md).

> [!TIP]
> Puede arrastrar y colocar servidores entre distintos grupos de servidores.



## <a name="additional-resources"></a>Recursos adicionales
- [Configuración de área de trabajo y usuario](settings.md)