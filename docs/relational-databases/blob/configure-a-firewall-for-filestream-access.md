---
title: Configurar un Firewall para el acceso de FILESTREAM | Microsoft Docs
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
ms.openlocfilehash: 94df8085482c48d02e1e174ade2207ddad494acb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085432"
---
# <a name="configure-a-firewall-for-filestream-access"></a>Configurar un Firewall para el acceso de FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para utilizar FILESTREAM en un entorno protegido mediante firewall, tanto el cliente como el servidor deben poder resolver los nombres DNS en el servidor que contenga los archivos FILESTREAM. FILESTREAM requiere que los puertos 139 y 445 de uso compartido de archivos de Windows estén abiertos.  
  
### <a name="to-open-the-windows-file-sharing-ports-on-a-computer-that-is-running-windows-7"></a>Para abrir los puertos de uso compartido de archivos de Windows en un equipo que ejecuta Windows 7  
  
1.  En el Panel de control, abra **Firewall de Windows**.  
  
2.  En el panel izquierdo, haga clic en **Configuración avanzada**. Si le solicitan una contraseña de administrador o le piden confirmación, escriba la contraseña o proporcione la confirmación.  
  
3.  En el cuadro de diálogo **Firewall de Windows con seguridad avanzada** , en el panel izquierdo, haga clic en **Reglas de entrada**y, a continuación, en el panel derecho, haga clic en **Nueva regla**.  
  
4.  Siga las instrucciones del Asistente para nueva regla de entrada para agregar el puerto TCP 139.  
  
5.  Repita el paso anterior para agregar el puerto TCP 445.  
  
6.  Cierre el cuadro de diálogo de **Firewall de Windows con seguridad avanzada** .  
  
  
