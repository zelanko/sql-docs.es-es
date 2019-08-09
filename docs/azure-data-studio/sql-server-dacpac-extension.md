---
title: Extensión dacpac de SQL Server
titleSuffix: Azure Data Studio
description: Instale y use la extensión dacpac de SQL Server (versión preliminar) para Azure Data Studio.
ms.custom: seodec18
ms.date: 03/18/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: e40e377310b33034b4abecdc5e58eab17d39695d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959194"
---
# <a name="sql-server-dacpac-extension-preview"></a>Extensión dacpac de SQL Server (versión preliminar)

El **Asistente para aplicaciones de capa de datos** proporciona una experiencia fácil de usar para implementar y extraer archivos .dacpac, así como para importar y exportar archivos .bacpac.

Esta experiencia está actualmente en su versión preliminar inicial. Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).

![data-actions](media/sql-server-dacpac-extension/data-tier-application-actions.png)

 ### <a name="requirements"></a>Requisitos
 * Para iniciarse, este asistente requiere una conexión activa a una instancia de SQL Server.

 ### <a name="how-do-i-start-the-data-tier-application-wizard"></a>¿Cómo se inicia el Asistente para aplicaciones de capa de datos?
 * El punto de entrada principal del asistente consiste en hacer clic con el botón derecho en una base de datos en el Explorador de objetos y, luego, hacer clic en el **Asistente para aplicaciones de capa de datos**.
 * Si un usuario está conectado a una instancia de SQL Server, también puede iniciar el asistente desde la paleta de comandos (Ctrl+Mayús+P), para lo que debe buscar el **Asistente para aplicaciones de capa de datos**.

 ### <a name="why-would-i-use-the-data-tier-application-wizard"></a>¿Por qué es tan útil Asistente para aplicaciones de capa de datos?
 Este asistente está diseñado para agregar la capacidad de extraer e implementar archivos .dacpac e importar y exportar archivos .bacpac en Azure Data Studio.

## <a name="install-the-sql-server-dacpac-extension"></a>Instalación de la extensión dacpac de SQL Server

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione la extensión dacpac de SQL Server y haga clic en **Instalar**.
1. Seleccione **Recargar** para habilitar la extensión (solo es necesario la primera vez que se instala una extensión).
2. Para ir al panel de administración, haga clic con el botón derecho en el servidor o la base de datos y seleccione **Administrar**.
3. Las extensiones instaladas aparecen como pestañas en el panel de administración:

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre dacpac, consulte [nuestra documentación](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/data-tier-applications?view=sql-server-2017).