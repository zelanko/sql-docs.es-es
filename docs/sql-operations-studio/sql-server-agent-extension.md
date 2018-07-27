---
title: SQL Operations Studio extensión del Agente SQL Server (versión preliminar) | Microsoft Docs
description: Extensión del Agente SQL Server para SQL Operations Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 07/19/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 0da107a9f5dab0a9eb468bc3570788cff816b24a
ms.sourcegitcommit: 4b21840f20195d70f255465666f7b409ba839d18
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2018
ms.locfileid: "39147037"
---
# <a name="sql-server-agent-extension"></a>Extensión del Agente SQL Server

La extensión del Agente SQL Server es una extensión para administrar y solucionar problemas de configuración y los trabajos del Agente SQL. Esta extensión está actualmente en versión preliminar.

Las acciones claves son:
- Trabajos del agente lista SQL Server configurados en un servidor SQL Server
- Ver historial de trabajos con los resultados de la ejecución de trabajo
- Control de trabajo básico para iniciar y detener trabajos

## <a name="install-the-sql-server-agent-extension"></a>Instalar la extensión del Agente SQL Server

1. Para abrir el Administrador de extensiones y tener acceso a las extensiones disponibles, seleccione el icono de extensiones o **extensiones** en el **vista** menú.
2. Seleccione una extensión disponible para ver sus detalles.

   ![Instalar agente](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. Seleccione la extensión que desee y **instalar** lo.
2. Seleccione **recarga** para habilitar la extensión (solo es necesario instalar una extensión por primera vez).
1. Vaya a su panel de administración haciendo clic en el servidor o base de datos y seleccionar **administrar**.
2. Las extensiones instaladas aparecen como pestañas en el panel de administración:

   ![Agente de vista](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Ver trabajos

Cuando se conecta a la extensión del Agente SQL Server, lo primero que ve es una lista de todos los trabajos del agente.

   ![Ver trabajos](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el Agente SQL Server, [consulte nuestra documentación.](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017)


