---
title: Configurar registros de errores de SQL Server | Microsoft Docs
description: Obtenga información sobre el reciclaje de registros de errores. Vea cómo establecer un tamaño máximo de archivo de registro y cómo establecer el número de archivos de registro anteriores que SQL Server archiva y del que hace una copia de seguridad.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 060b3828c772a030ab095ae1bea857dc8eaa3b5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651375"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>Servicios SCM - Configurar registros de errores de SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe cómo ver o modificar la forma en que se reciclan los registros de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>Para abrir el cuadro de diálogo Configurar registros de errores de SQL Server  

1. En el Explorador de objetos, expanda la instancia de SQL Server, expanda **Administración**, haga clic con el botón derecho en **Registros de SQL Server**y después haga clic en **Configurar**.

2. En el cuadro de diálogo **Configurar registros de errores de SQL Server** , elija una de las siguientes opciones.

    a. Número de archivos de registro

      **Limitar el número de archivos de registro de error antes de reciclarlos**

      Actívela para limitar el número de registros de error que se deben crear antes de que se reciclen. Se crea un nuevo registro de errores cada vez que se inicia una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva copias de seguridad de los seis registros anteriores, a menos que se active esta opción y se especifique un número máximo de archivos de registro de errores diferente a continuación.  
  
      **Número máximo de archivos de registro de errores**

      Especifica el número máximo de archivos de registro de errores archivados que se pueden crear antes de reciclarse. El valor predeterminado es 6, sin incluir el actual. Este valor determina el número de registros de copia de seguridad anteriores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva antes de reciclarlos.

    b. Tamaño de archivo de registro

      **Tamaño máximo del archivo de registro de errores en KB**

      Puede establecer la cantidad de tamaño de cada archivo en KB. Si lo deja en 0, el tamaño del registro es ilimitado.
