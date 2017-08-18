---
title: Configurar registros de errores de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d6815aac3852922ae49a4953abc501a2cf958a4c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="scm-services---configure-sql-server-error-logs"></a>Servicios SCM - Configurar registros de errores de SQL Server
  En este tema se describe cómo ver o modificar la forma en que se reciclan los registros de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir el cuadro de diálogo Configurar registros de errores de SQL Server  
  
1.  En el Explorador de objetos, expanda la instancia de SQL Server, expanda **Administración**, haga clic con el botón derecho en **Registros de SQL Server**y después haga clic en **Configurar**.  
  
2.  En el cuadro de diálogo **Configurar registros de errores de SQL Server** , elija una de las siguientes opciones.  
  
     **Limitar el número de archivos de registro de error antes de reciclarlos**  
     Actívela para limitar el número de registros de error que se deben crear antes de que se reciclen. Se crea un nuevo registro de errores cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva copias de seguridad de los seis registros anteriores, a menos que se active esta opción y se especifique un número máximo de archivos de registro de errores diferente a continuación.  
  
     **Número máximo de archivos de registro de errores**  
     Especifica el número máximo de archivos de registro de errores que se pueden crear antes de reciclarse. El valor predeterminado es 6, que es el número de registros de copia de seguridad anteriores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva antes de reciclarlos.  
  
  
