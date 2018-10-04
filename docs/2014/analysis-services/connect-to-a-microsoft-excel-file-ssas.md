---
title: Conectarse a un archivo de Microsoft Excel (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connexcelfile.f1
ms.assetid: 126f7d6b-d270-40e7-b23e-8d114f87065b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 199da8714542f8de8b7281906f07f3fcd4aaa430
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067435"
---
# <a name="connect-to-a-microsoft-excel-file-ssas"></a>Conectar con un archivo de Microsoft Excel (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite conectar con un archivo de Microsoft Excel almacenado en el equipo local. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un archivo de Microsoft Excel, debe tener instalado en el equipo el proveedor ACE adecuado. Para obtener más información, vea [Orígenes de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar un archivo en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer el archivo seleccionado.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Ruta de acceso de archivo de Excel**  
 Especifique la ruta de acceso completa para el archivo de Excel.  
  
 **Examinar**  
 Navegue a una ubicación donde haya un archivo de Excel.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales al usar el cuadro de diálogo **Establecer propiedades avanzadas** .  
  
 **Usar la primera fila como encabezados de columna**  
 Especifique si utilizar la primera fila de datos como encabezados de columna de la tabla de destino.  
  
 **Probar conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  
