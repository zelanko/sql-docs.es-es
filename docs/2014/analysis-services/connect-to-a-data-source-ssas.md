---
title: Conectarse a un origen de datos (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndatasource.f1
ms.assetid: 1e2b17e9-092b-4af1-8a58-c52b8fe10ff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1c1114dd63b9082c6be7486ab5e576a6b8270485
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087340"
---
# <a name="connect-to-a-data-source-ssas"></a>Conectarse a un origen de datos (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite crear una nueva conexión con un origen de datos con diversidad de orígenes de datos, como bases de datos relacionales, fuentes de distribución de datos y archivos. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado. También debe tener el proveedor adecuado instalado en el servidor de bases de datos del área de trabajo. Para los servidores de 32 bits (x86), se deben instalar los proveedores de 32 bits. Para los servidores de 64 bits (x64), se deben instalar los proveedores de 64 bits.  
  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] siempre se ejecuta en un proceso de 32 bits, independientemente de la arquitectura. Cuando ejecute [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] en un equipo de 64 bits, debe tener en cuenta lo siguiente al instalar los proveedores de datos:  
  
-   Para los proveedores que admiten la instalación en paralelo de proveedores de 32 y 64 bits, debe instalar los dos proveedores.  
  
-   Para el proveedor ACE, debe instalar la versión de 64 bits del proveedor. Dado que Office instala automáticamente el proveedor ACE, no debe ejecutar una versión de 32 bits de Microsoft Office en un equipo de 64 bits que hospeda el servidor de bases de datos del área de trabajo.  
  
     El proveedor ACE se utiliza para importar datos de archivos de texto, de Excel y de Access. Si no necesita estos orígenes de datos, puede ejecutar una versión de 32 bits de Microsoft Office en un equipo que ejecuta un servidor de bases de datos del área de trabajo de 64 bits.  
  
-   Para otros proveedores que no admiten la instalación en paralelo de proveedores de 32 y 64 bits, debe instalar el proveedor de 32 bits. Si solo dispone de equipos de 64 bits, debe usar un equipo remoto con un proveedor de 64 bits instalado como servidor de bases de datos del área de trabajo.  
  
  
