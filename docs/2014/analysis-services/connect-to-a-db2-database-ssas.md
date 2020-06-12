---
title: Conectarse a una base de datos DB2 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.conndb2db.f1
ms.assetid: eeef3697-a4fd-4263-ba7e-f86afa1f46cc
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03c98f3ab44a4a9f3aac91be36f3d704a3f796ab
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527221"
---
# <a name="connect-to-a-db2-database-ssas"></a>Conectarse a una base de datos de DB2 (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite especificar los valores para conectarse con una base de datos de DB2. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 Para conectarse a un origen de datos, debe tener instalado en el equipo el proveedor adecuado.  
  
> [!NOTE]  
>  Al seleccionar una base de datos en esta página, se usan las credenciales del usuario especificado. Sin embargo, la importación no se realizará correctamente si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada.  
  
## <a name="ui-element-list"></a>Lista de elementos de la interfaz de usuario  
 **Nombre descriptivo de la conexión**  
 Escriba un nombre único para esta conexión de origen de datos. Este campo es obligatorio.  
  
 **Nombre del servidor**  
 Escriba o seleccione la instancia de servidor a la que va a conectarse.  
  
 **Nombre de usuario**  
 Especifique un nombre de usuario para la conexión con la base de datos.  
  
 Este nombre de usuario se utiliza para crear la cadena de conexión para el origen de datos. Estas credenciales también se utilizan al obtener una vista previa y filtrar datos en la ventana Propiedades de la tabla y en el Asistente para la importación. Estas credenciales no se utilizan para importar ni actualizar datos, sino que se utilizan las credenciales de Windows especificadas en la página Información de suplantación.  
  
 **Contraseña**  
 Especifique una contraseña para la conexión a la base de datos.  
  
 **Guardar mi contraseña**  
 Especifique si la contraseña que ha escrito en el cuadro **Contraseña** está almacenada.  
  
 **Nombre de la base de datos**  
 Seleccione una base de datos en la lista de bases de datos.  
  
 **Colección de paquetes**  
 Especifique el nombre de la recolección para los paquetes de DB2. Un proveedor utiliza los paquetes para emitir instrucciones SQL y llamar a procedimientos almacenados.  
  
 **Esquema predeterminado**  
 Especifique el nombre del esquema predeterminado para la base de datos seleccionada.  
  
 **Avanzadas**  
 Establezca las propiedades de conexión adicionales mediante el cuadro de diálogo **establecer propiedades avanzadas** .  
  
 **Probar la conexión**  
 Intente establecer una conexión con el origen de datos usando la configuración actual. Se muestra un mensaje que indica si la conexión es correcta.  
  
  
