---
title: Conectarse a un archivo de Microsoft Excel (SSAS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.bidtoolset.connexcelfile.f1
ms.assetid: 126f7d6b-d270-40e7-b23e-8d114f87065b
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 48de9fd006c3918a23227a097743a95e138b577e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111682"
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
  
  