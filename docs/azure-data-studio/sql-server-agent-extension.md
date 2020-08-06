---
title: Extensión del Agente SQL Server
description: Aprenda a instalar y usar la extensión Agente SQL Server (versión preliminar) para Azure Data Studio, una extensión para administrar trabajos y configuraciones del Agente SQL.
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e3329950ba9b6b4b9db46950a1633a4bfd5f2ccf
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522489"
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

Para obtener más información sobre el Agente SQL Server, [vea la documentación](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent?view=sql-server-2017).


