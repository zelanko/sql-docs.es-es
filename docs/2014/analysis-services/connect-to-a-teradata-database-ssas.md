---
title: Conectarse a una base de datos de Teradata (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connterradb.f1
ms.assetid: 875ad4a3-a2b3-4b68-8c1c-6507e9f25b4d
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cfe95cae0b7c3dba77bc08839569fa8cca20d114
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37163856"
---
# <a name="connect-to-a-teradata-database-ssas"></a>Conectarse a una base de datos de Teradata (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite especificar los valores para conectarse con una base de datos de Teradata. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado.  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar una base de datos en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Nombre del servidor**  
 Escriba o seleccione el nombre de la instancia de servidor a la que va a conectarse.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario para la conexión con la base de datos.  
  
 Este nombre de usuario se utiliza para crear la cadena de conexión para el origen de datos. Estas credenciales también se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos.  
  
 **Guardar mi contraseña**  
 Especifique si es necesario guardar la contraseña que ha escrito en el cuadro **Contraseña** .  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales con el cuadro de diálogo **Establecer propiedades avanzadas** . Para obtener más información, vea [Establecer propiedades avanzadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Probar conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  
