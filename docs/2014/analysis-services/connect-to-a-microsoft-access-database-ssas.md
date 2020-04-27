---
title: Conectarse a una base de datos de Microsoft Access (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connaccessdb.f1
ms.assetid: 9fa81839-dd8b-41d3-915e-c774a707ed53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95d40cc0a6da642fe92f46a86308da348d5cc040
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087298"
---
# <a name="connect-to-a-microsoft-access-database-ssas"></a>Conectarse a una base de datos de Microsoft Access (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite especificar los valores para conectarse con una base de datos de Microsoft Access. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a una base de datos de Microsoft Access, debe tener instalado en el equipo el proveedor ACE adecuado. Para más información, vea [Orígenes de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-sources-supported-ssas-tabular.md).  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar un archivo en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer el archivo seleccionado.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Nombre de la base de datos**  
 Especifique la ruta de acceso completa para un archivo de base de datos de Microsoft Access.  
  
 **Examinar**  
 Navegue a una ubicación donde haya un archivo de base de datos de Microsoft Access.  
  
 **Nombre de usuario**  
 Especifique un nombre de usuario para la conexión con la base de datos.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos.  
  
 **Guardar mi contraseña**  
 Especifique si la contraseña que ha escrito en el cuadro **Contraseña** está almacenada.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales con el cuadro de diálogo **Establecer propiedades avanzadas** .  
  
 **Probar la conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  
