---
title: Crear o editar un grupo de servidores
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.editgroup.f1
- sql13.swb.newgroup.f1
helpviewer_keywords:
- Registered Servers [SQL Server], server groups
- server groups [SQL Server]
- groups [SQL Server], server
ms.assetid: d4a942bd-2dd1-42db-ad0e-e9a9ae5b856d
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: eb39627de23f236dcd3a7241f83883b747353501
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001741"
---
# <a name="create-or-edit-a-server-group-sql-server-management-studio"></a>Crear o editar un grupo de servidores (SQL Server Management Studio)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

En este tema se describe cómo organizar los servidores de Servidores registrados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] creando grupos de servidores y poniendo los servidores en los grupos de servidores. Puede crear grupos de servidores en cualquier momento en Servidores registrados o cuando registra los servidores.  

## <a name="SSMSProcedure"></a>

### <a name="to-create-a-server-group-in-registered-servers"></a>Para crear un grupo de servidores en Servidores registrados  

1. En Servidores registrados, haga clic en el tipo de servidor en la barra de herramientas Servidores registrados. Si Servidores registrados no está visible, haga clic en **Servidores registrados** en el menú **Ver** .  

2. Haga clic con el botón derecho en un servidor o un grupo de servidores, seleccione **Nuevo**y, después, haga clic en **Grupo de servidores**.  

3. En el cuadro de diálogo **Nuevo grupo de servidores** , en el cuadro de lista **Nombre del grupo** , escriba un nombre único para el grupo de servidores. El nombre del grupo de servidores debe ser único en la ubicación actual del árbol Servidores registrados.

4. En el cuadro de lista **Descripción del grupo** , puede escribir, si lo desea, un nombre descriptivo del grupo, por ejemplo, "Servidores financieros para América Latina".  

5. En el cuadro **Seleccionar una ubicación para el nuevo grupo de servidores** , haga clic en la ubicación en la que desee colocar el grupo y, a continuación, haga clic en **Guardar**.  

   > [!NOTE]
   > También puede crear un grupo de servidores mientras está registrando un servidor. Para ello, haga clic en **Nuevo grupo**y, después, rellene el cuadro de diálogo **Nuevo grupo** .  

## <a name="see-also"></a>Consulte también

[Registrar servidores](../../tools/sql-server-management-studio/register-servers.md)