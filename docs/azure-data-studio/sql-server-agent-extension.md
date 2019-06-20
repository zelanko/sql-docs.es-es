---
title: Extensión del Agente SQL Server
titleSuffix: Azure Data Studio
description: Instalar y usar la extensión del Agente SQL Server (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: c21cab43211e168802e8acd94d4664124182b2de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798048"
---
# <a name="sql-server-agent-extension-preview"></a>Extensión del Agente SQL Server (versión preliminar)

La extensión del Agente SQL Server (versión preliminar) es una extensión para administrar y solucionar problemas de configuración y los trabajos del Agente SQL. Esta extensión está actualmente en versión preliminar.

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


