---
title: Conectarse a una base de datos de Microsoft SQL Server (SSAS) | Microsoft Docs
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
- sql12.asvs.bidtoolset.connsqlserverdb.f1
ms.assetid: 6ebfe029-dbba-4f0d-a556-328e79ef629f
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 50dcb1cfa930a6fd09ff1f25d91b4ad4e5b42acb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189462"
---
# <a name="connect-to-a-microsoft-sql-server-database-ssas"></a>Conectarse a una base de datos de Microsoft SQL Server (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite especificar los valores para conectarse con una base de datos de Microsoft SQL Server. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado.  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar una base de datos en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Nombre del servidor**  
 Seleccione el nombre o escriba el nombre o la dirección IP de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la que conectarse.  
  
 Puede utilizar un punto (.), (local) o localhost para indicar el servidor local.  
  
 **Utilizar autenticación de Windows**  
 Especifique si la autenticación de Windows se usa para conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 El modo de autenticación de Windows permite que un usuario pueda conectarse a través de una cuenta de usuario de Windows. Siempre que sea posible, utilice la autenticación de Windows.  
  
 Cuando se utiliza la autenticación de Windows, las credenciales del usuario actual se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Utilizar autenticación de SQL Server**  
 Especifique si la autenticación de SQL Server se usa para conectarse a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Con la autenticación de SQL Server, SQL Server realiza la autenticación por sí mismo comprobando si se ha configurado una cuenta de inicio de sesión de SQL Server y si la contraseña especificada coincide con la registrada previamente.  
  
 La autenticación de SQL Server se utiliza para crear la cadena de conexión para el origen de datos. Estas credenciales también se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario para la conexión con la base de datos. Esta opción solo está disponible si ha seleccionado la autenticación de SQL Server para conectarse.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos. Esta opción solo es modificable si ha seleccionado la autenticación de SQL Server para conectarse.  
  
 **Guardar mi contraseña**  
 Especifique si la contraseña que ha escrito en el cuadro **Contraseña** está almacenada. Esta opción solo está disponible si ha seleccionado la autenticación de SQL Server para conectarse.  
  
 **Nombre de la base de datos**  
 Seleccione una base de datos en la lista de bases de datos.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales con el cuadro de diálogo **Establecer propiedades avanzadas** . Para obtener más información, vea [Establecer propiedades avanzadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Probar conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión fue correcta.  
  
  
