---
title: Configurar registros de errores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60d38caf365d6db54ea0abe688a3fc2979fdab82
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809688"
---
# <a name="configure-sql-server-error-logs"></a>Configurar registros de errores de SQL Server
  En este tema se describe cómo ver o modificar la forma en que se reciclan los registros de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir el cuadro de diálogo Configurar registros de errores de SQL Server  
  
1.  En el Explorador de objetos, expanda la instancia de SQL Server, expanda **Administración**, haga clic con el botón derecho en **Registros de SQL Server**y después haga clic en **Configurar**.  
  
2.  En el cuadro de diálogo **Configurar registros de errores de SQL Server** , elija una de las siguientes opciones.  
  
     **Limitar el número de archivos de registro de error antes de reciclarlos**  
     Actívela para limitar el número de registros de error que se deben crear antes de que se reciclen. Se crea un nuevo registro de errores cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva copias de seguridad de los seis registros anteriores, a menos que se active esta opción y se especifique un número máximo de archivos de registro de errores diferente a continuación.  
  
     **Número máximo de archivos de registro de errores**  
     Especifica el número máximo de archivos de registro de errores que se pueden crear antes de reciclarse. El valor predeterminado es 6, que es el número de registros de copia de seguridad anteriores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva antes de reciclarlos.  
  
  
