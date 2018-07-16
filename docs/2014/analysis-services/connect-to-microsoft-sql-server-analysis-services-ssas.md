---
title: Conectarse a Microsoft SQL Server Analysis Services (SSAS) | Microsoft Docs
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
- sql12.asvs.bidtoolset.connsqlserveras.f1
ms.assetid: 7f3244ee-b690-471c-893d-68e361c2d416
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43a7dd31c52c81f7a2bfcbf87d1a8df3f6740081
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323665"
---
# <a name="connect-to-microsoft-sql-server-analysis-services-ssas"></a>Conectarse a Microsoft SQL Server Analysis Services (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite especificar valores para importar datos de un cubo de Microsoft SQL Server Analysis Services o un libro PowerPivot que se hospeda en SharePoint. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado.  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar una base de datos en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Servidor o el nombre de archivo**  
 Escriba uno de los datos siguientes:  
  
-   Escriba el nombre o dirección IP del servidor SQL Server Analysis Services al que conectarse.  
  
     Puede utilizar un punto (.), (local) o localhost para indicar el servidor local.  
  
-   Escriba la dirección URL de un libro PowerPivot publicado en SharePoint.  
  
 **Utilizar autenticación de Windows**  
 Especifique si se utiliza la autenticación de Windows para conectarse a un servidor de SQL Server Analysis Services.  
  
 El modo de autenticación de Windows permite que un usuario pueda conectarse a través de una cuenta de usuario de Windows. Siempre que sea posible, utilice la autenticación de Windows.  
  
 Cuando se utiliza la autenticación de Windows, las credenciales del usuario actual se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Utilizar autenticación de SQL Server**  
 Especifique si se utiliza la autenticación de SQL Server para conectarse a un servidor de SQL Server Analysis Services.  
  
 Con la autenticación de SQL Server, SQL Server realiza la autenticación por sí mismo comprobando si se ha configurado una cuenta de inicio de sesión de SQL Server y si la contraseña especificada coincide con la registrada previamente.  
  
 La autenticación de SQL Server se utiliza para crear la cadena de conexión para el origen de datos. Estas credenciales también se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario para la conexión con la base de datos. Esta opción solo está disponible si ha seleccionado la autenticación de Windows para conectarse.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos. Esta opción solo es modificable si ha seleccionado la autenticación de SQL Server para conectarse.  
  
 **Guardar mi contraseña**  
 Especifique si la contraseña que ha escrito en el cuadro **Contraseña** está almacenada. Esta opción solo está disponible si ha seleccionado la autenticación de SQL Server para conectarse.  
  
 **Nombre de la base de datos**  
 Seleccione una base de datos en la lista de bases de datos.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales con el cuadro de diálogo **Establecer propiedades avanzadas** . Para obtener más información, vea [Establecer propiedades avanzadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Probar conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  
