---
title: Habilitar la opción Bloquear páginas en la memoria (Windows) | Microsoft Docs
description: Obtenga información sobre cómo activar la opción de bloqueo de páginas en memoria. Vea cómo puede mejorar el rendimiento manteniendo los datos en la memoria física en lugar de paginarlos en el disco.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6390c4a4bb4d8ea2ed9b5e5be1712eb7e782a29b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772473"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Habilitar la opción Bloquear páginas en la memoria (Windows)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta directiva de Windows determina qué cuentas pueden usar un proceso para mantener los datos en la memoria física, impidiendo que el sistema realice la paginación de los datos en la memoria virtual del disco.  
  
> [!NOTE]  
>  El bloqueo de páginas en memoria puede aumentar el rendimiento cuando se espera paginación de memoria en disco.  
  
 Use la herramienta Directiva de grupo de Windows (gpedit.msc) para habilitar esta directiva para la cuenta usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe ser el administrador del sistema para cambiar esta directiva.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Para habilitar la opción de bloqueo de páginas en memoria  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**. En el cuadro **Abrir** , escriba **gpedit.msc**.  
  
2.  En la consola **Editor de directivas de grupo local** , expanda **Configuración del equipo**y, a continuación, expanda **Configuración de Windows**.  
  
3.  Expanda **Configuración de seguridad**y, a continuación, expanda **Directivas locales**.  
  
4.  Seleccione la carpeta **Asignación de derechos de usuario** .  
  
     Las directivas se mostrarán en el panel de detalles.  
  
5.  En el panel, haga doble clic en **Bloquear páginas en la memoria**.  
  
6.  En el cuadro de diálogo **Configuración de seguridad local: Bloquear páginas en memoria**, haga clic en **Agregar usuario o grupo**.  
  
7.  En el cuadro de diálogo **Seleccionar usuarios, cuentas de servicio o grupos**, seleccione la cuenta de servicio de SQL Server.  
  
8.  Reinicie el servicio de SQL Server para que esta configuración surta efecto.
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
