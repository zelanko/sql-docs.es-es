---
title: Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server)
description: Obtenga información sobre el Selector de demonio de filtro de texto completo de SQL, un servicio que SQL Server usa para iniciar un proceso que necesita para la búsqueda de texto completo.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 63a3cb64254f314d8f997f0b062629c09b1eec39
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881869"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>Selector de demonio de filtro de texto completo de SQL (Administrador de configuración de SQL Server)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el servicio del iniciador del demonio de filtro de la búsqueda de texto completo (iniciador de FDHOST) para iniciar el proceso de host de demonio de filtro, que administra las operaciones de filtrado y separación de palabras de la búsqueda de texto completo. Este servicio debe estar ejecutándose para poder utilizar la búsqueda de texto completo. El servicio del iniciador de FDHOST reconoce las instancias y está asociado a una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El servicio del iniciador de FDHOST propaga la información de la cuenta de servicio a cada proceso de host de demonio de filtro iniciado. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
  
