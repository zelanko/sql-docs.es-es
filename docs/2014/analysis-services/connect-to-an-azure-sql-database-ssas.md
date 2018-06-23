---
title: Conectarse a una base de datos SQL Azure (SSAS) | Documentos de Microsoft
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
- sql12.asvs.bidtoolset.connsqlazure.f1
ms.assetid: 4e0344e9-1822-4698-ad22-05f1f341ced7
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1e127b69e30032a31a97f4cc46ae87279de7987d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113064"
---
# <a name="connect-to-an-azure-sql-database-ssas"></a>Conexión con una Azure SQL Database (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite conectar con [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
> [!NOTE]  
>  Si va a conectarse a un conjunto de datos de Azure DataMarket, vea [Conectarse a un informe o a una fuente de distribución de datos &#40;SSAS&#41;](connect-to-a-report-or-data-feed-ssas.md).  
  
 [!INCLUDE[ssSDS](../includes/sssds-md.md)] es una base de datos relacional hospedada con la que se conecta usando la autenticación de SQL Server. Para obtener más información sobre [!INCLUDE[ssSDS](../includes/sssds-md.md)], vea el sitio web [Base de datos SQL](http://go.microsoft.com/fwlink/?LinkID=157856). Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado.  
  
> [!NOTE]  
>  Las credenciales del usuario actual se utilizan al seleccionar una base de datos en esta página. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Nombre del servidor**  
 Escriba el nombre o la dirección IP del servidor al que va a conectarse.  
  
 **Nombre de usuario.**  
 Especifique un nombre de usuario para la conexión con la base de datos.  
  
 Este nombre de usuario se utiliza para crear la cadena de conexión para el origen de datos. Estas credenciales también se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos.  
  
 **Guardar mi contraseña**  
 Especifique si la contraseña que ha escrito en el cuadro **Contraseña** está almacenada.  
  
 **Nombre de la base de datos**  
 Seleccione una base de datos en la lista de bases de datos.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales con el cuadro de diálogo **Establecer propiedades avanzadas** . Para obtener más información, vea [Establecer propiedades avanzadas &#40;SSAS&#41;](set-advanced-properties-ssas.md).  
  
 **Probar conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  