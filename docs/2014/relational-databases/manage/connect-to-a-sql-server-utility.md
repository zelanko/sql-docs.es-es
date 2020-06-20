---
title: Conexión a una utilidad de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cfb8c5c86683c90c590a93ec13959954df329ab6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023609"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectarse a una utilidad de SQL Server
  Antes de poder conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe crear un punto de control de la utilidad (UCP). Para obtener más información, vea [Características y tareas de la utilidad de SQL Server](sql-server-utility-features-and-tasks.md).

 Para ver y administrar el mantenimiento de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

 Para conectarse a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de SSMS:

1.  Inicie SSMS.

2.  En SSMS, conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

3.  Haga clic en **Ver** y, a continuación, en **Explorador de la utilidad**.

4.  En el panel de navegación del Explorador de la utilidad, haga clic en ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**Conectar con la utilidad**.

5.  En el cuadro de diálogo **Conectar con el servidor** , especifique el nombre de instancia del UCP y, a continuación, haga clic en **Conectar**.

6.  Vea el panel de navegación del explorador de la utilidad para obtener una vista de árbol de los recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el UCP.

 Cuando cree un UCP nuevo, también se conectará a la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).

## <a name="see-also"></a>Consulte también
 [Utilidad de SQL Server características y tareas](sql-server-utility-features-and-tasks.md) [vista Resource Health resultados de la directiva &#40;utilidad de SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)


