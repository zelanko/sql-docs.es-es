---
title: Propiedades de la base de datos (página Archivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36b0d8b5d91b18ad4b97ac873ad3073ca97b133e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871991"
---
# <a name="database-properties-files-page"></a>Propiedades de la base de datos (página Archivos)
  Utilice esta página para crear una nueva base de datos o para ver o modificar las propiedades de la base de datos seleccionada. Este tema se aplica a **Propiedades de la base de datos (página Archivos)** de las bases de datos existentes y a **Nueva base de datos (página General)**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre de la base de datos**  
 Agregue o muestre el nombre de la base de datos.  
  
 **Propietario**  
 Especifique el propietario de la base de datos seleccionándolo en la lista.  
  
 **Usar indización de texto completo**  
 Esta casilla está activada y deshabilitada debido a que la indización de texto completo siempre está habilitada en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Búsqueda de texto completo](../search/full-text-search.md).  
  
 **Archivos de la base de datos**  
 Agregue, vea, modifique o quite archivos de la base de datos asociada. Los archivos de la base de datos tienen las siguientes propiedades:  
  
 **Nombre lógico**  
 Escriba o modifique el nombre del archivo.  
  
 **Tipo de archivo**  
 Seleccione el tipo de archivo en la lista. El tipo de archivo puede ser **Datos**, **Registro**o **Datos de FILESTREAM**. No se puede modificar el tipo de archivo de un archivo existente.  
  
 Seleccione **Datos de FILESTREAM** si va a agregar archivos (contenedores) a un grupo de archivos optimizados para memoria.  
  
 Para agregar archivos (contenedores) a un grupo de archivos de datos FILESTREAM, debe haber habilitado FILESTREAM. Puede habilitar FILESTREAM mediante el cuadro de diálogo [Propiedades del servidor (página Opciones avanzadas)](../../database-engine/configure-windows/server-properties-advanced-page.md) .  
  
 **Grupo de archivos**  
 Seleccione el grupo de archivos en la lista. El grupo de archivos es PRIMARY de forma predeterminada. Puede crear un nuevo grupo de archivos si selecciona **\<nuevo grupo de archivos>** y escribe información sobre el grupo de archivos en el cuadro de diálogo **Grupo de archivos nuevo**. También se puede crear un nuevo grupo de archivos en la página **Grupo de archivos** . No se puede modificar el grupo de archivos de un archivo existente.  
  
 Al agregar archivos (contenedores) a un grupo de archivos optimizados para memoria, el campo **Grupo de archivos** se rellenará con el nombre del grupo de archivos optimizados para memoria de la base de datos.  
  
 **Tamaño inicial**  
 Escriba o modifique el tamaño inicial del archivo en megabytes. De forma predeterminada, será el valor de la base de datos **modelo** .  
  
 Este campo no es válido para los archivos FILESTREAM.  
  
 Para los archivos de los grupos de archivos optimizados para memoria, este campo no se puede modificar.  
  
 **Crecimiento automático**  
 Seleccione o muestre las propiedades de crecimiento automático del archivo. Estas propiedades controlan cómo se expande el archivo cuando se alcanza su máximo tamaño de archivo. Para editar los valores de crecimiento automático, haga clic en el botón de edición situado junto a las propiedades de crecimiento automático del archivo deseado y modifique los valores del cuadro de diálogo **Cambiar crecimiento automático** . De forma predeterminada, serán los valores de la base de datos **modelo** .  
  
 Este campo no es válido para los archivos FILESTREAM.  
  
 En el caso de los archivos de los grupos de archivos optimizados para memoria, este campo debe establecerse en **Ilimitado**.  
  
 **Ruta de acceso**  
 Muestra la ruta de acceso del archivo seleccionado. Para especificar una ruta de acceso a un nuevo archivo, haga clic en el botón de edición situado junto a la ruta de acceso al archivo y navegue a la carpeta de destino. No se puede modificar la ruta de acceso de un archivo existente.  
  
 Para los archivos FILESTREAM, la ruta de acceso es una carpeta. El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creará los archivos subyacentes en esta carpeta.  
  
 **Nombre de archivo**  
 Muestra el nombre del archivo.  
  
 Este campo no es válido para los archivos FILESTREAM, lo cual incluye los archivos en grupos de archivos optimizados para memoria.  
  
 **Agregar**  
 Agrega un nuevo archivo a la base de datos.  
  
 **Quitar**  
 Elimina el archivo seleccionado de la base de datos. No podrá eliminarse un archivo a menos que esté vacío. El archivo de datos principal y el archivo de registro principal no se pueden quitar.  
  
 Para obtener información acerca de los archivos, vea [Database Files and Filegroups](database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
