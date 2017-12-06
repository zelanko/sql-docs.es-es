---
title: "Selector de demonio de filtro de texto completo SQL (Administrador de configuración de SQL Server) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: "8"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0829cbef976a5fc53166cf5616a900e8472e9e0d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], utiliza el servicio de selector de demonio de filtro de texto completo de SQL (iniciador de FDHOST) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] búsqueda de texto completo para iniciar el proceso de host de demonio de filtro, que controla la separación de palabras y los filtros de búsqueda de texto completo. Este servicio debe estar ejecutándose para poder utilizar la búsqueda de texto completo. El servicio del iniciador de FDHOST reconoce las instancias y está asociado a una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El servicio del iniciador de FDHOST propaga la información de la cuenta de servicio a cada proceso de host de demonio de filtro iniciado. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
