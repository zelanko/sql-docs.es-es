---
title: Habilitar la opción Bloquear páginas en la memoria (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
caps.latest.revision: 35
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bc2bbf20b7219d55f14911142913e7b6a941bcae
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197452"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Habilitar la opción Bloquear páginas en la memoria (Windows)
  Esta directiva de Windows determina qué cuentas pueden usar un proceso para mantener los datos en la memoria física, impidiendo que el sistema realice la paginación de los datos en la memoria virtual del disco.  
  
> [!NOTE]  
>  El bloqueo de páginas en memoria puede aumentar el rendimiento cuando se espera paginación de memoria en disco.  
  
 Use la herramienta Directiva de grupo de Windows (gpedit.msc) para habilitar esta directiva para la cuenta usada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe ser el administrador del sistema para cambiar esta directiva.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Para habilitar la opción de bloqueo de páginas en memoria  
  
1.  En el menú **Inicio** , haga clic en **Ejecutar**. En el **abiertos** , escriba `gpedit.msc`.  
  
2.  En la consola **Editor de directivas de grupo local** , expanda **Configuración del equipo**y, a continuación, expanda **Configuración de Windows**.  
  
3.  Expanda **Configuración de seguridad**y, a continuación, expanda **Directivas locales**.  
  
4.  Seleccione la carpeta **Asignación de derechos de usuario** .  
  
     Las directivas se mostrarán en el panel de detalles.  
  
5.  En el panel, haga doble clic en **Bloquear páginas en la memoria**.  
  
6.  En el cuadro de diálogo **Configuración de seguridad local – Bloquear páginas en memoria** , haga clic en **Agregar usuario o grupo**.  
  
7.  En el cuadro de diálogo **Seleccionar usuarios, cuentas de servicio o grupos** , agregue una cuenta con privilegios para ejecutar sqlservr.exe.  
  
8.  Cierre sesión y vuelva a iniciarla para que este cambio surta efecto.  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de memoria del servidor](server-memory-server-configuration-options.md)  
  
  