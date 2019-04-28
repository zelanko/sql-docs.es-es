---
title: Fundamentos del Control de origen | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- source controls [SQL Server Management Studio], providers
- source controls [SQL Server Management Studio]
- source controls [SQL Server Management Studio], about source controls
- source controls [SQL Server Management Studio], clients
ms.assetid: ca35b67a-104a-41fb-ac58-a61be06fe114
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bce3bd6862e612a8cefa35d1c981d608bf2c341c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843003"
---
# <a name="source-control-basics"></a>Fundamentos del control de código fuente
  El control de código fuente hace referencia a un sistema en el que una pieza central de software del servidor almacena y realiza un seguimiento de las versiones de los archivos, además de controlar el acceso a esos archivos. Un sistema típico de control de código fuente incluye un proveedor de control de código fuente y dos o más clientes de control de código fuente.  
  
## <a name="source-control-benefits"></a>Ventajas del control de código fuente  
 La colocación de los archivos bajo control de código fuente permite  
  
-   Administrar el proceso mediante el que el control de los elementos pasa de una persona a otra. Los proveedores de control de código fuente permiten tanto el acceso compartido como el acceso exclusivo a los archivos. Si el acceso a los archivos de un proyecto es exclusivo, el proveedor de control de código fuente solamente permite que un usuario desproteja los archivos y los modifique cada vez. Si el acceso es compartido, más de un usuario podrá desproteger el archivo de script. Además, el proveedor de control de código fuente proporciona un mecanismo para combinar las versiones cuando éstas se protegen.  
  
-   Archivar versiones sucesivas de los elementos controlados por código fuente. Un proveedor de control de código fuente almacena los datos que distinguen una versión de un elemento controlado por código fuente de otra. El proveedor almacena las diferencias entre versiones, así como información vital sobre la versión: cuándo fue creada, cuándo fue modificada y por quién. Cuando varios usuarios trabajan en el mismo archivo, deben utilizar la misma página de códigos para que las versiones se puedan comparar de una forma precisa. Por lo tanto, es posible recuperar cualquier versión de un elemento controlado por código fuente. También se puede designar cualquier versión como última versión de ese elemento.  
  
-   Conservar información detallada del historial y de la versión de los elementos controlados por código fuente. El control de código fuente almacena la fecha y la hora en que se creó el elemento, cuándo fue protegido o desprotegido y el usuario que realizó la acción.  
  
-   Colaborar en varios proyectos. El hecho de compartir archivos permite que varios proyectos compartan elementos controlados por código fuente. Los cambios realizados en un elemento compartido se reflejan en todos los proyectos que comparten ese elemento.  
  
-   Automatizar operaciones de control de código fuente que se repiten con frecuencia. Un proveedor de control de código fuente puede definir una interfaz de símbolo del sistema que sea compatible con las características clave del control de código fuente. Es posible utilizar esta interfaz en los archivos por lotes para automatizar las tareas de control de código fuente que se realizan con regularidad.  
  
-   Recuperar archivos eliminados accidentalmente. Es posible restaurar la última versión del archivo protegido en el control de código fuente.  
  
-   Ahorrar espacio en disco tanto en el cliente como en el servidor de control de código fuente. Algunos proveedores de control de código fuente, como [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe, ofrecen ahorro de espacio en disco en el servidor mediante el almacenamiento de la última versión de un archivo y las diferencias entre cada versión y la versión anterior y siguiente. En el cliente, Visual SourceSafe proporciona ahorro de espacio en disco. Puede esconder carpetas y archivos para que no se descarguen en el disco local.  
  
 Las desprotecciones y protecciones de archivos y otras operaciones de control de código fuente se realizan realmente mediante un cliente de control de código fuente, como [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. El cliente está diseñado para interactuar con el proveedor y así poner a disposición de un grupo de usuarios distribuido las funciones del proveedor. Mediante un cliente de control de código fuente, los usuarios pueden examinar los archivos almacenados por el proveedor, agregar y eliminar archivos, proteger y desproteger archivos, y recuperar copias de archivos locales.  
  
> [!NOTE]  
>  En la presente documentación se supone que se utiliza [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe como proveedor de control de código fuente. Si utiliza otro proveedor de control de código fuente, puede observar diferencias entre esta documentación y el software que ejecute. Si observa diferencias, consulte la documentación de su proveedor de control de código fuente.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tarea**|**Tema**|  
|Establecer las opciones de Control de código fuente|[Establecer las opciones de control de código fuente](../../2014/database-engine/set-source-control-options.md)|  
|Cambiar las conexiones de control de código fuente|[Cambiar las conexiones del control de código fuente](../../2014/database-engine/change-source-control-connections.md)|  
|Excluir archivos de control de código fuente|[Excluir archivos desde el control de código fuente](../../2014/database-engine/exclude-files-from-source-control.md)|  
  
  
