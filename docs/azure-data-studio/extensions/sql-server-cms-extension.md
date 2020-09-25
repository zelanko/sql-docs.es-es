---
title: Extensión Servidores de administración central de SQL Server
description: Obtenga información sobre cómo instalar y usar la extensión de Servidores de administración central de SQL Server. Una extensión para agrupar servidores y aplicar acciones al grupo.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 06/06/2019
ms.openlocfilehash: ca200de903675da9fdfbd2549d3ee1b5bd192907
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123491"
---
# <a name="sql-server-central-management-servers-extension-preview"></a>Extensión de Servidores de administración central de SQL Server (versión preliminar)

La extensión Servidores de administración central permite a los usuarios almacenar una lista de instancias de SQL Server organizadas en uno o más grupos. Las acciones que se llevan a cabo mediante un servidor de administración central (CMS) actúan en todos los servidores del grupo.

Esta experiencia está actualmente en su versión preliminar inicial. Puede notificar cualquier problema y solicitar nuevas características [aquí](https://github.com/microsoft/azuredatastudio/issues).

![Extensión CMS](media/sql-server-cms-extension/cms-list.png)

## <a name="install-the-sql-server-central-management-servers-extension"></a>Instalación de la extensión Servidores de administración central de SQL Server

1. Para abrir el administrador de extensiones y acceder a las extensiones disponibles, seleccione el icono de extensiones, o bien seleccione **Extensiones** en el menú **Ver**.
2. Seleccione una extensión disponible para ver sus detalles.
3. Seleccione la extensión que desee (Servidores de administración central de SQL Server) y seleccione **Instalar**.

### <a name="how-do-i-start-central-management-servers"></a>¿Cómo se inicia Servidores de administración central?

 Para ver Servidores de administración central, haga clic en el icono Conexiones (Ctrl/CMD + G). La primera vez que se descarga la extensión, la vista de CMS aparece minimizada; para abrirla, haga clic en **Servidores de administración central**.

## <a name="next-steps"></a>Pasos siguientes

[Aquí puede leer más información](../../ssms/register-servers/create-a-central-management-server-and-server-group.md) sobre los conceptos de Servidores de administración central.