---
title: Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79d3fbb53d59c9a85ba7246e7e20179eb25085e9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37292805"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta)
  Utilice la página **Seleccionar una tabla de dimensiones y claves** para seleccionar una tabla de dimensiones para cargar. Asigne columnas del flujo de datos a las columnas que se van a cargar.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Connection manager**  
 Seleccione un administrador de conexiones OLE DB existente de la lista o haga clic en **Nuevo** para crear uno nuevo.  
  
> [!NOTE]  
>  El Asistente para dimensiones de variación lenta solamente admite los administradores de conexiones OLE DB y las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nueva**  
 Use el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** para seleccionar un administrador de conexiones existente o haga clic en **Nuevo** para crear una nueva conexión OLE DB.  
  
 **Tabla o vista**  
 Seleccione una tabla o una vista de la lista.  
  
 **Columnas de entrada**  
 Seleccione las columnas de la lista de columnas de entrada para las que desea especificar asignaciones.  
  
 **Columnas de dimensión**  
 Muestra todas las columnas de dimensión disponibles.  
  
 **Tipo de clave**  
 Seleccione una de las columnas de dimensión para que sea la clave empresarial. Es necesario disponer de una clave empresarial.  
  
## <a name="see-also"></a>Vea también  
 [Configuración de salidas con el Asistente para dimensiones de variación lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
