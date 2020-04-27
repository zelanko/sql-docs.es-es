---
title: Configurar un Firewall para el acceso de FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall [Database Engine], FILESTREAM
- FILESTREAM [SQL Server], Windows Firewall
ms.assetid: fc52007f-c26f-4f8e-b9d8-55a7978f4d56
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fff59c773e4c96b8d14cf604c1a9a3e2b31869f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010309"
---
# <a name="configure-a-firewall-for-filestream-access"></a>Configurar un Firewall para el acceso de FILESTREAM
  Para utilizar FILESTREAM en un entorno protegido mediante firewall, tanto el cliente como el servidor deben poder resolver los nombres DNS en el servidor que contenga los archivos FILESTREAM. FILESTREAM requiere que los puertos 139 y 445 de uso compartido de archivos de Windows estén abiertos.  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>Para abrir los puertos de uso compartido de archivos de Windows en un equipo que ejecuta Windows 7  
  
1.  En el Panel de control, abra **Firewall de Windows**.  
  
2.  En el panel izquierdo, haga clic en **Configuración avanzada**. Si se le pide una contraseña de administrador o una confirmación, escriba la contraseña o proporcione la confirmación.  
  
3.  En el cuadro de diálogo **Firewall de Windows con seguridad avanzada** , en el panel izquierdo, haga clic en **Reglas de entrada**y, a continuación, en el panel derecho, haga clic en **Nueva regla**.  
  
4.  Siga las instrucciones del Asistente para nueva regla de entrada para agregar el puerto TCP 139.  
  
5.  Repita el paso anterior para agregar el puerto TCP 445.  
  
6.  Cierre el cuadro de diálogo de **Firewall de Windows con seguridad avanzada** .  
  
  
