---
description: Cambiar el nombre de un servidor registrado o un grupo de servidores registrados
title: Cambio del nombre de un servidor o un grupo de servidores registrados
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/02/2016
ms.openlocfilehash: 28ed9e04486fe587ea3bd25d6659283846a6fa8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491824"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Cambiar el nombre de un servidor registrado o un grupo de servidores registrados

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

En este tema se describe cómo cambiar el nombre de un servidor o un grupo de servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este nombre se puede cambiar en cualquier momento. El hecho de cambiar el nombre de un servidor en Servidores registrados solo cambia el nombre que se visualiza. Para conectarse a otro servidor, debe editar las propiedades de conexión del servidor registrado.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio

En el menú, vaya a **Vista\\Servidores registrados** para abrir el panel **Servidores registrados**.

### <a name="to-change-the-name-of-a-server"></a>Para cambiar el nombre de un servidor

1. En **Servidores registrados**, expanda **Motor de base de datos** y, luego, **Grupos de servidores locales**.  

2. Haga clic con el botón derecho en un servidor y seleccione **Propiedades** para abrir la ventana de diálogo **Editar propiedades de registro de servidor** .

3. En el cuadro de texto **Nombre del servidor registrado** , escriba el nuevo nombre del registro del servidor y, luego, haga clic en **Guardar**.  

### <a name="to-change-the-name-of-a-server-group"></a>Para cambiar el nombre de un grupo de servidores  

1. En **Servidores registrados**, expanda **Motor de base de datos** y, luego, **Grupos de servidores locales**.  

2. Haga clic con el botón derecho en un grupo de servidores y seleccione **Propiedades** para abrir la ventana de diálogo **Editar propiedades de registro de servidor** . 

3. En el cuadro de texto **Nombre del grupo** , escriba el nuevo nombre del grupo de servidores y, luego, haga clic en **Guardar**.  

## <a name="see-also"></a>Consulte también

[Cambiar el registro de un servidor &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)
