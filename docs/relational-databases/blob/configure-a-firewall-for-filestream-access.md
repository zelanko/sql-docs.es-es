---
title: Configurar un Firewall para el acceso de FILESTREAM | Microsoft Docs
description: Use FILESTREAM en un entorno protegido mediante firewall. Para ello, abra los puertos 139 y 445 de uso compartido de archivos de Windows a fin de configurar el firewall para el acceso de FILESTREAM.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e26da4e57a58340cfca240fe99d8a36787528a49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768043"
---
# <a name="configure-a-firewall-for-filestream-access"></a>Configurar un Firewall para el acceso de FILESTREAM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para utilizar FILESTREAM en un entorno protegido mediante firewall, tanto el cliente como el servidor deben poder resolver los nombres DNS en el servidor que contenga los archivos FILESTREAM. FILESTREAM requiere que los puertos 139 y 445 de uso compartido de archivos de Windows estén abiertos.  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>Para abrir los puertos de uso compartido de archivos de Windows en un equipo que ejecuta Windows 7  
  
1.  En el Panel de control, abra **Firewall de Windows**.  
  
2.  En el panel izquierdo, haga clic en **Configuración avanzada**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o proporcione la confirmación.  
  
3.  En el cuadro de diálogo **Firewall de Windows con seguridad avanzada** , en el panel izquierdo, haga clic en **Reglas de entrada**y, a continuación, en el panel derecho, haga clic en **Nueva regla**.  
  
4.  Siga las instrucciones del Asistente para nueva regla de entrada para agregar el puerto TCP 139.  
  
5.  Repita el paso anterior para agregar el puerto TCP 445.  
  
6.  Cierre el cuadro de diálogo de **Firewall de Windows con seguridad avanzada** .  
  
  
