---
title: Extensión de dacpac de SQL Server
titleSuffix: Azure Data Studio
description: Instalar y usar la extensión de dacpac de SQL Server (versión preliminar) para Azure Data Studio
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959194"
---
# <a name="sql-server-dacpac-extension-preview"></a>Extensión dacpac de SQL Server (versión preliminar)

**El Asistente para aplicaciones de capa de datos** proporciona una experiencia fácil de usar para implementar y extraer archivos .dacpac, importar y exportar archivos bacpac.

Esta experiencia está actualmente en su versión preliminar inicial. Por favor, notificar problemas y solicitudes de características [aquí.](https://github.com/microsoft/azuredatastudio/issues)

![acciones de datos](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisitos
 * Este asistente requiere una conexión activa a una instancia de SQL Server para iniciar.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>¿Cómo se puede iniciar el Asistente para aplicaciones de capa de datos?
 * Es el punto de entrada principal para que el asistente a la derecha, haga clic en una base de datos en el Explorador de objetos y haga clic en **Asistente para aplicaciones de capa de datos**.
 * Si un usuario está conectado a una instancia de SQL Server, el usuario también puede iniciar el asistente desde la paleta de comandos (Ctrl + Mayús + P) mediante la búsqueda de **Asistente para aplicaciones de capa de datos.**

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>¿Por qué se puede usar el Asistente para aplicaciones de capa de datos?
 Se creó este asistente para agregar la capacidad para extraer e implementar archivos .dacpac e importar y exportar archivos bacpac en Azure Data Studio.

## <a name="install-the-sql-server-dacpac-extension"></a>Instalar la extensión de dacpac de SQL Server

1. Para abrir el Administrador de extensiones y tener acceso a las extensiones disponibles, seleccione el icono de extensiones o **extensiones** en el **vista** menú.
2. Seleccione la extensión de dacpac de SQL Server y haga clic en **instalar**.
1. Seleccione **recarga** para habilitar la extensión (solo es necesario instalar una extensión por primera vez).
2. Vaya a su panel de administración haciendo clic en el servidor o base de datos y seleccionar **administrar**.
3. Las extensiones instaladas aparecen como pestañas en el panel de administración:

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre la dacpac, [consulte nuestra documentación.](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017)