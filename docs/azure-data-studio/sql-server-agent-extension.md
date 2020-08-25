---
title: Extensión del Agente SQL Server
description: Aprenda a instalar y usar la extensión Agente SQL Server (versión preliminar) para Azure Data Studio, una extensión para administrar trabajos y configuraciones del Agente SQL.
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 207388fed1ea2465fb965457640b5e1fb0d162cf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766164"
---
# <a name="sql-server-agent-extension-preview"></a>Extensión del Agente SQL Server (versión preliminar)

La extensión del Agente SQL Server (versión preliminar) es una extensión para administrar y solucionar los problemas de los trabajos del Agente SQL y la configuración. Esta extensión está actualmente en versión preliminar.

Estas son algunas de las acciones principales:
- Mostrar una lista de los trabajos del Agente SQL Server configurados en una instancia de SQL Server
- Ver el historial de trabajos con resultados de la ejecución de trabajos
- Control básico de trabajos para iniciar y detener trabajos

## <a name="install-the-sql-server-agent-extension"></a>Instalar la extensión del Agente SQL Server

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.

   ![Instalar el agente](media/extensions/sql-server-agent-extension/install-sql-agent.png)

1. Seleccione la extensión que quiera e **instálela**.
2. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).
1. Para ir al panel de administración, haga clic con el botón derecho en el servidor o la base de datos y seleccione **Administrar**.
2. Las extensiones instaladas se muestran como pestañas en el panel de administración:

   ![Ver el agente](media/extensions/sql-server-agent-extension/view-sql-agent.png)

## <a name="view-jobs"></a>Ver trabajos

Al conectarse a la extensión del Agente SQL Server, lo primero que verá es una lista de todos los trabajos del agente.

   ![Ver trabajos](media/extensions/sql-server-agent-extension/job-view.png)

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el Agente SQL Server, [vea la documentación](../ssms/agent/sql-server-agent.md?view=sql-server-2017).